https://css-tricks.com/snippets/css/a-guide-to-flexbox/
## Flex Direction
Imaging we have a div parent `container` and the child is `red`, `orange`, `yellow`, etc.
(It's set on the children container)
```CSS
<div class="container">

    <div class="red">Red</div>

    <div class="orange">Orange</div>

    <div class="yellow">Yellow</div>

    <div class="green">Green</div>

    <div class="blue">Blue</div>

    <div class="indigo">Indigo</div>

    <div class="purple">Purple</div>

  </div>
```

In CSS, if we want to make a change to a child, like set `flex-basic` we are not able to do it in .container 
```CSS
.container {
	flex-basis: 100px; WRONG
}
```


To access the child:
```CSS
.container > * {
	flex-basis: 100px; RIGHT
}
```

## Flex layout

#### order
Change the order (index) 
```CSS
.green {
	order: 1;
}
```

#### flex-wrap

If we have items and wanted it not going to the next line:
```CSS
flex-wrap: nowrap;
```
going to the next line:

```CSS
flex-wrap: wrap;
```


#### justify-content

It's set on the parent container.
```CSS
.container {
	justify-content: start
	//justify-content: end
	//justify-content: center

}
```


#### align-items

This is the position of the item.

```CSS
.container {
	align-items: start, end, center,...
}
```

#### align-content

It is similar to align-items, but only works when we have the `flex-wrap` set to `wrap`
```CSS
flex-wrap: wrap;
align-content: center;
```

