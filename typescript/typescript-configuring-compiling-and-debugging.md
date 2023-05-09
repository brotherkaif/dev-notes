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

#### Example: Setting-Up Watching in TypeScript
Add a `watchOptions` property within `tsconfig.json`:
```JSON
{
	// ...
	"watchOptions": {
		// You will probably want to exclude some locations from the watchlist
		"excludeDirectories": ["**/node_modules", "app"]
		// "**/node_modules": ignore `node_modules` recursively
		// "app": ignore the build directory
	}
	// ...
}
```

You can add some scripts to `package.json` to make it easier to run `tsc` in watch mode:
```JSON
{
	// ...
	"scripts": {
		// ...
		"watch": "tsc -w"
	}
	// ...
}
```

In a new terminal session, you can now run the following:
```bash
$ npm run watch
```

Now, whenever a new change is made to the `*.ts` files being watched, they will be compiled to `*.js` files.

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

#### Example: Extending the `node16` Base Configuration
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
	- Not ideal (as it introduces more dependencies), but, it is what it is

#### Single-File Compilation for Majority of Tasks
Compiling a TypeScript application to a single file generally makes it easier to deploy ad both a web and a server-side application.

- Greater support for isomorphic applications (applications that have an element on both the frontend and backend
	- The same file we make will work in both those environments 
- Fewer HTTP requests, simpler deployment to web applications
	- Results in applications running faster
- Greater consistency across browser / Node versions

#### Example: Using Webpack to Compile TypeScript Applications into a Single File

Take the following structure:
```bash
project
├── node_modules
│   └── ...
├── package-lock.json
├── package.json
├── src
│   ├── app
│   │   └── Main.ts
│   └── index.ts
└── tsconfig.json
```

`Main.ts`:
```TypeScript
export class Main {
	render() : any {
		console.log("Rendering the application.");
	}
}
```

`index.ts`:
```TypeScript
// const Main = require("./app/Main")
import { Main } from "./app/Main";

new Main().render();
```

`tsconfig.json`:
```JSON
{
    "exclude": ["node_modules"]
}
```

After running a build (using a script like `npm run build`), we get the following:
```bash
src
├── app
│   ├── Main.js
│   └── Main.ts
├── index.js
└── index.ts
```

As can be seen, the compiler has created a `*.js` file for each corresponding `*.ts` file. **What we'd prefer in this example is to have all of the `*.ts` files compiled down into a single `*.js` file.**  This can be achieved using [webpack](https://webpack.js.org/) + [babel](https://babeljs.io/).

Installing what we need:
```bash
$ npm install --save-dev webpack webpack-cli webpack-dev-server ts-loader
```

Create a `webpack.config.js` file:
```JavaScript
const path = require('path');

module.exports = {
	// specify the file we're interested in as our main file
	entry: './src/index.ts',

	// ensures that stuff like `console.log()` are not removed
	mode: 'development',

	module: {
		// rules lets us specify what to do with each type of file 
		rules: [
			// here, we've specified for `*.ts` or `*.tsx` files
			// to use the `ts-loader` package
			// and to ignore the `node_modules` directory
			{
				test: /\.tsx?$/, // tsx only necessary for react projects
				use: 'ts-loader',
				exclude: /node_modules/,
			},
		],
	},
	resolve: {
		// tell webpack to be interested in `*.ts` or `*.js` files
		extensions: ['.ts', '.js'],
	},
	output: {
		// tell webpack that the final file should be called `bundle.js`...
		filename: 'bundle.js',
		// ... and put it in a directory called `bin`
		path: path.resolve(__dirname, 'bin')
	},
	// set up a dev server (which is like an additional watch)
	// on port 7777
	// serving the 'public' directory
	devServer: {
		static: {
			directory: path.join(__dirname, 'public'),
		},
		compress: true,
		port: 7777,
	},
};
```

You can add a `webpack` script to `package.json`:
```JSON
{
	// ...
	"scripts": {
		// ...
		"webpack": "webpack"
	}
	// ...
}
```

Run the `webpack` script:
```bash
$ npm run webpack
```

This creates a *massive* file called `bundle.js` in the `bin` directory:
```bash
bin
└── bundle.js
```

Let's create a quick `index.html` in the `public` directory:
```bash
public
└── index.html
```

`index.html`:
```HTML
<div>
	Hello World!
</div>
<script src="bundle.js"></script>
```

Remember, both `bin` and `public` are configured to be served on the dev server. Let's add a script for that in `package.json`:
```JSON
{
	// ...
	"scripts": {
		// ...
		"dev": "webpack serve"
	}
	// ...
}
```

Run the `dev` script:
```bash
$ npm run dev
```

The webpage should be visible on `http://localhost:7777`

### Summary
- The TypeScript compiler is configured by using `tsconfig.json`
- `tsc` is used to compile multi-file builds, while `webpack` or other tools are used to create a single file application or other tools are used to create a single file application
- Build tools can watch files for changes
	- Automatic build after each change saves time and concentration
- Base configurations provide industry-standard combinations of options that can be overridden as needed
