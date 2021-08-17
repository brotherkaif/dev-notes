# Setting up a basic CRUD API with `node`

## Setup
- Install Node.js (LTS should do)
- Create a project directory, `run npm init`
- Fill out details in wizard
- You should have a `package.json` file created
- Install **express** (for creating the API) as a dependency with `npm install express`
- Install **eslint** (for linting the code) as a dev dependency with `npm install eslint -D`
- Add the script `"lint": "eslint",` to `package.json` (this allows **eslint** to be installed on the project level instead of globally)
- Initialise eslint with `npm run lint -- --init`
- Run through the wizard
- Change the script to be `"lint": "eslint .",`
- Install **nodemon** (for restarting the application when there is a code change) as a dependency with `npm install nodemon`
- Add the script `"start": "nodemon app.js",` to `package.json` (this allows nodemon to run the `app.js` file we are going to create)

You want to add the following **nodemon** config to your `package.json`:
```javascript
  "nodemonConfig": {
    "restartable": "rs",
    "ignore": [
      "node_modules/**/node_modules"
    ],
    "delay": "2500",
    "env": {
      "NODE_ENV": "development",
      "PORT": 4000
    }
  }
```

You should now be able to create your `app.js`. Here’s some sample code below:
```javascript
const express = require('express');

const app = express();

const port = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send('API is running successfully');
});

app.listen(port, () => {
  console.log(`API is listening on port: ${port}`);
});
```
