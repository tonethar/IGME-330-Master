# Intro to TypeScript

## I. What is TypeScript?

- *TypeScript is a free and open source programming language developed and maintained by Microsoft. It is a strict syntactical superset of JavaScript and adds optional static typing to the language. It is designed for the development of large applications and transpiles to JavaScript. As it is a superset of JavaScript, existing JavaScript programs are also valid TypeScript programs.*
  - https://en.wikipedia.org/wiki/TypeScript
- https://www.typescriptlang.org/
- https://basarat.gitbook.io/typescript/

<hr>

## II. Try it out

### II-A. Let's see how TS works in a REPL
- https://www.typescriptlang.org/play
- Our TypeScript annotations will be transpiled into ES5 VanillaJS
- We'll look at:
  - *explicit* typing
  - *implicit* typing

- **"Starter" JS code we can add type annotations to:**
```js
const meaningOfLife = 42;
const defaultName = "Mr. X";
let temp = "utils.js temp value";

const doubleIt = (val) =>  val * 2;

const formatGreeting = (greeting, name, forcefully) => {
  const recipient  = name ? name : defaultName;
  const str = `${greeting} ${recipient}`;
  return forcefully ? `${str.toUpperCase()}!` : str;
};
```

- **TS code to try:**

```ts
const stuff:string[] = []; // typed array
stuff.push("red");
stuff.push(10);

// declare the "shape" of an object
interface Car {
  make:string,
  model:string,
  cylinders?:number,
  equipment?: string[]
}

let car1:Car = {make:"Ford", model:"Bronco", cylinders:8};
let car2:Car = {make:"Chevy"};

type RgbColor = "red" | "green" | "blue";  // union type
let color1:RgbColor = "red";
let color2:RgbColor = "yellow";
```

<hr>

### II-B. Discussion
- disadvantages of TypeScript:
  - tooling
  - writing more code than you would have to with VanillaJS
- advantages of TypeScript:
  - catch bugs while you are writing the code, not later on during development or after it is shipped
  - tooling enables lots of code hints in your IDE
  - TypeScript is a *superset* of JS, meaning that legal JS is also legal TS
  - Can write code that uses the latest version of JS, and because of transpilation, you don't need to worry about browser support

<hr>

## III. Use node & webpack to transpile a TypeScript app to JS

- Go ahead and grab the [**greeter-modules-ts.zip**](_files/greeter-modules-ts.zip) code - this is the ES6 module/TypeScript version of the Greeter demo
- Open it up in VSCode (but don't launch LiveServer) - note that the code in **main.ts** and **utils.ts** is written in TypeScript and thus won't run in a web browser until it is *transpiled*
- We'll need some node packages:
  - https://www.npmjs.com/package/typescript
  - https://www.npmjs.com/package/webpack
  - https://www.npmjs.com/package/webpack-cli
  - https://www.npmjs.com/package/webpack-dev-server
- In a console app (Terminal, GitBash etc) `cd` into the **greeter-modules-ts** folder
- Let's install these packages by typing some code (ONE line at a time):

```
// 1 - generate a package.json file
npm init -y
// 2 - install typescript
npm install --save-dev typescript
// 3 - install webpack & webpack-cli
npm install --save-dev webpack webpack-cli ts-loader
// 4 - install webpack-dev-server
npm install --save-dev webpack-dev-server
```

- In the **greeter-modules-ts/** folder, create **webpack.config.js**
- Docs at: https://www.typescriptlang.org/tsconfig

```js
const path = require('path');

module.exports = {
  entry: './src/main.ts',
  module: {
    rules: [
      {
        test: /\.ts?$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  devtool: 'source-map'
};
```

- In the **greeter-modules-ts/** folder, create **tsconfig.json**

```json
{
  "compilerOptions": {
      "target": "ES5",
      "module": "ES6",
      "sourceMap": true
  }
}
```

- In **package.json** make the `"scripts:"` key look like this:

```json
"scripts": {
  "build": "webpack --mode production --watch "
}
```

<hr>

## IV. Run the app!

- Type: `npm run build`
- Look at **dist/bundle.js** - the TypeScript has been transpiled to JS!
- Note the `<script>` tag in **greeter.html** has already been modified to point at **dist/bundle.js** 
- Double-click on **greeter.html** to test the app (you don't need a web server) - it should work normally
- Go ahead and make some changes in your **main.ts** or **utils.ts** file, and note that webpack is re-compiling the code for you
  - now test your changes in the web browser to sure that they "took"
- Also note that "source mapping" is turned on - you can see that in the Chrome debugger
- Type ctrl-c to quit node when you are done

