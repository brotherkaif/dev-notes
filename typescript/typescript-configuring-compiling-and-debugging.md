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

## Configuring the TypeScript Compiler
Effectively configuring the compiler allows you to design a build process that suits your app, and not the other way around.

- **Output Format:** Specify the format of generated code (ES3, ES6, ESNext, etc.)
- **Supported Features:** Restrict certain TypeScript features (e.g. `any` type)
- **Style Guidelines:** Codify and enforce style (line breaks, tab size, etc.) among large teams

### Watching for Changes to TypeScript Files
Architecting your application so that builds occur automatically lets your developers focus on completing their tasks.

#### "Watching" File Changes
- Compiler executes automatically when code is edited
- Other tooling (tests, etc.) can also be triggered
- Can ignore specific files (e.g. `node_modules`)

#### Possible Changes and Tasks

**Possible Changes**
- Manual Changes to code
- Results of code being merged
- Accidental change (key press, file corruption)
- Automated change caused by editor, test suite, or code quality tool

**Possible Tasks After Change**
- Rebuild code base
- Refresh web browser
- Run tests
- Run code quality tools (e.g. ESLint)
- None (ignore changes under certain conditions)

### Reviewing Configuration Options

[TypeScript Handbook: Configuring Watch](https://www.typescriptlang.org/docs/handbook/configuring-watch.html)

```JSON
{
  // Some typical compiler options
  "compilerOptions": {
    "target": "es2020",
    "moduleResolution": "node"
    // ...
  },
  // Options for file/directory watching
  "watchOptions": {
	// Relates to HOW files are watched
	// Depending on the OS, polling can be inconsistent or slow
	// You may want to use a different option if that's the case
    "watchFile": "useFsEvents",
    "watchDirectory": "useFsEvents",

	// Some OS may have a limit to how many files may be watched
	// This option provides workarounds
    "fallbackPolling": "dynamicPriority",

    // Used if your OS does not support recursive watching
    // This can be really slow!
    "synchronousWatchDirectory": true,

    // Finally, two additional settings for reducing the amount of possible
    // files to track  work from these directories
    "excludeDirectories": ["**/node_modules", "_build"],
    "excludeFiles": ["build/fileWhichChangesOften.ts"]
  }
}
```

### Extending Base Configurations
#### What Are Base Configurations?
- Collection of compiler options and values
- Available locally or as a package maintained by TypeScript
	- [TypeScript Base Configurations Repository](https://github.com/tsconfig/bases)
- Any option can be overwritten

#### Common `tsconfig` Bases
- [recommended](https://github.com/tsconfig/bases/blob/main/bases/recommended.json): Enforces strict style and targets ES2015
- [create react app](https://github.com/tsconfig/bases/blob/main/bases/create-react-app.json): Settings needs for `jsx` interoperability
- [node 16](https://github.com/tsconfig/bases/blob/main/bases/node16.json): Outputs modern server JavaScript `require`, async, etc. 

#### Example
A base configuration ([node 16](https://github.com/tsconfig/bases/blob/main/bases/node16.json) in this example) can be installed using the following:
```bash
$ npm install --save-dev @tsconfig/node16
```

If we wanted to extend this configuration, we can do the following in our `tsconfig.json`:
```JSON
{
    // the statement below loads in the base configuration
    "extends": "@tsconfig/node16/tsconfig.json",

    // everything below will get added/merged into the base configuration
    "compilerOptions":{
        "removeComments": true,
        "lib": ["ES2018", "DOM"]
    },
    "include": ["src/**/*"],
    "watchOptions": {
        "excludeDirectories": ["**/node_modules", "app"]
    }
}
```

### Multi-File and Single-File Compilation
**Multi-File Compilation**
- Creates one JavaScript file for every target TypeScript file
- Each file must be loaded for the application to work in a browser
- Files must be concatenated or use `require` to work in Node.js
- Possible to update just one generated file in production
- Standard compilation option for TypeScript

**Single-File Compilation**
- Combines all TypeScript files into one single JavaScript file
- Only a single file must be loaded for the application to work in a browser
- Single file will work when invoked as a Node script
- Updated production code must be pushed in its entirety
- Additional tooling (Webpack, Babel) needed