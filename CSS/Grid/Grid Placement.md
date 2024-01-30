We create a grid with 4 columns

```HTML
<style>
    body {
      padding: 0;
      margin: 0;
    }
    .container {
      height: 80vh;
      display: grid;
      gap: 3rem;
      grid-template-columns: 1fr 1fr 1.5fr 1fr;
      grid-template-rows: 1fr 1fr;
    }
    .item {
      font-size: 5rem;
      color: white;
      font-family: Arial, Helvetica, sans-serif;
      background-color: blueviolet; 
      display: flex;
      justify-content: center;
      align-items: center;
    }

  </style>
 <body>
  <div class="container">
    <div class="item cowboy">🤠</div>
    <div class="item astronaut">👨‍🚀</div>
    <div class="item book">📖</div>
  </div>
</body>
```

Change the start of column `cowboy`:

```CSS
.cowboy {
      grid-column-start: 2;
    }
```

Change the size of the column `cowboy`:

```CSS
.cowboy {
      grid-column: span 2 ;
    }
```

