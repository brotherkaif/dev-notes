# NODE: Using dotenv

## Method
- add your variable to `.env` (eg. `API_KEY=1234`)
- add `dotenv` to `package.json`
- add `dotenv` into your file and pull out the variable

## Example
```javascript
const dotenv = require('dotenv');
dotenv.config({ path: `../../../.env` });
const API_KEY = process.env.API_KEY;

console.log(API_KEY);
```
