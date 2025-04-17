[NodeJS Doc](https://nodejs.org/docs/latest/api/)

## Import File System module

```js
const fs = require("fs");
```

## Write file

```js
fs.writeFile("message.txt", "Hello from NodeJS!", (err) => {
	if (err) throw err;
	console.log("The file has been saved");
});
```

