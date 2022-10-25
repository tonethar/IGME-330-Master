# Intro to TypeScript

## I. What is TypeScript?

- *TypeScript is a free and open source programming language developed and maintained by Microsoft. It is a strict syntactical superset of JavaScript and adds optional static typing to the language. It is designed for the development of large applications and transpiles to JavaScript. As it is a superset of JavaScript, existing JavaScript programs are also valid TypeScript programs.*
  - https://en.wikipedia.org/wiki/TypeScript
- https://www.typescriptlang.org/
- https://basarat.gitbook.io/typescript/

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

