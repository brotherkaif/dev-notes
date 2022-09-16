# TYPESCRIPT: The Big Picture

## Setup & Config

### Installing TypeScript

```bash
npm install -g typescript
```

### Configuring TypeScript

- Create a `tsconfig.json` file in the root of your project

Example config:

```json
{
  "compilerOptions": {
    "target": "es5",
    "outDir": "dist"
  }
}
```

### Compiling TypeScript

- In terminal run `tsc -w` to run the TypeScript compiler and have it watch for changes

## The Basics

### Basic JavaScript Types

- String
- Boolean
- Number
- BigInt
- Null
- Undefined
- Symbol
- Object (includes Array, Functions, Date, RegEx etc)

### Declaring types in variables

- Append the variable declaration with `: TYPE`
- Once specified, it is not possible to reassign with a different type

```
let someVariable: string = "this can only be a string!";

someVariable = 666; // this will not work!
```

### Declaring types in Functions

- You can specify the types for the arguments of a declared function
- You can also specify the return types for the function too
- Once declared, it will also be possible to peek at the specification using the LSP hover function

```
// here, we specify that this function is just going to return an object
function aFunction(anArgument: string): object {
  // function logic
}

// we can do better, we can specify the individual parameter types within the object itself
function aBetterFunction(anArgument: string): {
  aReturnedParameter: string; // NOTE: this is a semi-colon
  anotherReturnedParameter: number;
} {
  // function logic
}
```

### Type inference

- You don't need to specify the type for everything
- In some cases, the type can be _inferred_ from other type declarations

```
// here, we specify that this function is going to return an object with a string parameter
function aFunction(anArgument: string): {
  aReturnedParameter: string;
} {
  // function logic
}

// if we were to hover over `inferredVariableType`, we'll see that the LSP has figured out the type from the `aFunction` type declaration we made earlier
let inferredVariableType = aFunction(anArgument);

// LSP will even help with autocomplete in this case and only suggest the option of `.aReturnedParameter` when interacting with `inferredVariableType`
```

### Type casting

- If you would rather specify the type of a value instead of a variable (and let Type inference take over) you can use the `as` keyword

```
// instead of...
let aTypedVariable: number = 425;

// you can do...
let aCastValue = 425 as number;
```

### Gradual Typing

- If you _really_ want to, you can tell TypeScript to not enforce typing (which you can then specify later) by using the `any` type
- Be careful using this! Question why you are bypassing the entire point of TypeScript if you are using this

```
// doing this...
let aTypedVariable: any = 425;
let aCastValue = 666 as any;

// let's you do this...
aTypedVariable = "I'm a string now!";
aCastValue = "Same here!";

// BUT, if you're doing this, ask yourself 'why?'
```

## Defining Custom Types

### Defining Interfaces

Complex types (e.g. defining the subtypes within an object) can also be defined using Interfaces

Consider the following:

```
function getInventoryItem(trackingNumber: string): {
  displayName: string;
  inventoryType: string;
  trackingNumber: string;
  createDate: Date;
  originalCost: number;
} {
  // function logic
}

function saveInventoryItem(item) {
  // function logic
}
```

Instead, we could create an Interface for `InventoryItem` which helps better convey the nature of the object being passed around:

```
interface InventoryItem {
  displayName: string;
  inventoryType: string;
  trackingNumber: string;
  createDate: Date;
  originalCost: number;
}

function getInventoryItem(trackingNumber: string): InventoryItem {
  // function logic
}

function saveInventoryItem(item: InventoryItem) {
  // function logic
}
```

By doing this, `InventoryItem` can be another type that you can use in the same way you use primitive types in TypeScript.

NOTE: Interface definitions won't appear in the final compiled code, they are used by the LSP to provide diagnostic utilities when working in the editor.

### Enhancing Interface Definitions

- Interfaces respect 'duck typing', meaning that if you manually construct an entity that follows the same type definition, TypeScript will accept it
- Interface properties can be made optional by appending a `?`
- Interface properties can be made read only by prepending `readonly`
- You can also define interface methods (see syntax example below)

```
interface InventoryItem {
  displayName: string;
  inventoryType: string;
  trackingNumber: string;
  readonly createDate: Date; // this is readonly (see `saveInventoryItem` below)
  originalCost?: number; // this is optional

  // one way to define interface methods
  addNote?(note: string): string;

  // another way to define interface methods
  anotherAddNote?: (note: string) => string;
}

function saveInventoryItem(item: InventoryItem) {
  // function logic
  item.createDate = new Date(); // THIS WILL NOT WORK as this parameter has been defined as readonly
}

// The below will work because the argument satifies all of the requirements of the type defined in the interface
saveInventoryItem({
  displayName: "Display Name",
  inventoryType: "Inventory Type",
  trackingNumber: "Tracking Number",
  readonly createDate: new Date(),
});
```

### Restricting Values

#### Enum Restriction

Consider the following:

```
interface InventoryItem {
  type: string;
}
```

If we wanted to restrict the value of `type`, we could define an enum:

```
enum InventoryItemType {
  Computer, // will assign 0
  Furniture, // will assign 1
}

interface InventoryItem {
  type: InventoryItemType;
}

saveInventoryItem({
  type: InventoryItemType.Computer, // will assign 0
})
```

By default, TypeScript will assign the `Computer` and `Furniture` to `0` and `1` respectively. THIS MIGHT NOT BE WHAT WE WANT!

To explicitly have enums map to values, do the following:

```
enum InventoryItemType {
  Computer = 'com', // will assign the string 'com'
  Furniture = 'furn', // will assign the string 'furn'
}

interface InventoryItem {
  type: InventoryItemType;
}

saveInventoryItem({
  type: InventoryItemType.Computer, // will assign the string 'com'
})
```

#### Literal Type Restriction

An alternative (and simpler) pattern for restrictions is to use literal types using the pipe `|` symbol.

Consider the same `enum` example refactored to use literal types:

```
interface InventoryItem {
  type: 'com' | 'furn';
}

saveInventoryItem({
  type: 'com' // LSP will warn against values outside of this restriction
})
```

### Multi-Type Variables

You can define multi-type variables using **Union Types**:

```
let originalCost: number | string = 420;
```

You can also save the combination of types:

```
type Cost = number | string;
let originalCost: Cost = 420;
```

HOWEVER, this can cause problems in some situations:

```
type Cost = number | string;
let originalCost: Cost;

// This WON'T work because originalCost can also be a string
let cost: number = originalCost;

// A solution to this could be...
if (typeof originalCost === 'number') {
  let cost: number = originalCost;
}

// TypeScript is smart enough to recognise that originalCost can only be a number in this pattern
```
