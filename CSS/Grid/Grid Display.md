Use grid:

```CSS
.container {
	display: grid;
}
```

set the columns and rows:

`fr`: fractional size
```CSS
.container {
	display: grid;
	grid-template-columns: 1fr 2fr;
	grid-template-rows: 1fr 2fr;
}
```


Example using grid to make a chess board

```HTML
<div class="container">
    <div class="white"></div>
    <div class="black"></div>
    <div class="white"></div>
    <div class="black"></div>
    <div class="white"></div>
    <div class="black"></div>
    <div class="white"></div>
    <div class="black"></div>
    <div class="black"></div>
    <div class="white"></div>
    <div class="black"></div>
    <div class="white"></div>
    <div class="black"></div>
    <div class="white"></div>
    <div class="black"></div>
  </div>
```

```CSS
.container {

      width: 800px;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    }
    .white {

      height: 100px;
      width: 100px;
      background-color: #f0d9b5;
    }
    .black {
      height: 100px;
      width: 100px;
      background-color: #b58863;
    }
```

