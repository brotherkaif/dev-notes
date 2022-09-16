# TYPESCRIPT: Configuring, Compiling and Debugging

## Scaffolding an Environment for TypeScript Compilation

### Installing TypeScript

#### Understanding TypeScript Installation

- TypeScript can be located in any folder and one workstation can have multiple versions
- TypeScript is an NPM (Node.js) package
- TypeScript is installed through the command line via NPM
- Different versions can be installed locally, plus one global version

#### Multiple TypeScript Versions

Each TypeScript project on a workstation can be of a different version. There can also be one globally installed version of TypeScript.

- **Local Version:** Found within a project's directory, only used by that project
- **Global Version:** Fallback for where there is no local version
- **Embedded Version:** Fixed version built into some software (i.e. VSCode, WebStorm)

##### Installing TypeScript Globally

```bash
npm install -g typescript@4.2.4
```

**Note:** It is considered good practice to not have a global version of TypeScript installed on your workstation to ensure that the version of TypeScript being run is the local project version.

##### Installing TypeScript Locally

```bash
npm install --save-dev typescript@4.2.4
```

### Executing the TypeScript Compiler

#### What is the TypeScript Compiler?

- Turns TypeScript into a browser-compatible language
- Browsers understand JavaScript, but not TypeScript
- Results may be different based on the compiler version
- Can be executed automatically by watching code changes

The compiler can compile a single file with the following:

```bash
tsc src/index.ts
```

In the example above, a file called `src/index.js` will be generated. This is the compiled version of the `src/index.ts` file.

### Setting up a `tsconfig` file

#### What is a `tsconfig` file?

- Using `tsconfig.json allows you to customise TypeScript to suit your project
- Defines which TypeScript files should be compiled and the resulting structure
- Which TypeScript features to use when compiling
- Varies from project to project

#### Example TypeScript Configuration

```json
{
  "extends": "@tsconfig/node12/tsconfig.json", // inherits from standard package
  "compilerOptions": {
    "module": "commonjs", // modifies the format of JavaScript output
    "noImplicitAny": true, // prevents developers from using "any" type
    "removeComments": true, // removes comments from generated code
    "sourceMap": true // creates a source map used for debugging
  },
  "include": ["src/**/*"] // defines which files should be compiled
}
```

`tsconfig` files take the form of a JSON object.
There are hundreds of options available - above are some of the most common.
[TSConfig Reference](https://www.typescriptlang.org/tsconfig)

### What Does a TypeScript Project Consist of?

- `package.json`: Tracks versions of TypeScript and ESLint (used to enforce coding style), contains shortcuts for building and watching TypeScript code
- `index.ts`: Contains code which serves the application, and references to other TypeScript files (may vary between projects)
- `tsconfig.json`: Configures how TypeScript should be compiled, and the source and output file locations
