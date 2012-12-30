html2canvas
===========

#### JavaScript HTML renderer ####

 This script allows you to take "screenshots" of webpages or parts of it, directly on the users browser. The screenshot is based on the DOM and as such may not be 100% accurate to the real representation as it does not make an actual screenshot, but builds the screenshot based on the information available on the page.


###How does it work?###
The script renders the current page as a canvas image, by reading the DOM and the different styles applied to the elements.

It does <b>not require any rendering from the server</b>, as the whole image is created on the <b>clients browser</b>. However, as it is heavily dependent on the browser, this library is *not suitable* to be used on for example on node.js.
It doesn't magically circumvent and browser content policy restrictions either, so rendering cross origin content will require a <a href="https://github.com/niklasvh/html2canvas/wiki/Proxies">proxy</a> to get the content to the <a href="http://en.wikipedia.org/wiki/Same_origin_policy">same origin</a>.

The script is still in a **very experimental state**, so I don't recommend using it in a production environment nor start building applications with it yet, as there will be still major changes made.

###Browser compatibility###

The script should work fine on the following browsers:

* Firefox 3.5+
* Google Chrome
* Opera 12+
* IE9+

Note that the compatibility will most likely be increased in future builds, as many of the current restrictions have at least partial work arounds, which can be used with older browser versions.

###So what isn't included yet?###

There are still a lot of CSS properties missing, including most CSS3 properties such as <code>text-shadow</code>, <code>box-radius</code> etc. as well as all elements created by the browser, such as radio and checkbox buttons and list icons. I will compile a full list of supported elements and CSS properties soon.
 There is no support for <code>frame</code> and <code>object</code> content such as Flash.

### Usage ###
To render an `element` with html2canvas, simply call:
` html2canvas( [ element ], options);`

To access the created canvas, provide the `onrendered` event in the options which returns the canvas element as the first argument, as such:

    html2canvas( [ document.body ], {
        onrendered: function( canvas ) {
            /* canvas is the actual canvas element,
               to append it to the page call for example
               document.body.appendChild( canvas );
            */
            }
    });

### Building ###

The library uses <a href="http://gruntjs.com/">grunt</a> for building. Alternatively, you can download ready builds from the <a href="https://github.com/niklasvh/html2canvas/downloads">downloads page</a>.

Run the full build process (including lint, qunit and webdriver tests):

    $ grunt

Skip lint and tests and simply build from source:

    $ grunt concat
    $ grunt min

### Running tests ###

The library has two sets of tests. The first set is a number of qunit tests that check that different values parsed by browsers are correctly converted in html2canvas. To run these tests with grunt you'll need <a href="http://phantomjs.org/">phantomjs</a>.

The other set of tests run Firefox, Chrome and Internet Explorer with <a href="https://github.com/niklasvh/webdriver.js">webdriver</a>. The selenium standalone server (runs on Java) is required for these tests and can be downloaded from <a href="http://code.google.com/p/selenium/downloads/list">here</a>. They capture an actual screenshot from the test pages and compare the image to the screenshot created by html2canvas and calculate the percentage differences. These tests generally aren't expected to provide 100% matches, but while commiting changes, these should generally not go decrease from the baseline values.

If you didn't download `html2canvas` from `npm`, start by downloading the dependencies:

    $ npm update

Run qunit tests:

    $ grunt test

Run webdriver tests:

    $ java -jar /path/to/selenium-server-standalone-2.xx.x.jar
    $ grunt webdriver

Commiting improvements in baseline values:

    $ grunt webdriver:baseline

### Examples ###

For more information and examples, please visit the <a href="http://html2canvas.hertzen.com">homepage</a> or try the <a href="http://html2canvas.hertzen.com/screenshots.html">test console</a>.

### Changelog ###

v0.40 -
 * Switched to using grunt for building
 * Reformatted all tests to small units to test specific features
 * Added rendering tests with <a href="https://github.com/niklasvh/webdriver.js">webdriver</a>

v0.34 - 26.6.2012

* Removed (last?) jQuery dependencies (<a href="https://github.com/niklasvh/html2canvas/commit/343b86705fe163766fcf735eb0217130e4bd5b17">niklasvh</a>)
* SVG-powered rendering (<a href="https://github.com/niklasvh/html2canvas/commit/67d3e0d0f59a5a654caf71a2e3be6494ff146c75">niklasvh</a>)
* Radial gradients (<a href="https://github.com/niklasvh/html2canvas/commit/4f22c18043a73c0c3bbf3b5e4d62714c56acd3c7">SunboX</a>)
* Split renderers to their own objects (<a href="https://github.com/niklasvh/html2canvas/commit/94f2f799a457cd29a21cc56ef8c06f1697866739">niklasvh</a>)
* Simplified API, cleaned up code (<a href="https://github.com/niklasvh/html2canvas/commit/c7d526c9eaa6a4abf4754d205fe1dee360c7660e">niklasvh</a>)

v0.33 - 2.3.2012

* SVG taint fix, and additional taint testing options for rendering (<a href="https://github.com/niklasvh/html2canvas/commit/2dc8b9385e656696cb019d615bdfa1d98b17d5d4">niklasvh</a>)
* Added support for CORS images and option to create canvas as tainted (<a href="https://github.com/niklasvh/html2canvas/commit/3ad49efa0032cde25c6ed32a39e35d1505d3b2ef">niklasvh</a>)
* Improved minification saved ~1K! (<a href="https://github.com/cobexer/html2canvas/commit/b82be022b2b9240bd503e078ac980bde2b953e43">cobexer</a>)
* Added integrated support for Flashcanvas (<a href="https://github.com/niklasvh/html2canvas/commit/e9257191519f67d74fd5e364d8dee3c0963ba5fc">niklasvh</a>)
* Fixed a variety of legacy IE bugs (<a href="https://github.com/niklasvh/html2canvas/commit/b65357c55d0701017bafcd357bc654b54d458f8f">niklasvh</a>)

v0.32 - 20.2.2012

* Added changelog!
* Added bookmarklet (<a href="https://github.com/niklasvh/html2canvas/commit/b320dd306e1a2d32a3bc5a71b6ebf6d8c060cde5">cobexer</a>)
* Option to select single element to render (<a href="https://github.com/niklasvh/html2canvas/commit/0cb252ada91c84ef411288b317c03e97da1f12ad">niklasvh</a>)
* Fixed closure compiler warnings (<a href="https://github.com/niklasvh/html2canvas/commit/36ff1ec7aadcbdf66851a0b77f0b9e87e4a8e4a1">cobexer</a>)
* Enable profiling in FF (<a href="https://github.com/niklasvh/html2canvas/commit/bbd75286a8406cf9e5aea01fdb7950d547edefb9">cobexer</a>)
