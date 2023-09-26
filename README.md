# ElementPicker.js

Forked from https://github.com/AlienKevin/html-element-picker for custom mods:
 - hoverBox & hoverBoxInfo
 - styles
 - more getters
 - pass event on trigger
 - ... more

Many thanks to [https://github.com/AlienKevin](https://github.com/AlienKevin) for the wonderful work. :clap: :pray:


# -- ORIGINAL README FOLLOWS --

# html-element-picker
**Pick and highlight any HTML element on a page using only Vanilla JS. Hovered elements are automatically highlighted in the color you want. Tested in Chrome, Firefox, and Opera, does not work in IE.**

# Installation
## NPM
`npm install html-element-picker`

## CDN
Append the one of the following scripts at the end of `body` tag

**jsDelivr**

```html
<script src="https://cdn.jsdelivr.net/npm/html-element-picker@latest"></script>
```
**Unpkg**
```html
<script src="https://unpkg.com/html-element-picker@latest"></script>
```

# Update
Because of the usual 24-hour cache by CDN providers, you should replace the @latest tag with @(the latest version number) for immediate update to the latest version. It's always the safest to use the current stable version @1.0.4.

# Support
See the [html-element-picker API documentation](https://alienkevin.github.io/html-element-picker/docs/index.html).

# Usage
After importing html-element-picker, instantiate the ElementPicker class with optional configurations.
```js
new ElementPicker(options);
```
The default configurations are
```js
{
container: document.body,
selectors: "*",
background: "rgba(153, 235, 255, 0.5)",
borderWidth: 5,
transition: "all 150ms ease",
ignoreElements: [document.body],
action: {}
}
```
## container (HTMLElement)
`container` is the boundary of the element picker. No highlights will be shown on mouse hover outside the container. Defaults to the document body.
## selectors (String)
`selectors` serve as the filter for the element picker. Only elements matching the CSS rule specified in the `selectors` string will be highlighted. Defaults to accepting all elements ("*", star operator).
## background (String)
`background` specifies the background color of the higlight when an element is hovered. You should always set a **transparent** color using `"rgba(...)"` or `"hsla(...)"` so as not to block the hovered element. Same as setting `elementPicker.hoverBox.style.background`. Defaults to light blue.
## borderWidth (Integer)
`borderWidth` indicates the width of the highlight box border (in **px**) that covers the hovered element. Pass in a positive value to enlarge the highlight box and a negative to decrease the size (smaller than the hovered element). Zero means no border or same size as the hovered element. Defaults to 5px.
## transition (String)
`transition` specifies the animation when the highlight box transfer to another hovered element. Same as setting `elementPicker.hoverBox.style.transition`. Pass in `""` (empty string) to disable transition. Defaults to `"all 150ms ease"`.
## ignoreElements (Array of HTMLElement)
`ignoreElements` lists the elements to **not** highlight when being hovered over. Add, remove, modify elements in this property same as a normal array (`push`, `pop`, etc). The order of elements does not matter. Defaults to the document body.
## action (Object with two properties)
`action` indicates a callback function to run when an event is triggered and **the target element is being picked up by the element picker**, meaning only elements that are accepted by the picker will trigger the callback. `trigger` is a `String` with possible event names such as `"click"`, `"dblclick"`, `"mouseover"`, etc. `callback` is a function given a `target` parameter when triggered which contains the hovered element. Sample `callback` functions are:
```js
(function (target) {
    target.remove();
})
```
```js
(function (target) {
    target.style.fontSize = "50px";
})
```
```js
(function (target) {
    target.classList.toggle("highlight");
})
```
A full `action` option can look like:
```js
action: {
    trigger: "click",
    callback: (function (target) {
        target.classList.toggle("highlight");
    })
}
```
You must **surround the `callback` function with parentheses** just like Immediately Invoked Function Expressions (IIFEs). Defaults to no action (empty Object).

## Dynamic Update
All of the above options can be **dynamically** updated in Javascript at runtime. Element picker will respond immediately to any configuration change.