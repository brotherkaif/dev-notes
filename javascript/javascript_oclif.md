# JavaScript: Open CLI Framework (OCLIF)

## Resources
- [OCLIF Homepage](https://oclif.io/)

## Quickstart
```(bash)
$ npx oclif generate mynewcli
? npm package name (mynewcli): mynewcli
$ cd mynewcli
$ ./bin/dev hello world
hello world! (./src/commands/hello/world.ts)
```

This will generate the project structure, along with a few sample commands to get you started. It will even generate the test harness for each of the files.

## Basic Project Structure
The main command files are broken up into the following folder structure in the `src` directory:
```(bash)
src
├── commands
│   └── hello
│       ├── index.ts
│       └── world.ts
└── index.ts
```

Each of the files are executed depending on the command issued. In the table below, we will assume that the application entry command has been set to `mycli`:

| Command Issued      | File Executed             |
|-------------------- |-------------------------- |
| `mycli`             | `commands/index.ts`       |
| `mycli hello`       | `commands/hello/index.ts  |
| `mycli hello:world` | `commands/hello/world.ts` |

**Note:** Obviously, in runtime, the compiled `.js` files in the `dist` folder are executed instead... but you know what I mean.

## Testing
`oclif` will also generate a test harness for you in the `test` directory. The test system uses `mocha` along with some other assertion libraries that have been put together for `oclif`. `package.json` also gets generated with an `npm test` mapping.

The test folder structure is as follows:
```(bash)
test
├── commands
│   └── hello
│       ├── index.test.ts
│       └── world.test.ts
├── helpers
│   └── init.js
└── tsconfig.json
```

As can be seen above, there is a 1:1 mapping between the `test` folder structure and `src`, which should make maintenence a lot easier.
