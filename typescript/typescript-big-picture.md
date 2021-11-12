# TYPESCRIPT: The Big Picture

## Setup & Config

### Installing TypeScript 
```
npm install -g typescript
```

### Configuring TypeScript
- Create a `tsconfig.json` file in the root of your project

Example config:
```
{
  "compilerOptions": {
    "target": "es5",
    "outDir": "dist"
  }
}
```

### Compiling TypeScript
- In terminal run `tsc -w` to run the TypeScript compiler and have it watch for changes

## Core Concepts

### Basic JavaScript Types
- String
- Boolean
- Number
- BigInt
- Null
- Undefined
- Symbol
- Object (includes Array, Functions, Date, RegEx etc)
