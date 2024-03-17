Integrating TypeScript with Node.js, especially in a monorepo project, can be a challenging and time-consuming process. Lift aims to streamline the process and eliminate the need to build TypeScript in both development and production environments. Lift is not limited to just this functionality and seeks to enhance Node.js in other aspects, such as integrating it with a more efficient HTTP server. That's why it's named Lift instead of Node.ts.

### Features

- [x] Running and testing TypeScript (both CommonJS and ES module systems)
- [x] Integration with the built-in Node.js test runner
- [x] Integration with ESLint and Prettier for linting and formatting
- [x] Monorepo setup
  - Uses the standard [NPM workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces/) for linking packages in monorepo
  - Uses the standard Node.js's [subpath patterns](https://nodejs.org/docs/latest-v20.x/api/packages.html#subpath-patterns) for path aliasing
- [ ] Supports TypeScript debugging

## Hello World!

Save and run the [hello world](./scripts/hello_world.sh) script to see Lift in action:

### Usage:

```bash
npm i -D @bitair/lift
lift init
```

#### Subcommands

|        | Description                                | Example                                                                                                                           | Status          |
| ------ | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| help   | Lists the subcommands                      | lift help                                                                                                                         | Implemented     |
| init   | Generates a monorepo                       | lift init                                                                                                                         | Implemented     |
| add    | Adds a new app or lib to the monorepo      | lift add app server<br> lift add lib common<br> lift add app @my-org/my-project.server<br> lift add lib @my-org/my-project.common | Implemented     |
| link   | Links a lib to an app                      | lift link server common<br> lift link my-project.server my-project.common                                                         | Implemented     |
| format | Formats the code                           | lift format \*\*/\*.ts                                                                                                            | Implemented     |
| lint   | Lints the code                             | lift lint \*\*/\*.ts                                                                                                              | Implemented     |
| test   | Runs TypeScript test suits                 | lift test test/\*.ts                                                                                                              | Implemented     |
| run    | Runs a TypeScript program                  | lift run index.ts                                                                                                                 | Implemented     |
| debug  | Generates a debug configuration for VSCode |                                                                                                                                   | Not Implemented |

#### Notes

- When importing a TypeScript module, it is important to explicitly prefix the path with either '.ts', '.mts', or '.cts':

  ```ts
  import { func } from './sample_module.ts'
  ```

- The `lint` subcommand uses the `eslint` command with the `--config` argument pointing to the `.eslintrc.cjs` file at the root of the repo. To set a specific configuration file, reset the `--config` argument. Other available options of the eslint command can also be included.

- The `lint` subcommand also utilizes the `tsc` command with a predefined set of configurations. To specify a custom set of configurations, set the `--tsconfig` argument to point to a `tsconfig.json` file. No options from the `tsc` command will be processed and should not be passed.

- The `format` subcommand uses the `prettier` command with the `--write` argument. Other options of the prettier command can also be included.

- The `test` subcommand uses the `node` command with the `--test` argument. Additional options of the node command can also be specified.
