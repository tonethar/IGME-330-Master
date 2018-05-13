# 6 - Transpiling ES6 to ES5

## Overview



## Contents
<!--- Local Navigation --->
I. [What is *transpiling*?](#section1)

II. [Babel](#section2)

III. [Node.js, NPM & webpack](#section3)

IV. [Transpiling an ES6 project down to ES5](#section4)

V. [Discussion](#section5)

<hr>

## I. <a id="section1">What is *transpiling*?
- Transpilers are tools that read source code written in one programming language, and transform it to the equivalent code in another language.
- Transpiling has been a part of JavaScript development for quite some time. You may have heard of [TypeScript](https://www.typescriptlang.org) or [CoffeeScript](http://coffeescript.org). Both of these JavaScript libabries add strong typing and other features to JavaScript by utilizing a transpiler to transform the type annotated JavaScript code to legal ES5 JavaScript that the web browser can understand.
  
 ### Transpiler references 
- https://scotch.io/tutorials/javascript-transpilers-what-they-are-why-we-need-them
- https://en.wikipedia.org/wiki/Source-to-source_compiler
- https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js

## II. <a id="section2">Babel
 
Babel is a an ES6 (and future versions of ES) to ES5 transpiler.

- https://babeljs.io

Try pasting the following ES6 class code into the Babel REPL at http://babeljs.io/repl - and see what kind of ES5 code you get back.

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


## III. <a id="section3">Node.js, NPM & webpack

- https://nodejs.org/en/
- https://www.npmjs.com
- https://www.npmjs.com/package/webpack

- **Node.js** is a command-line JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
- **npm** is the package manager for javascript
- **webpack** is a module bundler. Its main purpose is to bundle JavaScript files for usage in a browser, yet it is also capable of transforming, bundling, or packaging just about any resource or asset.

## IV. <a id="section4">Transpiling an ES6 project down to ES5
	
- Go get your *canvas-sprites-4-HW.html* code - this is the one that uses ES6 classes and ES6 modules
- We are going to transpile all of that ES6 code to ES5 so that it will run on all recent browsers, even ones that don't know about ES6
  
 **1) Install Node.js and the Node Package Manager (npm)**
 
- You could do this with nvm (the Node Version Manager) like this:
 
 ```js
 curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
 ```
 
 - and then: 
 
 ```js
 nvm install node
 nvm -v
 npm install npm@latest -g
 ```
 
 **Or**
 
 - you can head to https://nodejs.org/en/download/ and grab an installer - instructions are here:
 
 https://docs.npmjs.com/getting-started/installing-node
 
 - once Node.js is installed, head to the command prompt to install npm:
 
 ```js
 npm -v
 npm install npm@latest -g
 ```
 
 **Note: Mac OS users will often have to have `sudo` at the beginning of the command whenever they are installing applications or packages.**
 
 **2) Change directory to your project folder**
 
Head to the command prompt, and `cd` to your project folder.
 
 **3) Verify that the node and npm versions are up-to-date**
 
 ```js
 node -v
 npm -v
 ```
 
 **4) Create a node project with npm**
 
 - Type: 
 
 ```js
 npm init -y
 ```
 
 - This will create your **package.json** file with default settings, which are in an object literal, which should look something like this:
 
 ```js
 {
  "name": "part-IV-homework",
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

Note that the default `name` of the project is the name of the folder that *package.json* is contained in. You can change this if you wish.

**5) Next we need to install webpack**

```js
npm install webpack --save
```

**and**

```js
npm install webpack-cli -D --save
```


- Which will download all of the modules you will need - check out the `node_modules` folder in your project directory
- the added `--save` flags will also add `"dependencies"` keys to *package.json*


```js
"dependencies": {
    "webpack": "^4.0.1"
  },
  "devDependencies": {
    "webpack-cli": "^2.0.9"
  }
```
  
**PS - Mac users will probably need `sudo` again**

**6) Create a new file named *webpack.config.js***

- It needs to look like this:

**webpack.config.js**

```js
module.exports = {
    entry: ['./js/init.js','./js/classes.js','./js/main.js','./js/utilities.js'],
    output: {
        filename: './bundle.js'
    }
};
```

- You can see above that `module.exports` is an object literal:
    - `entry` contains an array of all of the JS files we wish to compile
    - `output` is the name of the single JavaScript file we will compile to
    - you can read more about the options for the *webpack.config.js* file here: https://webpack.js.org/concepts/#entry
    
**7) Modify *package.json***

- Open up *package.json* and make the "scripts" key look like this:

```js
"scripts": {        
    "start": "npm run webpack",
    "webpack": "webpack -d --watch"
},
```

- This custom `start` command will run webpack in debug mode, which will be more verboise in flagging issues. This command also sets webpack to watch for any changes in the JavaScript files; when we make a change, webpack will re-builf the bundle.js file automatically for us.

**8) Run npm!**

- Type: 

```js
npm start
```
- this executes `webpack -d --watch` for you

You should now see that *dist/bundle.js* has been created. If you open *bundle.js*, you will see that your 4 JavaScript files have been compiled to ES5 and the results bundled into it.

**9) Edit your HTML file**

Make your HTML file look like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Canvas & ES6 Classes - HW</title>
</head>
<body>
	<canvas width="600" height="400"></canvas>
<!-- 	<script src="js/init.js" type="module"></script> -->
	<script src="dist/bundle.js"></script>
</body>
</html>
```

- we are now pointing the &lt;script> tag at the compiled JS file at *dist/bundle.js* rather than at *init.js*
- note that this is a regular ES5 JavaScript file now, so we don't need `type="module"` any longer


**10) Final Test**
- Reload the page, everything should work as before!
- Note that webpack is stil running and watching our files, and if we make any changes, it will automatically recompile our files for us

**11) Distribution**

When you post this to the web:

- you need the HTML file, *dist/bundle.js*, and your *images* folder
- you don't need your `js` folder - because all that ES6 has been compiled down to ES5 and put into *bundle.js*
- you don't need any of the other of the other configuration files or *package.json*
- PS - this transpiled code will also run off of the desktop - it no longer needs a web server to function


## V. <a id="section5">Discussion

- Go ahead and make some changes in *main.js*, like increasing the number of circles. If webpack is still running, it will automatically compile a new *bundle.js* for you.

- because webpack recursively builds a dependency graph that includes every module your application needs, then packages all of those modules into *bundle.js*, your *webpack.config.js* file may only need to list the first JS file. In our example, we only need to list *init.js* as the entry file, and webpack will then be able to determine the other required JavaScript files. 

New **webpack.config.js**
```js
module.exports = {
    entry: './js/init.js',
    output: {
        filename: './bundle.js'
    }
};
```


<hr><hr>

**[Previous Chapter <- JavaScript & the ES5 *Revealing Module Pattern* (chapter 5)](canvas-sprites-5.md)**
