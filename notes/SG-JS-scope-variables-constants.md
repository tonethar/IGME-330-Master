# Study Guide: Scope for variables and functions

- See review questions below!
- Be sure to study for the exam by reviewing the resources that we suggested --> [midterm-exam-review.md](./midterm-exam-review.md)

<hr>

I. [Declaring variables with `var`, `let` & `const`](#variable-scope) - 15 questions

II. [Immutabilty](#immutabilty) - 6 questions 

III. [Answer Sheet](#answer-sheet)

IV. [Some of the Answers](#completed-answer-sheet)

<hr><hr>
## Overview

- JavaScript's scope (where a variable is visible) rules can be a little weird, so we're going to spend some time running though the various rules 
- For simplification of the discussion below, we are going to assume that our JS code is always running in [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode), and not worry about the many edge cases when JS is running in "sloppy mode"

## I. JavaScript Data Types

- *primitive* types


## II. What is variable *scope*

- https://stackoverflow.com/questions/500431/what-is-the-scope-of-variables-in-javascript?answertab=votes#tab-top

## I. Variable & Function Scope


### I-A. Declaring variables with `var`

- "The scope of a variable declared with `var` is its current execution context, which is either the enclosing function or, for variables declared outside any function, global. If you re-declare a JavaScript variable, it will not lose its value." - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var
- PS: When a function is declared with the `function` keyword, it follows the same scope rules
- "Because `var` variable declarations (and declarations in general) are processed before any code is executed, declaring a variable *anywhere* in the code is equivalent to declaring it at the top. This also means that a variable can appear to be used before it's declared. This behavior is called "hoisting", as it appears that the variable declaration is moved to the top of the function or global code."

### I-B. Declaring variables with `let` & `const`

- `let` allows you to declare variables that are limited to a scope of a block statement, or expression on which it is used, unlike the `var` keyword, which defines a variable globally, or locally to an entire function regardless of block scope. The other difference between `var` and `let` is that the latter is initialized to a value only when a parser evaluates it..." - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let
- P.S. `const` has the same rules of scope as `let`
- P.P.S. If `let` is used to declare a variable *outside* of a function, method, or class, it ends up in what is called *script scope*, which is a "global-like" scope where it will be visible in other JavaScript files
- "Redeclaring the same variable (with `let`) within the same function or block scope raises a SyntaxError"



<hr>

<a id="variable-scope"/>

### I-D. Questions on Variable Scope

- For questions #1 - #9, what will be logged out? 
- If there is an error, write "ERROR" next to the line of code that produces it
- After you have answered all of the questions, test yourself in the debugger to see if you were right
- Assume that all of following code is running in [*strict mode*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

1. 

```js
<script>
  function init(){
    var myNum = 0;
    let myNum2 = 0;
  }
   init();
   console.log(myNum);
   console.log(myNum2);
</script>
```

<hr>

2. 

```js
<script>
  init();
  
  function init(){
    if(true){
      var myNum = 0;
    }
    console.log(myNum);
  }
</script>
```

<hr>

3.

```js
<script>
  init();
  
  function init(){
    if(true){
      let myNum = 0;
    }
    console.log(myNum);
  }
</script>
```

<hr>

4.

```js
<script>
  init();
  
  var myNum = 0;

  function init(){
    console.log(myNum);
  }
</script>
```

<hr>

5. 

```js
<script>
  init();
  let myNum = 0;

  function init(){
    console.log(myNum);
  }
</script>
```

<hr>

6. 

```js
<script>
  function init(){
    if(true){
      for(var i=0;i<5;i++){
      //
      }
    }
   console.log(i);
  }
  
  init();
  
</script>
```

<hr>

7. 

```js
<script>
  function init(){
    if(true){
      for(let i=0;i<5;i++){
      //
      }
    }
   console.log(i);
  }
  
  init();
  
</script>
```

<hr>

8. 

```js
<script>
init();

function init(){
  console.log("Hi there!");
}
</script>
```

<hr>

9. 

```js
<script>
init();

let init = () => {
  console.log("Hi there!");
}
</script>
```

<hr>

10. What is the *scope* of the `init` function below?

```js
<script>
let init = () => {
  console.log("Hi there!");
}
debugger; // to help you test it a browser debugger yourself
</script>
```

A) block

B) function/local

C) global

D) script

E) module

<hr>


11. What is the *scope* of the `init` function below?

```js
<script>
  function init(){
    console.log("Hi there!");
  }
  debugger;
</script>
```

A) block

B) function/local

C) global

D) script

E) module

<hr>

12. What is the *scope* of the `pi` function below?

```js
<script>
  init();
  function init(){
    console.log("pi is approximately " + pi());
		
    function pi(){
      return 3.1415;
    }
    debugger;
  }
</script>
```

A) block

B) function/local

C) global

D) script

E) module

<hr>

13. What is the *scope* of the `pi` function below?

```js
<script>
  init();
  function init(){
    const pi = () => {
      return 3.1415;
    }
    debugger;
  }
</script>
```

A) block

B) function/local

C) global

D) script

E) module

<hr>

14. What is the *scope* of `myNum`, `myNum2` & `init` below? (*note that the script is of `type="module"`*)

```js
<script type="module">
  var myNum;
  let myNum2;
  function init(){
    myNum = 0;
    myNum2 = 0;
  }
  init();
</script>
```

15. What is the *scope* of `myNum`, `myNum2`, `myNum3` & `myNum4` below? (*note that the script is of `type="module"`*)

```js
<script type="module">
  var myNum = 10;
  let myNum2 = 20;
  window["myNum3"] = 30;
  window.myNum4 = 40;
  debugger;
</script>
```

<hr><hr>

<a id="immutabilty"/>

## II. Immutability

- "The `const` declaration creates a read-only reference to a value. It does not mean the value it holds is immutable, just that the variable identifier cannot be reassigned. For instance, in the case where the content is an object, this means the object's contents (e.g., its properties) can be altered." - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const

- After you have answered all of the questions, test yourself in the debugger to see if you were right
- Assume that all of the following code is running in [*strict mode*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

<hr>

1. What will be logged when this code runs?

```js
const y = 1;
y++;
console.log(y);
```

A) This will produce a runtime error

B) 1

C) 2

D) undefined

<hr>

2. What will be logged when this code runs?

```js
const x = {};
x.species = "Orc";
console.log(x.species);
```

A) This will produce a runtime error

B) "Orc"

C) undefined

<hr>

3. What will be logged when this code runs?

```js
const x = {};
x = {"species":"Orc"};
x.species = "Goblin";
console.log(x.species);
```

A) This will produce a runtime error

B) "Orc"

C) "Goblin"

D) undefined

<hr>

- Read about what `Object.seal()` and `Object.freeze()` do there:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze

<hr>

4. What will be logged when this code runs?

```js
const x = Object.seal({species: "Orc"});
x.species = "Goblin";
console.log(x.species);
```

A) This will produce a runtime error

B) "Orc"

C) "Goblin"

D) undefined

<hr>

5. What will be logged when this code runs?

```js
const x = Object.seal({species: "Orc"});
x.hitpoints = 10;
console.log(x.species);
```

A) This will produce a runtime error

B) "Orc"

C) "Goblin"

D) undefined

<hr>

6. What will be logged when this code runs?

```js
const x = Object.freeze({species: "Orc"});
x.species = "Goblin";
console.log(x.species);
```

A) This will produce a runtime error

B) "Orc"

C) "Goblin"

D) undefined




<hr><hr>

<a id="interview-question"/>

## IV. Interview-Style Question

- Be sure you practice the interview question at the end of [sample-midterm-exam.md](./sample-midterm-exam.md)

<hr><hr>

<a id="answer-sheet"/>

## V. Answer Sheet

- Test yourself!  Answer the questions without using your neighbor or the Internet
- Then check your answers by trying the code out in a browser

```text
**I. Variable Scope**

1) 
2) 
3)
4)
5)
6)
7)
8)
9)
10)
11)
12)
13)
14)
15)

**II. Immutability**

1)
2)
3)
4)
5)
6)


```

<hr><hr>


<a id="completed-answer-sheet"/>

## VI. Some of the answers

```text
**I. Variable Scope**
```

1) ERROR - because both `myNum1` and `myNum2` have been declared inside of `init()`, and are thus *scoped* to that function

2) `0` - because `var` variables are *scoped* to the entire function in which they are declared

3) ERROR - because `let` variables are *scoped* to the *block* in which they are declared

4) `undefined` - because the `var` *declaration* of `myNum` (but NOT the *initialization* of a value) is *hoisted* to the top of the &lt;script> tag (which is the enclosing *scope* in this instance). The `init()` function is then called, which logs out the current value of `myNum`, which is `undefined`

5) ERROR - because a `let` variable is initialized to a value only when a parser evaluates it

6) `5` - because `var` variables are *scoped* to the entire function in which they are declared, thus `i` is visible outside of the `for` block

7) ERROR - `let` variables are scoped to the enclosing block, so `i` here is only visible within the `for` block

8) `Hi there!` - because function *declarations* (where the `function` keyword is used) are *hoisted* to the beginning of the scope, and can thus be used before they appear in code

9) ERROR - because function *expressions* (where we use `var`, `let`, or `const`) are NOT *hoisted* to the beginning of the scope, and thus cannot be used before they are declared

10) Try it in the browser's debugger

11) Try it in the browser's debugger

12) Try it in the browser's debugger

13) We are calling it "block" scope. The debugger says "local", which means `pi` is scoped to the entire function, which is true in this instance. But because `pi` uses a `let` declaration, it's actually *block-scoped* (which just happens to also be the entire function in this instance). We will make sure that any exam questions will be phrased in such a way to not have this ambiguity

14) Try it in the browser's debugger

15) Try it in the browser's debugger
