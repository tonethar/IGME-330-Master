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
  - interfaces
  - enumerations
  - strong typing of variables
  - strong typing of function parameters and return types

- **"Starter" JS code we can add type annotations to:**
```js
// I. Explicitly typing variables
let a: number;
let b: string;
let c: boolean;
let d: Date;
let e: string[]; // an array of strings
//a = "Fred" // ERROR
e = ["Scooby"];
//e.push(99); // ERROR


// II. Implicitly (i.e. "automatically") typing variables
const meaningOfLife = 42; // will be implicitly typed as a `number`
const defaultName = "Mr. X"; // will be implicitly typed as a `string`
let temp = "utils.js temp value"; // will be implicitly typed as a `string`
//temp = 99 // ERROR
let date = new Date("01-01-2001");
//date = "01-01-2001"; // ERROR
date = new Date()
console.log("date",date) // click the Run button to see the code execute 


// III. Function parameters and return types can be typed too
// Go ahead and "fix" these 3 functions
const doubleIt = (val) =>  val * 2;

const doubleItToString = (val) =>  String(val * 2);

const formatGreeting = (greeting, name, forcefully) => {
  const recipient  = name ? name : defaultName;
  const str = `${greeting} ${recipient}`;
  return forcefully ? `${str.toUpperCase()}!` : str;
};
```

- **More TS code to try:**

```ts
// IV. Interfaces
// declare the "shape" of an object
interface Car {
  make:string, // required
  model:string, // required
  cylinders?:number, // optional
  equipment?: string[], // optional
  [key:string]: any // and ANY other property is allowed
}

let car1:Car = {make:"Ford", model:"Bronco", cylinders:8, coolness: 11};
//let car2:Car = {make:"Chevy"}; // ERROR

// V. Enumerations
enum Alignment{
  law,
  chaos,
  neutral
}

// OR
// enum Alignment{
//   law = "lawful",
//   chaos = "chaotic",
//   neutral = "neutralty"
// }

interface NPC{
  name: string,
  alignment:  Alignment
}

let arthur: NPC = {name: "Arthur", alignment: Alignment.law };
//let bob: NPC = {name: "Bob", alignment: "Nice" }; // ERROR

// VI. union type
type RgbColor = "red" | "green" | "blue"; 
let color1:RgbColor = "red";
//let color2:RgbColor = "yellow"; // ERROR
```

<hr>

### II-B. Discussion
- Disadvantages of TypeScript:
  - having to download and script the tooling
  - writing more code than you would have to with VanillaJS
- Advantages of TypeScript:
  - catch bugs early while you are writing the code, not later on during development or after the code is shipped
  - tooling enables lots of code hints in your IDE
  - TypeScript is a *superset* of JS, meaning that legal JS is also legal TS, meaning that it's easy to build on top of your existing JS knowledge
  - can write code that uses the latest version of JS, and because of transpilation, you don't need to worry (much) about browser support

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


    - #1 - generate a package.json file
      - `npm init -y`
    - #2 - install typescript (note: `i` is short for `install` and `-D` is the shortcut for `--save-dev`)
      - `npm i -D typescript`
    - #3 - install webpack & webpack-cli
      - `npm i -D webpack webpack-cli ts-loader`
    - #4 - install webpack-dev-server
      - `npm i -D webpack-dev-server`

<hr>

- In the **greeter-modules-ts/** folder, create **webpack.config.js**
- Docs at: https://webpack.js.org/configuration/

**webpack.config.js**
```js
const path = require('path');

module.exports = {
  entry: './src/main.ts',
  module: {
    rules: [
      {
        test: [/\.ts?$/,/\.js?$/],
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

<hr>

- In the **greeter-modules-ts/** folder, create **tsconfig.json**
- Docs at: https://www.typescriptlang.org/tsconfig

**tsconfig.json**
```json
{
  "compilerOptions": {
      "target": "ES5",
      "module": "ES6",
      "sourceMap": true
  },
  "include": ["src/**/*"]
}
```

<hr>

- In **package.json** make the `"scripts:"` key look like this:

```json
"scripts": {
  "build": "webpack --mode production --watch"
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

