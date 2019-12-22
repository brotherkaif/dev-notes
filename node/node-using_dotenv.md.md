# Using dotenv
## Method
- make sure `.env` is in `.gitignore` (**important**)
- add your variable to `.env` (eg. `API_KEY=1234`)
- add `dotenv` to `package.json`
- add `dotenv` into your file and pull out the variable
## Example
```
const dotenv = require('dotenv');
dotenv.config({ path: `../../../.env` });
const API_KEY = process.env.API_KEY;

console.log(API_KEY);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MDkxNDYyOTFdfQ==
-->