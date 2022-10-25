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

## III. Use node & webpack to transpile a TypeScript app to 

- Grab **greeter-modules-ts.zip** start files from myCourses
- Open up in VSCode (but don't launch LiveServer)
- In a console app (Terminal, GitBash etc) `cd` into the **greeter-modules-ts** folder
- Type some code:

```
npm init -y
npm install --save-dev typescript
npm install --save-dev webpack webpack-cli ts-loader
npm install --save-dev webpack-dev-server
```

- Create **webpack.config.js**

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

- Create **tsconfig.json**

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




