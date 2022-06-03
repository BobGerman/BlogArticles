

This article will be about how to run inline code within an ES module. The code will run ONCE on the page no matter how many ES modules import the ES module containing it.

Here is the model code, from teamsHelpers.js:

~~~javascript
// Inline code to set theme on any page that uses this module
let initialThemeLoaded = false;
(async () => {
    if (!initialThemeLoaded) {
        initialThemeLoaded = true;
        // Set the initial theme
    }
})();
~~~