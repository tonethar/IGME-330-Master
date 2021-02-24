# Transpiling ES6 to ES5

## Contents
<!--- Local Navigation --->
I. [What is *transpiling*?](#section1)

II. [Babel](#section2)

III. [Node.js, NPM & webpack](#section3)

IV. [Transpiling an ES6 project down to ES5](#section4)

V. [Discussion](#section5)

VI. [Try This](#section6)

VII. [Reference](#section7)

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
 
## III. <a id="section3">Node.js, NPM & webpack

- https://nodejs.org/en/
- https://www.npmjs.com
- https://www.npmjs.com/package/webpack

- **Node.js** is a command-line JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
- **npm** is the package (i.e. "library") manager for JavaScript
- **webpack** is a module bundler. Its main purpose is to bundle JavaScript files for usage in a browser, yet it is also capable of transforming, bundling, or packaging just about any resource or asset.

<hr>
 
## IV. <a id="section4">Transpiling an ES6 project down to ES5
	
- Go get your ["ES6 Module Pattern"](ES-6-module-pattern-2195.md#section5) code - this is one where you converted "Sprity" to ES6 modules
- Test it in a browser to be sure that it works (it has to run off of a Web Server or Code's Live Server because of the ES6 Modules)
- We are going to transpile all of that ES6 code to ES5 so that it will run on all recent browsers, even ones that don't know about ES6
- **Important:** make sure there are not any spaces anywhere in the path (folder names) to your files - that ticks off webpack sometimes

<hr>
 
 **0) Install Node.js and the *Node Package Manager* (npm) - *if you need to***
 
 - Head to https://nodejs.org/en/download/ and grab an installer - instructions are here:
 
 https://docs.npmjs.com/getting-started/installing-node
 
 - When **Node.js** is installed, it also installs **npm** (Node Package Manager)
 - Head to the command prompt to verify that `node` and `npm` are installed by typing:
 
 ```js
 node -v
 npm -v
 ```
 
 - You can run the updater on `npm` itself by typing:
 
 ```js
 npm install npm@latest -g
 ```
 
 - You can also update `node` - https://hosting.review/tutorial/how-to-update-node/
 
<hr>
 
 **1) Change directory to your project folder**
 
- Head to the command prompt, and `cd` *into* the **sprites-plus-modular** folder.

<hr>
  
 **2) Create a node project with npm**
 
 - Type: 
 
 ```js
 npm init -y
 ```
 
 - This will create your **package.json** file with default *metadata* about your project, which are in an object literal, which should look something like this:
 
 ```js
 {
  "name": "sprites-plus-modular",
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
- You can read about **package.json** here: https://docs.nodejitsu.com/articles/getting-started/npm/what-is-the-file-package-json/

- Note that the default `name` of the project is the name of the folder that **package.json** is contained in. You can change this if you wish

<hr>
 
**3) Next we need to install the `webpack` module to this folder**

```js
npm install webpack --save
```

**and**

```js
npm install webpack-cli -D --save
```


- Which will download all of the modules you will need - check out the `node_modules` folder in your project directory
- the added `--save` flags will also add `"dependencies"` and `"devDependencies"` keys to *package.json*


```js
"dependencies": {
    "webpack": "^4.41.2"
  },
  "devDependencies": {
    "webpack-cli": "^3.3.9"
  }
```
  

**PS - You will now see a file named *package-lock.json* - you won't be editing it - read about it here: https://docs.npmjs.com/files/package-lock.json**

<hr>
 
**4) Create a new file named *webpack.config.js***

- It needs to look like this:

**webpack.config.js**

```js
module.exports = {
    entry: ['./src/loader.js','./src/main.js','./src/sprites.js','./src/utils.js','./src/canvas-utils.js'],
    output: {
        filename: './bundle.js'
    }
};
```

- You can see above that `module.exports` is an object literal:
    - `entry` contains an array of all of the JS files we wish to compile
    - `output` is the name of the single JavaScript file we will compile to
    - you can read more about the options for the **webpack.config.js** file here: https://webpack.js.org/concepts/#entry

<hr>
 
**5) Modify *package.json***

- Open up *package.json* and make the "scripts" key look like this:

```js
"scripts": {        
    "start": "npm run webpack",
    "webpack": "webpack -d --watch"
},
```

- This custom `start` command will run webpack in debug mode, which will be more verboise in flagging issues. This command also sets webpack to watch for any changes in the JavaScript files; when we make a change, webpack will re-build the **bundle.js** file automatically for us.

<hr>
 
**6) Run npm!**

- Type: 

```js
npm start
```
- this executes `webpack -d --watch` for you

You should now see that *dist/bundle.js* has been created. If you open *bundle.js*, you will see that your 5 JavaScript files have been compiled to ES5 and the results bundled into it.

<hr>
 
**7) Edit your HTML file**

In **index.html** - make the "bottom" of the &lt;body> tag look like this:

```html
  <!-- <script src="src/loader.js" type="module"></script> -->
  <script src="dist/bundle.js"></script>
</body>
</html>
```

- we are now pointing the &lt;script> tag at the compiled JS file at *dist/bundle.js* rather than at *loader.js*
- note that this is a regular ES5 JavaScript file now, so we don't need `type="module"` any longer

<hr>
 
**8) Final Test**
- Reload the page, everything should work as before!
- Note that `webpack` is stil running and watching our files, and if we make any changes, it will automatically recompile our files for us

<hr>

**9) Distribution**

When you post this to the web:

- you need the HTML file, *dist/bundle.js*, and your *images* folder
- you don't need your `js` folder - because all that ES6 has been compiled down to ES5 and put into *bundle.js*
- you don't need any of the other of the other configuration files or *package.json* or the *node_modules* folder
- PS - this transpiled code will also run off of the desktop - it no longer needs a web server to function

<hr>
 
## V. <a id="section5">Discussion

- Go ahead and make some changes in *main.js*, like increasing the number of sprites. If webpack is still running, it will automatically compile a new *bundle.js* for you.

- Because webpack recursively builds a dependency graph that includes every module your application needs, then packages all of those modules into *bundle.js*, your *webpack.config.js* file may only need to list the first JS file. In our example, we only need to list *loader.js* as the entry file, and webpack will then be able to determine the other required JavaScript files. 

New **webpack.config.js**
```js
module.exports = {
    entry: './src/loader.js',
    output: {
        filename: './bundle.js'
    }
};
```

- And finally, let's say that later on you have deleted the **node_modules** folder, and committed your project to GitHub. Later on when you are working on the project again, is there an easy way to download the modules you need? ***YES!*** Because these project dependencies are now listed in **package.json**, all you need to do is to change directory to the project folder and type in:

```js
npm install
```

- Which will download and install all modules listed as dependencies in *package.json* 

- You can then type `npm start` to run the project.

<hr>
 
## VI. <a id="section6">Try This
	
- We are not collecting this, but you should practice this technique on another ES6 project or HW assignment

<hr>
 
## VII. <a id="section7">Reference

- [`npm install`](https://docs.npmjs.com/cli/install)
- [`npm init`](https://docs.npmjs.com/cli/init)
- [`npm start`](https://docs.npmjs.com/cli/start)


