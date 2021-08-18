# Setting up a basic CRUD API with `node`

## Setup
- Install Node.js (LTS should do)
- Create a project directory, run `npm init`
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
## Creating a Router
A **Router** allows you to perform middleware and routing functions. For more info, refer to the [Express Router docs page](http://expressjs.com/en/5x/api.html#router).

Create a router instance:
```javascript
// you can put this up top before you assign port
const cakeRouter = express.Router();
```

## Implementing HTTP GET
### Specify the route
Using your **Router** instance, specify a route for the `GET` request:
```javascript
// this router can have multiple routes/paths implemented
cakeRouter.route('/cakes')
    .get((req, res) => {
	// moving the response payload out into a separate const is good practice
	const response = { hello: 'This is my API' };

	res.json(response);
    });
```
Notes:
- `get()` works in the same way we specified `app.get()` earlier
- `res.json()` sends a `json` response back instead of 	`res.send()` which was just plain text

### Wire up the router
After specifying the routes, use the `.use()` method on the `express()` instance created:
```javascript
app.use('/api', cakeRouter);
```
Notes:
- The above will generate the endpoint `.../api/cakes`
- You can use this to create multiple API versions (e.g. by specifying `/api/v1`)
