
## npm init

```js
npm init
```

## npm install package

```
npm install [package name]
```

## enable ES Module

Go to `package.json` > below the `"main": "index.js"`, insert
`"type": "module"` then save

Instead of

```js
var generateName = require('sillyname');
var sillyName = generateName();
```

We can use

```js
import generateName from "sillyname";
```


