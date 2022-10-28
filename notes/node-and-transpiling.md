# Bundling & Transpiling JS

## Contents
<!--- Local Navigation --->
I. [What is *transpiling*?](#section1)

II. [Babel](#section2)

III. [Node.js, `npm` & webpack](#section3)

IV. [Transpiling an ES6 project down to ES5](#section4)

V. [Discussion](#section5)

VI. [Try This](#section6)

VII. [Reference](#section7)

VIII. [We lied to you!](#section8)

IX. [Install `babel-loader`](#section9)

X. [Test `babel-loader`](#section10)

XI. [Bundling and transpiling Project 1](#section11)

<hr>

## I. <a id="section1">What is *transpiling*?
- Transpilers are tools that read source code written in one programming language, and transform it to the equivalent code in another language.
- Transpiling has been a part of JavaScript development for quite some time. You may have heard of [TypeScript](https://www.typescriptlang.org) or [CoffeeScript](http://coffeescript.org). Both of these JavaScript libraries add strong typing and other features to JavaScript by utilizing a transpiler to transform the type annotated JavaScript code to legal ES5 JavaScript that the web browser can understand.
  
 ### Transpiler references 
- https://scotch.io/tutorials/javascript-transpilers-what-they-are-why-we-need-them
- https://en.wikipedia.org/wiki/Source-to-source_compiler
- https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js

<hr>
 
## II. <a id="section2">Babel
 
Babel is a an ES6 (and future versions of ES) to ES5 transpiler.

- https://babeljs.io

Try pasting the following ES6 class code into the Babel REPL at http://babeljs.io/repl - and see what kind of ES5 code you get back.

- You'll need to select the "Enabled" and "FORCE ALL TRANSFORMS" checkboxes under ENV PRESET section to see the full ES5 compatible code. 
	
<hr>
	
**Example #1:**
```js
const doubleIt = num => num * 2;
const firstName = "Arthur";
const greeting = `Hello ${firstName}`;
```
	
**Transpiles to the following, because ES5 doesn't have `const`, arrow functions or template strings**	
```js
var doubleIt = function doubleIt(num) {
  return num * 2;
};
var firstName = "Arthur";
var greeting = "Hello ".concat(firstName);
```

<hr>

**Example #2 - check out what the code below transpiles to because ES5 doesn't have the `class` keyword**	
```js
class Vehicle{
    constructor(year,numWheels){
        this.year = year;
        this.numWheels = numWheels;
    }
	
    move(){
        console.log("Moving the vehicle now");
    }
  
    toString(){
  	return "Year: " + this.year + ", numWheels: " + this.numWheels;
    }
}

let skateboard = new Vehicle(2012,4);

console.log(`This skateboard has ${skateboard.numWheels} wheels.`);
```

<hr>
 
## III. <a id="section3">Node.js, npm & webpack

- https://nodejs.org/en/
- https://www.npmjs.com
- https://www.npmjs.com/package/webpack

- **Node.js** is a command-line JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
- **npm** is the package (i.e. "library") manager for JavaScript
- **webpack** is a module bundler. Its main purpose is to bundle JavaScript files for usage in a browser, yet it is also capable of transforming, bundling, or packaging just about any resource or asset.

<hr>
 
## IV. <a id="section4">Transpiling an ES6 project down to ES5 with Webpack
	
- Go ahead and grab the [greeter-modules.zip](_files/greeter-modules.zip) code - this is the ES6 module version of the Greeter demo
  - You can clean up the code if you want to - get rid of the console logs, unnecessary variables/imports/exports, etc
- Test it in a browser to be sure that it works (it has to run off of a Web Server or Code's Live Server because of the ES6 Modules)
- We are going to transpile all of that ES6 code to ES5 so that it will run on all recent browsers, even ones that don't know about ES6
- **Important:** make sure there are not any spaces anywhere in the path (folder names) to your files - that ticks off webpack sometimes

<hr>
 
 **0) Install Node.js and the *Node Package Manager* (`npm`) - *if you need to***
 
 - Head to https://nodejs.org/en/download/ and grab an installer
   - instructions are here: https://docs.npmjs.com/getting-started/installing-node
 - When **Node.js** is installed, it also installs `npm` (Node Package Manager)
 - On a Mac, open the **Terminal** application. On Windows, head to the command prompt (or **GitBash** if it's installed) to verify that `node` and `npm` (and `npx`, although we don't need it here) are installed by typing:
 
 ```js
 node -v
 npm -v
 npx -v
 ```
 
 - If needed, you can run the updater on `npm` itself by typing:
 
 ```js
 npm install npm@latest -g
 ```
 
 - You can also update `node` if need be - there is a program called `nvm` (*node version manager*) - or you can also just download a new installer from the web site - https://nodejs.org/en/download/
 
<hr>
 
 **1) Change directory to your project folder**
 
- In your command prompt application (Terminal, GitBash, etc), `cd` *into* the **greeter-modules** folder

<hr>
  
 **2) Create a node project with `npm`**
 
 - Type: 
 
 ```js
 npm init -y
 ```
 
 - This will create your **package.json** file with default *metadata* about your project, which are in an object literal, which should look something like this:
 
 ```js
 {
  "name": "greeter-modules",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
 ```
- You can read about **package.json** here: 
  - https://docs.npmjs.com/creating-a-package-json-file
  - https://heynode.com/tutorial/what-packagejson

- Note that the default `name` of the project is the name of the folder that **package.json** is contained in. You can change this if you wish

<hr>
 
**3) Next we need to install the `webpack` and `webpack-cli` modules to this folder**

```js
npm install webpack --save-dev
```

**and**

```js
npm install webpack-cli --save-dev
```

- Which will download all of the modules you will need - check out the `node_modules` folder in your project directory
- the added `--save-dev` flags will also add `"devDependencies"` keys to *package.json* - which makes it easy for you to re-download these libraries later:
  - note: your version #'s will be different, so DO NOT modify what `npm` generated for you

```js
"devDependencies": {
  "webpack": "^5.74.0",
  "webpack-cli": "^4.10.0"
}
```
  

**PS - You will now see a file named *package-lock.json* - you won't be editing it - read about it here: https://docs.npmjs.com/files/package-lock.json**

<hr>
 
**4) Create a new file named *webpack.config.js***

- It needs to look like this:

**webpack.config.js**

```js
module.exports = {
  mode: 'development',
  entry: ['./src/main.js'],
  output: {
    filename: './bundle.js'
  }
};
```

- You can see above that `module.exports` is an object literal:
  - `mode` can be "development" or "production"
  - `entry` contains an array of all of the JS files we wish to compile - in this case if we just specify **main.js** webpack will go ahead and transpile all of the other files that **main.js** depends on 
  - `output` is the name of the single JavaScript file we will compile to
  - you can read more about the options for the **webpack.config.js** file here: 
    - https://webpack.js.org/concepts/#entry
    - https://webpack.js.org/configuration/mode/

<hr>
 
**5) Modify *package.json***

- Open up **package.json** and make the "scripts" key look like this:

```js
"scripts": {        
  "start": "npm run webpack",
  "webpack": "webpack --watch"
},
```

- This custom `start` command will run webpack, and also tells webpack to watch for any changes in the JS files; and when we save a change, webpack will re-build the **bundle.js** file automatically for us.

<hr>
 
**6) Run npm!**

- Type: 

```js
npm start
```
- this executes `webpack --watch` for you

You should now see that **dist/bundle.js** has been created. If you open **bundle.js**, you will see that your 2 JavaScript files have been "bundled" into it.

<hr>
 
**7) Edit your HTML file**

In **greeter.html** - make the &lt;script> tag look like this:

```html
<!-- <script type="module" src="src/main.js"></script> -->
<script src="dist/bundle.js"></script>
```

- we are now pointing the `<script>` tag at the compiled JS file at **dist/bundle.js** rather than at **loader.js**
- note that this is a regular ES5 JavaScript file now, so we don't need `type="module"` any longer

<hr>
 
**8) Final Test**
- Reload the Greeter HTML page, everything should work as before!
  - But it doesn't! You will likely see an error in the browser console - `main.js:16 Uncaught TypeError: Cannot read properties of null (reading 'checked')`
  - This happens because the **bundle.js** code is loading/running BEFORE the page loads! (Remember that problem from ES5?)
  - The easiest fix is to move the `<script src="dist/bundle.js"></script>` tag to the bottom of the page
  - Test it again. Now Greeter should work.
- Note that `webpack` is still running and watching our files, and if we make any changes, it will automatically recompile our files for us
- Handy tip! When you want to quit the npm/webpack app running in the console, type **control-c** (or **ctrl-c** depending on your keyboard)

<hr>

**9) Distribution**

When you post this to the web:

- you need the HTML file, **dist/bundle.js** (and your **images** folder, **styles** folder etc if applicable)
- you don't need your `src` folder - because all that ES6 has been compiled down to ES5 and put into *bundle.js*
- you don't need any of the other of the other configuration files or **package.json** or the **node_modules** folder
- PS - this transpiled code will also run off of the desktop - it no longer needs a web server to function

<hr>
 
## V. <a id="section5">Discussion
- The **node_modules** folder is huge! Once you are done with your transpiling activities, go ahead and delete it.
- And finally, let's say that you have deleted the **node_modules** folder, and committed Greeter to GitHub
- Later on when you are working on Greeter again, and what to be sure that the code changes are being transpiled, is there an easy way to download the modules you need? 
- ***YES!*** Because these project dependencies are now listed in **package.json**, all you need to do is to change directory to the project folder and type in:

```js
npm install
```

- Which will download and install all modules listed as dependencies in **package.json**
- You can then type `npm start` to run the project.

<hr>
 
## VI. <a id="section6">Try This
	
- You should practice this technique on another ES6 project or HW assignment

<hr>
 
## VII. <a id="section7">Reference

- [`npm install`](https://docs.npmjs.com/cli/install)
- [`npm init`](https://docs.npmjs.com/cli/init)
- [`npm start`](https://docs.npmjs.com/cli/start)

<hr>
	
## VIII. <a id="section8"> We lied to you!

- Yes, your Greeter code has been *bundled* (from 2 files to 1)
- But it has not yet been *transpiled* from ES5 to ES6 
- In **webpack.config.js**, change the `mode` from `development` to `production`
- Quit node in the console (if it's running) with control-c
- Type `npm start` to load these **webpack.config.js** changes 
- Open up **bundle.js** - you should see that all of the code has been jammed onto one line, but will still have `const`, arrow functions, template strings and other ES6 features in the code

**bundle.js**
```js
(()=>{"use strict";const e="Mr. X",o=(o,t,l)=>{const c=`${o} ${t||e}`;return l?`${c.toUpperCase()}!`:c},t=document.querySelector("#input-firstname"),l=document.querySelector("#output"),c=document.querySelector("#cb-forcefully"),n=document.querySelector("#btn-hello"),r=document.querySelector("#btn-goodbye");let u=c.checked;c.onchange=e=>u=e.target.checked,n.onclick=()=>l.innerHTML=o("Hello",t.value.trim(),u),r.onclick=()=>l.innerHTML=o("Goodbye",t.value.trim(),u),console.log("formatGreeting('Hey There') = ",o("Hey there")),console.log("doubleIt(10) = ",20),console.log("defaultName = ",e),console.log("meaningOfLife = ",42),console.log("temp = ","main.js temp value"),console.log("utils.temp = ","utils.js temp value")})();	
```
- This is because that `webpack` just does *bundling*, but we need `babel` to do the *transpiling*
- Let's fix this!

<hr>
	
## IX. <a id="section9"> Install `babel-loader`
- Reference: https://www.npmjs.com/package/babel-loader
- To install **`babel-loader`**:
  - type: `npm install --save-dev babel-loader @babel/core @babel/preset-env`
  - then check **package.json** to see the `dev-dependencies:` that were added
  - and see that **node_modules** just got bigger with more babel-related files
- Add the following to the bottom of **webpack.config.js**
  - except for the `...`

```js
...,
module: {
  rules: [
    {
      test: /\.m?js$/,
      exclude: /node_modules/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env'],
        },
      },
    },
  ],
}	
```

<hr>
	
## X. <a id="section10"> Test `babel-loader`

- Quit node in the console (if it's running) with control-c
- Type `npm start` to load the **webpack.config.js** changes 
- Make sure that Greeter still works
- Open up **bundle.js** - you should see that all of the code has been jammed onto one line, AND that it has been *transpiled* to ES5 JS, meaning there are no longer arrow functions, template strings, `const` and other ES6 features in the code
	
**bundle.js**
	
```js
(()=>{"use strict";var e="Mr. X",o=function(o,t,n){var c=t||e,r="".concat(o," ").concat(c);return n?"".concat(r.toUpperCase(),"!"):r},t=document.querySelector("#input-firstname"),n=document.querySelector("#output"),c=document.querySelector("#cb-forcefully"),r=document.querySelector("#btn-hello"),l=document.querySelector("#btn-goodbye"),u=c.checked;c.onchange=function(e){return u=e.target.checked},r.onclick=function(){return n.innerHTML=o("Hello",t.value.trim(),u)},l.onclick=function(){return n.innerHTML=o("Goodbye",t.value.trim(),u)},console.log("formatGreeting('Hey There') = ",o("Hey there")),console.log("doubleIt(10) = ",20),console.log("defaultName = ",e),console.log("meaningOfLife = ",42),console.log("temp = ","main.js temp value"),console.log("utils.temp = ","utils.js temp value")})();
```

<hr>
	
## XI. <a id="section11"> Bundling and transpiling Project 1
- Bundling and transpiling Project 1 (*Web App of Awesomeness*) is a little bit trickier because it's a *multi-page app*
- Which means 3 entry points - **app.js**, **community.js** and **favorites.js**
- And 3 bundled output files - **app-bundle.js**, **community-bundle.js** and **favorites-bundle.js**
- There's also the matter of the firebase library imports - there's no way to bring those in without using an `import` statement, which means we're not in 100% ES5 land anymore, Toto
- The following config file worked for me - you might need to change some of the file names depending on how you named things:
	
	
**webpack.config.js**
```js
module.exports = {
  mode: 'production',
  entry: {
    app: './src/app.js',
    community: './src/community.js',
    favorites: './src/favorites.js'
  },
  output: {
    filename: '[name]-bundle.js',
    path: __dirname + '/dist',
  },
  // https://webpack.js.org/configuration/externals/#externalstypemodule
  experiments: {
    outputModule: true, /* Fixes the firebase import issue */
  },
  module: {
    rules: [
      {
        test: /\.m?js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
    ],
  }
};	
```
