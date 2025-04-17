```PowerShell
Set-Location -path D:\CodeNotes\CodeNotes
```

**Change style for a specific element**

The bracket square after the HTML element to select that specific style for that element

Ex:
```HTML
HTML 
<p draggble="true"> This is first paragrah </p> 
<p draggble="false"> This is second paragrah </p>
```
Only the first paragraph has the color red.
```CSS
.p[draggble="true"] {
color: red
}
```


# Advance CSS

## Responsive Websites

There is 4 component to create a responsive website `Media Queires`, `Css Grid`, `CSS Flexbox`, `External Framework e.g Bootstrap`.

### Media Query

```CSS
@media (max-width: 600px){
	/*CSS for screens below or equal to 600px wide*/
	h1 {
		font-size: 15px;
	}
}
```

```CSS
@media (max-width: 600px) {
	h1 {
		font-size: 20px;
	}
}
```
`max-width` is a breakpoint, everything less than or equal to the break point, the styling will be applied.
`min-width` is a same thing.

Combine `min-width` and `max-width`
```CSS
@media (min-width: 600px) and (max-width: 900px) {
	/*Styling*/
}
```



### CSS Grid

Create a div that contains another 5 div tags
- HTML
```HTML
<div> class="grid-container">
	<div class="first card"></div>
	<div class="card"></div>
	<div class="card"></div>
	<div class="card"></div>
	<div class="card"></div>
</div>
```
- CSS
```CSS
.grid-container {
	display:grid;
	grid-template-columns: 1fr 1fr; /*<- 2 columns*/ 
	grid-template-rows: 100px 200px 200px; /* 3 rows*/
	gap: 30px;
	
}

.first {
	grid-column: span 2;
}

.card {
	background-color: blue;
}
```

### CSS Flexbox

![[Pasted image 20240117102339.png]]
### CSS Bootstrap Framework

![[Pasted image 20240117102737.png]]

