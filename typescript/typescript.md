---
title: TypeScript
description: 
published: true
date: 2022-05-03T17:38:36.329Z
tags: 
editor: markdown
dateCreated: 2022-05-03T17:37:27.433Z
---

# TypeScript

## Why TypeScript?

- Less error code
- Cleaner code

## What is TypeScript?

- Is a superset of JavaScript. A language building up on JavaScript.
- Add new features and advantages to JavaScript
- Browser can't execute TypeScript. It's also a compiler which run over your code to compile TypeScript to JavaScript.
- It is possible to write easier code that compiles to a more complex JavaScript snippets.
- Permit to identify errors in code before it runs with extra error checking.
- TypeScript add:
  - Types
  - Non-JavaScript features like Interfaces, Generics.
  - Rich configuration options.
  - Next-gen JS features compiled down for old browsers.
  - Meta-Programming features like Decorators.
  - Tools that helps even in non TypeScript projects.
- TypeScript helps only during development, before the code get's compiled. It doesn't run in execution time.

## Some difference between JavaScript and TypeScript

- JavaScript uses dynamic types resolved at runtime, TypeScript uses static types setted during development.

## Installing TypeScript

```bash
npm install -g typescript
```

## Compiling ts files

It is possible to compile the ts files and get the error messages from the console. It creates a .js file with the result of the compilation.

```bash
tsc my-ts-script.ts
```

## Creating Node environment with package.json

It creates the package.json configuration file.

```bash
npm init
```

After that it is possible to install all the necessary packages described in the file with the command:

```bash
npm install
```

Also it can install a new npm package adding the name.

## Install node packages

```bash
npm install your-npm-package
```

Another variant install development dependencies.

```bash
npm install --save-dev your-dev-package
```

## Executing the app with lite-server

Install lite-server and add a script in the package.json file to start with the server. It runs an index.html file in the root of the project.

```TypeScripton
"start": "lite-server"
```

The html file needs to include the js compiled file.

```html
<script src="app.js" defer></script>
```

Init the app with:

```bash
npm start
```

## Watch Node

Compiling ts files with the watch option, the file is compile automatically when the ts file is saved.

```bash
tsc app.ts --watch
tsc app.ts -w
```

## Initiating a TypeScript project

With the next command the `tsconfig.json` file **is created** to configure the ts project.

```bash
tsc --init
```

After that is possible to compile all js files in the whole project with the tsc command and only whatch the files.

```bash
tsc -w
```

## TypeScript configurations

Some configurations about the tsconfig.json file.

- target

Set the JavaScript language version for emitted JavaScript and include compatible library declarations.

e.g. "ES5", "ES6", "ES2015", "ES2016", ...

- lib

Can add the common libraries to the project, instead add all the js libraries.

```TypeScripton
"lib": [
      "DOM",
      "es6",
      "DOM.Iterable",
      "ScriptHost"
    ]
```

- exclude/include

```TypeScripton
"include": [
    "src/app.ts",
    "src/analytics.ts"
  ],
  "exclude": [
    "node_modules", // would be the default
  ]
```

- sourceMap

Generate the corresponding .map file to link directly the compiled .js with the .ts original file. Usefull to debugging.

- output/input directories

```TypeScripton
"outDir": "./dist",
"rootDir": "./src",
```

- remove comments

Don't create the comments in the output js files.

- no emit (noEmit)

To don't emit the output js files, usefull tu check the syntax without compile.

- no emit on error (noEmitOnError)

Prevent to emit compiled ts files with errors.

- strict

Control many strict options to be more precise with the code.

## Organising folders

- src

Has the job to holding all the input, so all the source TypeScript files.

- dist

Has the job to holding all the output, so all the JavaScript files.


## Another concepts learned

- lite-server

Node application that creates a server running an index.html in the base of the project. It updates automatically the changes in the code when it's saved.

Then the start script can be created to execute the server.

```TypeScripton
"start": "lite-server"