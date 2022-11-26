# FUNCTIONAL PROGRAMMING: Book Summary - Professor Frisby’s Mostly Adequate Guide to Functional Programming

## Resources
- [Book Repo: mostly-adequate-guide](https://github.com/MostlyAdequate/mostly-adequate-guide)
- Support Files: `$ npm i @mostly-adequate/support`

## Chapter 01: What Ever Are We Doing?
### Seagull Application Example
Consider the following scenario: A seagull application - When flocks conjoin they become a larger flock, and when they breed, they increase by the number of seagulls with whom they're breeding.

#### OOP Approach
```javascript
class Flock {
  constructor(n) {
    this.seagulls = n;
  }

  conjoin(other) {
    this.seagulls += other.seagulls;
    return this;
  }

  breed(other) {
    this.seagulls = this.seagulls * other.seagulls;
    return this;
  }
}

const flockA = new Flock(4);
const flockB = new Flock(2);
const flockC = new Flock(0);
const result = flockA
  .conjoin(flockC)
  .breed(flockB)
  .conjoin(flockA.breed(flockB))
  .seagulls;
// 32
```

##### Issues
- Difficult to follow
- Difficult to keep track of the mutating internal state
- Doesn't even arrive at the correct answer (it should be `16`)

#### Functional Approach
```javascript
const conjoin = (flockX, flockY) => flockX + flockY;
const breed = (flockX, flockY) => flockX * flockY;

const flockA = 4;
const flockB = 2;
const flockC = 0;
const result =
    conjoin(breed(flockB, conjoin(flockA, flockC)), breed(flockA, flockB));
// 16
```

##### Advantages
- Much less code
- Easier to follow
- Got the correct answer this time

### Mathmatical Properties
For clarity, let's rename `conjoin` and `breed` to `add` and `multiply`

#### Renaming Custom Functions to `add` and `multiply`
```javascript
const add = (x, y) => x + y;
const multiply = (x, y) => x * y;

const flockA = 4;
const flockB = 2;
const flockC = 0;
const result =
    add(multiply(flockB, add(flockA, flockC)), multiply(flockA, flockB));
// 16
```

#### Arithmatic Laws
```javascript
// associative
add(add(x, y), z) === add(x, add(y, z));

// commutative
add(x, y) === add(y, x);

// identity
add(x, 0) === x;

// distributive
multiply(x, add(y,z)) === add(multiply(x, y), multiply(x, z));
```

#### Refactoring
```javascript
// Original line
add(multiply(flockB, add(flockA, flockC)), multiply(flockA, flockB));

// Apply the identity property to remove the extra add
// (add(flockA, flockC) == flockA)
add(multiply(flockB, flockA), multiply(flockA, flockB));

// Apply distributive property to achieve our result
multiply(flockB, add(flockA, flockA));
```

### Summary
- Functional is a paradigm that uses a mathmatical framework
- Can result in much simpler code that is easier to read, understand and maintain
- We are trying to represent our specific problem in terms of generic, composable bits and then exploit their mathematical properties for our own benefit