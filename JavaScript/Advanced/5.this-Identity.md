### `this`

**`this`** is the identity of the button/something that triggered the eventListener.

Ex:

```html
<h1 id="title">Drum 🥁 Kit</h1>
  <div class="set">
    <button class="w drum">w</button>
    <button class="a drum">a</button>
    <button class="s drum">s</button>
    <button class="d drum">d</button>
</h1>
```

```js
for(var i=0; i<document.querySelectorAll(".drum").length; i++){
    document.querySelectorAll("button")[i].addEventListener("click", function () {
        console.log(this);
    });
}
```

When we hit a button `w` or any button, the console return like this
```js
    <button class="w drum">w</button>
```


### use `this` to change its style
So when we click the button, it will change the color to white.

```js
for(var i=0; i<document.querySelectorAll(".drum").length; i++){
    document.querySelectorAll("button")[i].addEventListener("click", function () {
        this.style.color = "white";
    });
}
```


