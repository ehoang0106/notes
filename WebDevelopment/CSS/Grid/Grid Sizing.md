### Grid auto
We can define `grid-template-columns` and `grid-template-rows` by using `auto` keyword.
It's going to give us a responsiveness. 

- Each `column` is going to try and fit to `100%` of the horizontal available space.
- Each `row` is going to try and fit the content (it is not the same with column)

```HTML
<div class="grid-container">
	<div class="grid-item">1</div>
	<div class="grid-item">2</div>
	<div class="grid-item">3</div>
</div>
```

```CSS
.grid-containter {
	display: grid;
	grid-template-rows: 100px auto;
	grid-template-columns: 200px auto;
}
```

### Grid fractional


```CSS
.container {
	display: grid;
	grid-template-columns: 1fr 2fr;
	grid-template-rows: 1fr 2fr;
}
```


### Grid min/max
**Min/Max function** 

```CSS
.grid-container {
	display: grid;
	grid-template-rows: 200px 400px;
	grid-template-columns: 200px minmax(400px,800px);
}
```
Minimum width and maximum width of the columns we want to be
**Repeat function**
```CSS
.grid-container {
	display: grid;
	grid-template-rows: repeat(2, 200px);
	grid-template-columns: repeat(2, 100px);
}
```

