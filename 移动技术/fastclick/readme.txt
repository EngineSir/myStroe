FastClick 消除触屏版click事件的300ms延迟
FastClick is a simple, easy-to-use library for eliminating the 300ms delay between a physical tap and the firing of a click event on mobile browsers. The aim is to make your application feel less laggy and more responsive while avoiding any interference with your current logic.

FastClick is developed by FT Labs, part of the Financial Times.

Explication en fran?ais.

日本語で説明。

Why does the delay exist?

According to Google:

...mobile browsers will wait approximately 300ms from the time that you tap the button to fire the click event. The reason for this is that the browser is waiting to see if you are actually performing a double tap.
Compatibility

The library has been deployed as part of the FT Web App and is tried and tested on the following mobile browsers:

Mobile Safari on iOS 3 and upwards
Chrome on iOS 5 and upwards
Chrome on Android (ICS)
Opera Mobile 11.5 and upwards
Android Browser since Android 2
PlayBook OS 1 and upwards
When it isn't needed

FastClick doesn't attach any listeners on desktop browsers.

Chrome 32+ on Android with width=device-width in the viewport meta tag doesn't have a 300ms delay, therefore listeners aren't attached.

<meta name="viewport" content="width=device-width, initial-scale=1">
Same goes for Chrome on Android (all versions) with user-scalable=no in the viewport meta tag. But be aware that user-scalable=no also disables pinch zooming, which may be an accessibility concern.

For IE10, you can use -ms-touch-action: none to disable double-tap-to-zoom on certain elements (like links and buttons) as described in this MSDN blog post.

Usage

Include fastclick.js in your JavaScript bundle or add it to your HTML page like this:

<script type='application/javascript' src='/path/to/fastclick.js'></script>
The script must be loaded prior to instantiating FastClick on any element of the page.

To instantiate FastClick on the body, which is the recommended method of use:

window.addEventListener('load', function() {
    FastClick.attach(document.body);
}, false);
Don't forget to add a shim for addEventListener if you want to support IE8 and below.

Otherwise, if you're using jQuery:

$(function() {
    FastClick.attach(document.body);
});
If you're using Browserify or another CommonJS-style module system, the FastClick.attach function will be returned when you call require('fastclick'). As a result, the easiest way to use FastClick with these loaders is as follows:

var attachFastClick = require('fastclick');
attachFastClick(document.body);
Minified

Run make to build a minified version of FastClick using the Closure Compiler REST API. The minified file is saved to build/fastclick.min.js or you can download a pre-minified version.

Note: the pre-minified version is built using our build service which exposes the FastClick object through Origami.fastclick and will have the Browserify/CommonJS API (see above).

var attachFastClick = Origami.fastclick;
attachFastClick(document.body);
AMD

FastClick has AMD (Asynchronous Module Definition) support. This allows it to be lazy-loaded with an AMD loader, such as RequireJS. Note that when using the AMD style require, the full FastClick object will be returned, not FastClick.attach

var FastClick = require('fastclick');
FastClick(document.body, options);
Package managers

You can install FastClick using Component, npm or Bower.

For Ruby, there's a third-party gem called fastclick-rails. For .NET there's a NuGet package.

Advanced

Ignore certain elements with needsclick

Sometimes you need FastClick to ignore certain elements. You can do this easily by adding the needsclick class.

<a class="needsclick">Ignored by FastClick</a>
Use case 1: non-synthetic click required

Internally, FastClick uses document.createEvent to fire a synthetic click event as soon as touchend is fired by the browser. It then suppresses the additional click event created by the browser after that. In some cases, the non-synthetic click event created by the browser is required, as described in the triggering focus example.

This is where the needsclick class comes in. Add the class to any element that requires a non-synthetic click.

Use case 2: Twitter Bootstrap 2.2.2 dropdowns

Another example of when to use the needsclick class is with dropdowns in Twitter Bootstrap 2.2.2. Bootstrap add its own touchstart listener for dropdowns, so you want to tell FastClick to ignore those. If you don't, touch devices will automatically close the dropdown as soon as it is clicked, because both FastClick and Bootstrap execute the synthetic click, one opens the dropdown, the second closes it immediately after.

<a class="dropdown-toggle needsclick" data-toggle="dropdown">Dropdown</a>
Examples

FastClick is designed to cope with many different browser oddities. Here are some examples to illustrate this:

basic use showing the increase in perceived responsiveness
triggering focus on an input element from a click handler
input element which never receives clicks but gets fast focus
Tests

There are no automated tests. The files in tests/ are manual reduced test cases. We've had a think about how best to test these cases, but they tend to be very browser/device specific and sometimes subjective which means it's not so trivial to test.

Credits and collaboration

FastClick is maintained by Rowan Beentje, Matthew Caruana Galizia and Matthew Andrews at FT Labs. All open source code released by FT Labs is licenced under the MIT licence. We welcome comments, feedback and suggestions. Please feel free to raise an issue or pull request.