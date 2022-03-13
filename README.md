# Navigate-js
Easy client-side routing for vanilla JS sites

When you're building a single-page website without a frontend framework such as React, this small package can help you implement routing with a single function invocation.

Intended to be used when you have several anchors linking to different sections of your website, identified by an id. You want only the section whose link is clicked to be visible, while the rest should be hidden.
Ensures that the section displayed is in sync with the url, so that the browser routing (forward and back arrows) work as expected.

**Installation**
Run npm i navigate-js in your terminal.
Include import navigate-js as njs in your JS file.

**Usage**
Exports a single function which takes 3 parameters - 1 mandatory and 2 optional.
Parameter 1: A string array that contains the ids of the elements that you want to navigate between. These ids should also be the hrefs of anchors that link to those sections. Ids should be passed without the #.
Parameter 2: Optional. The id of the section that you wish to display by default. (Before any links are clicked.) If this parameter is not present, it will default to the first id in your list. Pass null if you want none of the sections to display before its link is clicked.
Parameter 3: Optional. An array of callback functions. Pass in up to one callback for each id, which will be invoked any time that page is navigated to. Each callback should be in the same array index as its corresponding id. If a callback array is passed but some ids do not have callbacks, the empty spots should be populated with null.

**Important Notes**
1. This hides all elements with an id that is in its list, other than the one whose link was clicked or who was navigated to in the browser. Any element whose id is not in the list and is not a child of elements whose ids are in the list will not be hidden by the navigation. This allows a common header, footer, etc. to be shared among all of the pages.
2. Callbacks will be invoked every time their respective page is navigated to. Callbacks will be invoked exactly as they are passed in with no additional parameters.
3. The navigate function can be invoked more than once for the same page with a second set of ids, for instance if one page has several links inside of it. See Example 2 for how this works and how it can be useful.

**Code Samples:**
Example 1:

JS file
import navigate-js as njs;

njs(['section1', 'section2', 'section3']);
//basic, without any optional parameters

njs(['section1', 'section2', 'section3'], 'section2');
//if you want section2 to be the first one displayed, before any links are clicked

njs(['section1', 'section2', 'section3'], 'section2', [callback1, null, callback3]);

function callback1() {
//code to run when section1 is opened
}

function callback3() {
//code to run when section3 is opened
}

Supporting html
![example1Html](https://user-images.githubusercontent.com/83898488/158046877-53082a14-8b7c-4f0a-9ba5-797153a5cd8d.jpg)

Example 2:
JS file
import navigate-js as njs;

njs(['section1', 'section2', 'section3'], 'section2', [callback1, callback2, callback3]);

function callback1() {
//code to run when section1 is opened
}

function callback2() {
//code to run when section2 is opened
}

function callback3() {
//code to run when section3 is opened
}

njs(['part1', 'part2', 'part3'], null);
//this allows you to route between the different pages inside section 2
//since null is passed as the second parameter, none of the elements with an id of part1, part2, or part3 will display by default

Supporting html
![example2Html](https://user-images.githubusercontent.com/83898488/158046858-f1ce6858-dae9-46c4-a159-bc4482d2dc3a.jpg)
