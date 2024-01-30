
Ex: 

```js
var houseKeeper1 = {
	yearsOfExperience: 12,
	name: "Jane",
	cleaning: ["bathroom", "lobby", "bedroom"]
}
```

```js
houseKepper1.name;
// return "Jane"
```

```js
houseKeeper1.cleaning;
// return ["bathroom", "lobby", "bedroom"]
```

### Constructor Function

The name of this has to be capitalize of the first each word

```js
function BellBoy (name, age, hasWorkPermit, languages){
	this.name = name;
	this.age = age;
	this.hasWorkPermit = hasWorkPermit;
	this.languages = languages
}
```

### Initialize Object

```js
var bellBoy1 = new BellBoy("Timmy", 19, true, ["French", "English"]);
```

