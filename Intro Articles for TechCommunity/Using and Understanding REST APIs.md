# Using and Understanding REST APIs

People use applications via a _user interface_ or UI; programs use other programs using an _application programming interface_ or API. Most modern applications, especially those in the cloud, have both user and application programming interfaces which make it possible to access the application's data from another program.

While technically anything that allows one program to access another is an API, for the last fifteen years or so there has been an explosion of APIs that work over the Internet following a style called "REST". This article will explain how to use these so-called "RESTful" APIs. The actual meaning of "REST" is left for the last section since it's kind of abstract and not very important for using this powerful technology, so feel free to skip it! Instead of theory, this article will begin with practical information on how to put REST APIs to use.

## Why learn to call REST services?

Learning how to call these services allows access to thousands of services from your Power Apps, Power Automate flows, Single-Page Apps, SharePoint Framework web parts, Azure Logic Apps, shell and Power Shell scripts, C# and NodeJS programs, and more.

Here are some examples of REST services to give you an idea of what's possible.

| Service | Description |
|--|--|
| [Microsoft Graph](https://docs.microsoft.com/en-us/graph/overview) | The primary API for Microsoft 365 including Teams, Planner, Azure AD, and the most commonly used features in SharePoint and Exchange online |
| [Amazon](https://developer.amazon.com/) | From Alexa to videos, Amazon has APIs for a myriad of services |
| [Bing Maps APIs](https://www.microsoft.com/en-us/maps/choose-your-bing-maps-api) | A suite of mapping APIs including REST services |
| [Ebay](https://developer.ebay.com/docs) | One of the very first REST APIs, EBay provides access to their extensive ecommerce services |
| [Facebook API](https://developers.facebook.com/docs/apis-and-sdks) | Access to Facebook services |
| [Github API](https://docs.github.com/en/rest) | Most Github operations are available via these APIs |
| [Google APIs](https://developers.google.com/apis-explorer/) | Dozens of APIs from ads to YouTube |
| [Open Weather API](https://openweathermap.org/api) | Weather conditions and forecasts |
| [Twitter API](https://developer.twitter.com/en/docs/twitter-api) | Access to Twitter services |

Here are some more compilations of popular APIs:

* [API List](https://apilist.fun/)
* [Github's collection of public APIs](https://github.com/public-apis/public-apis/blob/master/README.md)
* [Top 50 APIs from Computer Science Zone](https://www.computersciencezone.org/50-most-useful-apis-for-developers/#:~:text=%2050%20Most%20Useful%20APIs%20for%20Developers%20,The%20ability%20to%20log%20into%20a...%20More)

## How do REST APIs work?

REST APIs piggyback on the HTTP/HTTPS protocol, the same one used by web pages. Surely you've typed http about a million times by now, so you're already in practice! Generally the secure option, HTTPS, is used, but this article will generally say HTTP for brevity.

There are a number of advantages to using HTTP, including:

* Because web pages are so widely used, almost every programming environment can deal with HTTP. 
* There is a lot of infrastructure already in place to deal with HTTP, including firewalls, proxy servers, load balancers, etc; by using HTTP, REST calls can work over all of it.
* Traditional corporate networks block most protocols but nearly always have a provision for outgoing HTTP calls so users can access the world wide web.

And so this article is mostly about HTTP!

The HTTP protocol consists of _requests_ and _responses_; if you're using a public API, you'll generally be sending the _requests_ and recieving _responses_.

![Requests and Responses](./request-response.svg)

Each request and response each have:

* A URL or _Uniform Resource Locator_ - Just like the URL in a web browser except instead of a web page, it indicates the resource you want to act on within the API.
* An HTTP _verb_ - Each request includes a verb specifying what you want to do with the resource identified by the URL. For example to get a web page, use the GET verb.
* A _header_ - This is information about the request itself, such as the format of data in the _body_ portion. The header will include zero or more name-value pairs called "fields".
* A _body_ - Some requests and responses include a body for data; for example the response to a GET request for a web page includes a _body_ containing the HTML in the web page. APIs generally use [JSON](https://techcommunity.microsoft.com/t5/microsoft-365-pnp-blog/introduction-to-json/ba-p/2049369) rather than HTML in their body.
* A _status code_ and _message_ - Responses always include a status indicating if the request was successful, or if special actions (such as redirecting to a different URL) are needed.

When you browse the web, your web browser takes care of all that. When you make a REST call, you will see all these details in whatever tool you're using. This is both the good and bad of REST: it's not ideal that you have to see the plumbing behind each call, but it's great that the plumbing is so universal that it works almost anywhere.

In general, you should expect to see all of these explained in each API's documentation. At its simplest, all you have to do is copy the URL, verb, header fields and body into your tool of choice, filling in any values that are specific to your call and tell it to send the request.

The sections that follow will provide more details on each part of an HTTP request, but first let's play!

### Time to Play

It turns out that the Microsoft Graph team provides an excellent tool for experimenting with REST (and the Microsoft Graph); it's called the [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer). It's just a web page; check it out!

![Graph Explorer](./rest-graph-explorer.png)

[Add callouts and relate to the above]







