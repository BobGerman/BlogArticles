
# Caching Promises

## Singleton promises

It all started when I needed to initialize the Microsoft Teams JavaScript SDK for use in a web application. It's just a simple call in the browser:

~~~javascript
await microsoftTeams.app.initialize();
~~~

Now as you may know, the `await` keyword in Javascript waits for a _promise_, which is an object that represents the completion of some asynchronous operation. If you're new to this, I wrote [this article](https://bob1german.com/2015/03/16/understanding-javascript-promises/) on promises a while ago.

Anyway, the `initialize()` function returns a promise, and the `await` keyword tells Javascript to wait until the SDK resolves the promise before continuing.

This is all pretty easy, but the docs say you should only call `initialize()` once and my app is a bit  complex, with calls coming from multiple UI components that are rendered in parallel. So to prevent the multiple calls, I reached into my bag of geeky developer tricks and made this little function so it would only be called once:

~~~javascript
let isInitialized = false;
export async function ensureTeamsSdkInitialized() {
    if (!isInitialized) {
        await microsoftTeams.app.initialize();
        isInitialized = true;
    }
}
~~~

And whenever I want to initialize, I do this:

~~~javascript
await ensureTeamsSdkInitialized();
~~~

Pretty slick, right? I can call the function as often as I wish and it will only initialize the SDK the first time, right? Right???

Well, no not really. Maybe the problem is obvious to you, but at first I was sure this would work and was surprised when my code called `initialize()` twice, once for each of the two components that used it. There's a race condition here!

___________

_Self: "Say what, Javascript is single-threaded, how can there be a race condition?"_

_Other self: "You're still thinking like a synchronous programmer!"_

_Self: "Yeah, having multiple threads made parallel operations so much easier, right? Well, maybe not, there was locking and semaphores and all that stuff. And the overhead of a whole register set and stack per thread. Anyway, I have to use async on a web page or it will freeze up while waiting for things, right?"_

_Other self: "Right. Now look closer. Race conditions don't require threads, just concurrency."_

____

To clarify, a _race condition_ is when the outcome of some operation is dependent on the timing of other, uncontrollable events. In this case, if one component has called `ensureTeamsSdkInitialized()` and it's waiting for the call to `initialize()` to complete, and then another component makes the same call, the `isInitialized` flag will still be false and we'll call `initialize()` again.

In this scenario, I had two promises for each caller - four promises in all - two for the `ensureTeamsSdkInitialized()` calls and two more for the `initialize()` calls! That's a lot of promises for code that doesn't work right!

The solution for this is to use only one promise and store it in a singleton like this:

~~~javascript
let teamsInitPromise;
export function ensureTeamsSdkInitialized() {
    if (!teamsInitPromise) {
        teamsInitPromise = microsoftTeams.app.initialize();
    }
    return teamsInitPromise;
}
~~~

This works because `microsoftTeams.app.initialize()` returns a promise, and we don't need to `await` it right away. Instead, we can save it and also return it for our caller to `await`. When the SDK resolves the promise, all of the callers will wake up and the `initialize()` call will have happened only once. Even when a caller comes along later, the same promise will immediately resolve and the caller won't know or care.

Notice that I no longer needed the `async` keyword on the `ensureTeamsSdkInitialized()` function because it's not doing any `awaits`; it requests a promise and returns it to its caller as-is.

## Caching promises instead of data

Now suppose your application needs to `fetch` a bunch of data using a REST call, and this call may be used in various parts of the code. I ran into this exact situation in the same application. I needed information about the user's profile in two different web components, but didn't want the overhead of doing the `fetch` twice.

I started with a simple caching mechanism where I stored the user profile data in a singleton, but I noticed I was still doing two fetches whenever the page rendered. This was because two web components requested the data when the page was loaded, before the data was received and cached. I considered some complex logic to keep track of this but realized it's already built into the promise! By caching the promise, I was able to fetch the data only once.

~~~javascript
let getUserProfilePromise;
export function getUserProfile() {
    if (!getUserProfilePromise) {
        getUserProfilePromise = getUserProfile2();
    }
    return getUserProfilePromise;
}

async function getUserProfile2() {
    // Fetch the data
    return userProfile;
}
~~~

## Bonus content: Curt's Caching Corollaries

All this reminds me of some really helpful caching advice I got from my friend [Curt Devlin](https://www.linkedin.com/in/curt-devlin-20aa81/) ages ago. This is my take on his advice, with a title I made up because I admire alliteration.

1. Only cache data that changes less frequently than you'll consume it. This might sound obvious but I've seen people cache things that are only used once! Overcome your urge to cache everything and only use caching when you know there's an efficiency to be gained. Along with that, it helps if the data changes predictably so you can invalidate the cache, or if consumers can deal with slightly stale data.

2. Always cache data as close to the consumer as possible. If there are multiple services or layers involved, generally you're better off caching close to the caller and avoiding the extra calls to the underlying services each time.
 
   For example, if your web service reads from a database, it would be better to cache the data in the web server than in the database server to avoid copying it between servers each time.

3. Always cache data in its most processed form. For example, suppose you want to read something from a database and then format it as HTML. Why cache the raw data and then rebuild the HTML each time? You'll waste cycles generating the exact same HTML each time; better to cache the data after it's been processed.

## Postscript

Come to think of it, if I had remembered Curt's Caching Corollaries I might have gone directly to caching promises instead of trying to cache the data. Curt's 3rd corollary applies here! Indeed, a _promise for data_ is a more "processed" form that adds synchronization based on the data's availability in time. By not accounting for that, I introduced false cache misses and failed to speed up the initial render of my web application.

Thanks for reading and if you like this article, feel free to cache it for future use!
