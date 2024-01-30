## addEventListener()

```js
addEventListener(type, listener)
addEventListener(type, listener, options)
addEventListener(type, listener, useCapture)

```
Document: [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
`type`: [type](https://developer.mozilla.org/en-US/docs/Web/Events)

Ex:

Instead of pass the function in side the `addEventListener`, we only add the **name of its**. Because if we pass the function with parentheses, it will automatically run when refresh the page.

// WRONG

```js
document.querySelector("button").addEventListener("click", handleClick);
function handleClick() {
    alert("I got clicked!");
}
```

// RIGHT

```js
document.querySelector("button").addEventListener("click", handleClick);
function handleClick() {
    alert("I got clicked!");
}
```

Ex:

```html
<div class="set">
    <button class="w drum">w</button>
</div>
```

```js
for(var i=0; i<document.querySelectorAll(".drum").length; i++){
    document.querySelectorAll("button")[i].addEventListener("click", function () {
        alert("I got clicked!");
    });
}
```

## HTMLAudioElement

[HTMLAudioElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement)

Syntax:
```js
mysound = new Audio([URL_STRING]);
```
Ex:
```js
var audio = new Audio("car_horn.wav");
audio.play();
```
