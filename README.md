# P5js & Typescript Starter Template

## How to use

- clone repo as a Template

- if want to use local p5js
  - `mkdir web/p5js`
  - put the version of p5js you will be using in the folder
- else if using CDN or other source
  - update sketch.html to point to correct version of p5js
- else if using npm package... (TODO: explain)

- `npm install`
- `npm run tsc`
- `npm run http-server`

Note: if have trouble with clearing the cache on your browser try adding `?nocache=1` to the end of the url, e.g. `http://127.0.0.1:8080/?nocache=1`

## Steps to Create

See also 
- https://github.com/carlynorama/2023January-30DaysNatureOfCode
- https://github.com/Gaweph/p5-typescript-starter

### Setup Typescript

```zsh
## cd into project directory
which npm
brew update
npm i typescript --save-dev
npx tsc --init
## make changes to config file
touch index.html
mkdir src
mkdir build
touch src/index.ts
touch .gitignore
## Add the contents to the files
npx tsc

```

### Contents of index.js
```js
export function updateMessage() {
  const messageText = document.createTextNode(" and another thing...");
  let node = document.getElementById("message")?.appendChild(messageText)
}
```

### Contents of index.html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello JS</title>
    <script src="build/index.js"></script>
  </head>
  
  <body>
    <H1>hello!</H1>
    <p id="message">no message yet</p>
    <button onclick="updateMessage()">Click me</button>
  </body>
</html>
```

### Contents of .gitignore

```
.DS_Store
.vscode/
node_modules/

**/*.js
**/*.js.map
!build/index.js
```

### Add scripts

Change `package.json` to have the following block

```json
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "tsc": "tsc",
        "tsc:w": "tsc --watch",
        "http-server": "npx http-server -o"
    },
```

These scripts facilitate testing, running typescript, launching a server, etc. 

```
npm run http-server
```

### Add p5js

Uses the NPM module for the types see examples:

https://www.npmjs.com/package/p5?activeTab=versions

(note there is also https://www.npmjs.com/package/p5-typescript?activeTab=readme)

```zsh
npm install -D p5 @types/p5
```

This will install the types into the dev dependencies. One can then add an explicit dependency to a copy of p5.js on a server for the sketch to use. 

To make it easy to copy/paste between the web editor and the local project, add a `global.d.ts` to the src folder or other location and add to included in the `tsconfig.json` 

```
// This file will add both p5 instanced and global intellisence
// https://github.com/Gaweph/p5-typescript-starter/blob/master/global.d.ts 
import * as p5Global from 'p5/global' 
import module = require('p5');
export = module;
export as namespace p5;
```

My src folder now looks like 

```
src
  |_ global
    |_ global.d.ts
  |_ scaffold
    |_ index.ts
  |_ scaffold
    |_ index.ts
  |_ sketch
    |_ sketch.ts
```

Where `sketch.ts` contains:

```js
function setup() {  
    createCanvas(400, 400);
    console.log("hello");
    
    stroke(0);
    noFill();
    colorMode(HSB);
  }
  
function draw() {
    background(0, 0, 80);
    ellipse(50, 50, 50, 50);
    noLoop();
}
```

`index.html` now looks like:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello JS</title>
    <!-- as served in web editor 2025 Mar 11 -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.1/p5.js"></script>
    <script src="build/scaffold/index.js"></script>
    <script src="build/sketch/sketch.js"></script>
  </head>
  
  <body>
    <H1>hello!</H1>
    <p id="message">no message yet</p>
    <button onclick="updateMessage()">Click me</button>
  </body>
</html>

```

Since I want to have archival version of these sketches, i went to the github repository and downloaded the release files. 

https://github.com/processing/p5.js/releases/tag/v1.11.3

and updated the html header to

```html
<script src="p5js/p5.min.js"></script>
```

### Clean up HTML / Move output

I wanted to clean up the HTML into and index and an embedded iframe, which means the I wanted a folder that would represent the the website.

I changed the web files, moved the output in `tsconfig.json` and the webserver call in `package.json` as well. 

This is the current state of the project. 




