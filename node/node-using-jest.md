# NODE: Using Jest

## Resources
- [Jest Homepage](https://jestjs.io) 

## Method
- add `jest` to `package.json` via `npm install --save-dev jest`
- create your test files using `*.test.js` naming convention (Jest will pick these up automatically)
- run using `jest`, or create a script under `test` in `package.json` and run `npm test`/`npm t`

## Example
Let's take a simple module called `sum.js`:
```
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

The test file would be named `sum.test.js`:
```
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

You can add the following to to your `package.json`:
```
{
  "scripts": {
    "test": "jest"
  }
}
```

Finally, run everything with `yarn test`/`npm run test`/`npm t`:
```
PASS  ./sum.test.js
✓ adds 1 + 2 to equal 3 (5ms)
```

## Cheatsheet
### Run all available tests:
`jest`

### Run the test suites from files whose paths match the given regex patterns:
`jest test_file1 path/to/test_file2.js`

### Run the tests whose names match the given regex pattern:
`jest --testNamePattern spec_name`

### Run test suites related to a given source file:
`jest --findRelatedTests path/to/source_file.js`

### Run test suites related to all uncommitted files:
`jest --onlyChanged`

### Watch files for changes and automatically re-run related tests:
`jest --watch`

### Show help:
`jest --help`
