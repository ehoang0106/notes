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

