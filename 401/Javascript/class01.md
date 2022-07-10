# Node Ecosystem

- Node.js is a JS runtime built on Chrome's V8 JS engine
- V8 is responsible for compiling JS directly to native machine code that your computer executes.
- V8 is enhanced with various features, such as a file system API, an HTTP library and a number of OS related utility methods.
- Node.js is a program that we can use to execute JS on our computers (outside of the browser)

## Node Binaries vs Version Manager

- use a version manager when installing node.
- This allows you to install multiple version of Node and switch between them at will.
- negates potential permissions issues when using Node with npm and lets you set a Node version on a per-project basis.
- node -v or node --version to check if it's installed on your system

## NPM - The JS package manager

- Node comes bundled with a package manager called npm.
- npm is also the world's largest software registry and there are over 1 million packages of JS code to download.

## Install packages Globally

- `npm install -g jshint`

## Install packages Locally

- create a new test folder and cd into directory
- run `npm init -y`
- this will create and auto-populate a `package.json` file in the same folder.
- next use npm to install the lodash package and save it as a project depend. `npm install lodash --save`
- create a file name `test.js` and add:

```
const _ = require('lodash')
const arr = [0, 1, false, 2, '', 3];
console.log(_.compact(arr));
```

- run `node test.js` and you should see [1, 2, 3] in the terminal

## Working with the package.json file

- inside our `test` folder, you'll notice a folder entitled `node_modules`, this is where npm has saved lodash and any libraries that lodash depends on.
- `node_modules` folder shouldn't be check in to version control, and can simple be re-created by running `npm install` from within the projects root.
- inside your `package.json` file, you'll see lodash listed under the depends field.

## What is Node.js Used for?

- bundling your JS files and depends into static assets, running tests, or automate code linting and style checking.
- allows us to run JS on the Server
- plays a critical role in the technology stack of many high-profile companies.

## Node execution Model

- Node is single-threaded and event-driven, which means that everything happens in Node is in reaction to an event.
- uses libuv library under the hood to implement this asynchronous(non-blocking) behavior.
- execution model causes the server very little overhead, thus capable of handling a large number of simultaneous connections.

## Downsides?

- since Node runs on a single thread, it does pose some limitations.
- blocking I/O calls should be avoided, CPU-intensive operations should be handed off to a worker thread, and errors should always be handled correctly for fear of crashing the entire process.

## What Apps is Node suited to?

- apps which require real-time interaction or collaboration (chat sties, CodeShare)
- building APIs where you're handling lots of requests that are I/O driven (those needing to perform operations on a database)
- sites involving data streaming
- can process files that are still being uploaded.

## Advantages of Node

- speed, scalability, used in both a browser and web server
- speaks JSON
- one syntax from the browser, server and database.
- ubiquitous: transitioning to Node development is easier than to other server-side languages.

## Other uses of Node

- can be used as a scripting language to automate repetitive or error prone tasks on your PC.
- can be used to write your own command line tool.
- can be used to build cross-platform desktop apps and even to create your own robots

### Source

[sitepoint](https://www.sitepoint.com/an-introduction-to-node-js/)