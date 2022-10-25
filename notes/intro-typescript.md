# Intro to TypeScript

## I. What is TypeScript?

- *TypeScript is a free and open source programming language developed and maintained by Microsoft. It is a strict syntactical superset of JavaScript and adds optional static typing to the language. It is designed for the development of large applications and transpiles to JavaScript. As it is a superset of JavaScript, existing JavaScript programs are also valid TypeScript programs.*
  - https://en.wikipedia.org/wiki/TypeScript
- https://www.typescriptlang.org/
- https://basarat.gitbook.io/typescript/

<hr>

## II. Try it out here
- https://www.typescriptlang.org/play

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

export { doubleIt, formatGreeting };
```

<hr>

## III. Use node & webpack to transpile a TypeScript app to JS

- Go ahead and grab the [**greeter-modules-ts.zip**](_files/greeter-modules-ts.zip) code - this is the ES6 module/TypeScript version of the Greeter demo
- Open it up in VSCode (but don't launch LiveServer) - note that the code is written in TypeScript and thus won't run in a web browser until it is *transpiled*
- In a console app (Terminal, GitBash etc) `cd` into the **greeter-modules-ts** folder
- Let's install some node packages by typing some code (ONE line at a time):

```
npm init -y
npm install --save-dev typescript
npm install --save-dev webpack webpack-cli ts-loader
npm install --save-dev webpack-dev-server
```

- In the **greeter-modules-ts** folder, create **webpack.config.js**

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
  devServer: {
    static: path.join(__dirname, "dist"),
    compress: true,
    port: 4000,
  },
  devtool: 'source-map'
};
```

- In the **greeter-modules-ts** folder, create **tsconfig.json**

```json
{
  "compilerOptions": {
      "noImplicitAny": true,
      "target": "ES5",
      "module": "ES2015",
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
- Double-click on **greeter.html** to test the app (you don't need a web server) -it should work normally
- Go ahead and make some changes in your **main.ts** or **utils.ts** file, and note that webpack is re-compiling the code for you
  - now test your changes in the web browser to sure that they "took"
- Type ctrl-c to quite node when you are done

