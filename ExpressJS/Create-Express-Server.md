
1. Create directory.
2. Create `index.js` file.
3. Initialize NPM.
4. Install the Express package.
5. Write Server Application in index.js.
6. Start server


# 1. Create directory

```PowerShell
mkdir "Express Server"
```
# 2. Create `index.js` file

```PowerShell
touch index.js
```

# 3. Initialize NPM

[Install ExpressJS](https://expressjs.com/en/starter/installing.html)

```PS
npm init -y
```
# 4. Install Express

```PowerShell
npm install express
```

# 5. Write server Express

```js
import express from "express";
const app = express();
const port = 3000;

app.listen(port, () => {
  console.log(`Server running on port ${port}.`);
});
```

# 6. Start Server 

```js
http://localhost:3000/
```
