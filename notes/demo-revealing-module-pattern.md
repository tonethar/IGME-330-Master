# Demo - ES5 Revealing Module Pattern

## I. Overview
- Here we will learn how to create multiple **modules** in our code by utilizing IIFEs, where the various units of JavaScript can run without interference from the other units
- In the **FIRST part** of today's demo, we will take a previous demo where all of the JS code is contained in the HTML file and split the code between 4 JS files, which will improve the readability and organization of the code. There is a lot of re-factoring to do, so this part of the demo will take a while.
  - ***Issue***: as far as the JavaScript runtime engine is concerned, all of this code is still intermingled in the global and "script" scopes - so variables in different files can still overwrite each other - we need to fix this!
- In the **SECOND part** of today's demo, we will fix this issue by implementing the ***revealing module pattern***. 
  - This pattern uses multiple IIFEs to first hide away all the code in a file that we wish to be *private* and not visible to the outside, and then to only export those variables and functions that we wish to be *public*.
  - ***Issue***: the code is dramatically better than what we had before, but there is still a problem -  two of the  modules contain hard-coded *dependencies* on the 'app` global - so let's move on and fix that!
- In the **THIRD part** of today's demo - we will eliminate these *dependencies* by passing them in as parameters, rather than hard-coding them, which will have the effect of completely *decoupling* our modules, which makes them more re-usable and easier to test and debug. This is a very simple technique, but it comes with fancy names like *inversion of control (IOC)* and [*dependency injection (DI)*](https://medium.com/@fleeboy/dependency-injection-in-javascript-9db9ea6e4288), which can be summarized as "instantiate and pass in a module's dependencies"
  
 ## II. Start Files
- The start file for this presentation is the completed version of the the "Demo - Sprite Literals and Canvas Image Data", we did recently, and it is here --> [filter-plus-bitmap-manip-example.zip](./_files/filter-plus-bitmap-manip-example.zip)

## III. Demo Walkthrough

### Part One - move the code to separate files:

Follow along if you can - or try it out later!

1. Create a folder named `src`
2. In the `src` folder, create a file named `utilities.js`, and cut/paste your `UTILITY FUNCTIONS` into it
3. Reload the HTML page - ERROR!
4. Create your &lt;script> tag --> `<script src="src/utilities.js"></script>`
5. Reload the HTML page - ERROR! - **`ReferenceError: ctx is not defined`**
6. `getLinearGradient()` is looking for a globally scoped `ctx` variable - let's fix that! How? We add a `ctx` parameter to the beginning of the `getLinearGradient()` declaration in **utilities.js**, and then pass `ctx` in when we *call* `getLinearGradient()` in the HTML file  
7. Now move all of the `FACTORY FUNCTIONS` to a new file named `sprites.js` and save it into the `src` folder
8. Go ahead and create a new &lt;script> tag to link to `sprites.js`
9. Reload the page - ERROR! - **`ReferenceError: canvasWidth is not defined`** 
10. Go ahead and fix the `createSprites()` function
11. Move the rest of the code (minus the Iffy) into a file named `main.js` and create a &lt;script> for it
12. Delete the empty &lt;script> tag that remains in the HTML file
13. Reload the page - ERROR! - **`TypeError: document.querySelector(...) is null`**
14. Create a new JS file named `loader.js` and put this in it:

```js
window.onload = _ =>{
	init();
}
```
15. Create a &lt;script> tag for `loader.js`
16. Delete the `init()` call from `main.js`
17. Reload the page - multiple ERRORs! Why?
18. Fix the issues in `main.js` by initializing certain variables in the `init()` function
19. Reload Page - everything should work. So we have great code, right?
20. Not really! Check the debugger and you'll see that even though all of the code is in separate files, all the functions and variables are still stuck in either global or script scope!

### Part Two - create *modules* with their own scope:

1. At the top of `utilities.js` - add the following `var app = app || {};` - we will explain this in class - it's also the only time in this course that we MUST use `var`
2. Now create the utilities *module* - which is an IIFE - like this at the beginning of the code - `app.utilities = (function(){ ...` - and this at the end - `})();`
3. Now all of our utilities code is hidden away in an Iffy - obviously this will break everything - **`ReferenceError: getLinearGradient is not defined`**
4. Take a look at `app.utilities` in the debugger it's `undefined`
5. So how do we make this utilities code visible to the outside? Just return a "public interface" like this:

```js
// our "public interface"
return{
	getRandomUnitVector: getRandomUnitVector,
	getRandom:getRandom,
	getRandomColor: getRandomColor,
	getLinearGradient: getLinearGradient
};
// remind us to show you the shorthand way to initialize an object!
```
6. Now all the utilities functions can get called through `app.utilities`! Fix the errors and make it so!
7. Add this line to the top of all of the JS files - `var app = app || {};`
8. Now we will make `sprites.js` a module in a similar way to how we did `app.utilities` - make it so!
9. Reload the page. Fix the error!
10. Now make `main.js` a module - and you only need to "export" the `init()` function - everything else is "private"
11. Call `app.main.init()` from `loader.js` and you are good to go!
12. Put a breakpoint on the `app.main.init()` line in loader - and check out the `app` variable, its modules, and the "public" properties of those modules (i.e. the ones we returned)

### Part Three - get rid of the remaining dependencies:

The code we wrote in Part Two above works well, but as mentioned in the intro, two of the modules contain hard-coded *dependencies* on the 'app` global. Some people might stop refactoring at this point and say "good enough" - but that's not how we roll! To fix this properly, we are actually going to re-structure the app one more time so that we can pass arguments into the modules. This also necessitates getting rid of the Iffys. So we are going to tear this code apart one last time, but it will be worth it!

1. First, we need to look at our modules one at a time to look for the actual dependencies they have on global variables:
  - **utilities.js** does not depend on any global variables or functions. As a matter of fact, all of the functions in this file are highly re-usable ["pure functions"](https://en.wikipedia.org/wiki/Pure_function), which do not produce any side effects. 
  - **sprites.js** has two dependencies on the `app` global object:
    - when it calls `app.utilities.getRandomColor()` AND 
    - when it calls `app.utilities.getRandomUnitVector()`
  - **main.js** has two dependencies on the `app` global object:
    - when it calls `app.utilities.getLinearGradient()` AND
    - when it calls `app.sprites.createSprites()`
2. To really fix this and make it "right", to have truly independent and reusable modules, we are going to 
3. First, we will head to **utilities.js** - we are going to make it so it's not 


Let's head to **loader.js** where we will address these dependencies by dependency injection - in this case - passing in the dependency rather than hard-coding it.
3. Make **loader.js** look like this:

```js
var app = app || {};
window.onload = _ =>{
  // D.I.
  app.sprites.utilities = app.utilities;
	
  // Start the app
  app.main.init();
}
```

4. Above we have created a new *property* on the "sprites" module named `utilities`, and assigned a value. 
5. In **sprites.js**, we need to modify the 2 lines of code flagged above so that they call `this.utilities` instead of `app.utilities`. Reload the page, it should work as before
6. So what we did is have the **loader.js** file "inject" the dependency and attach it to a property of the sprites module, rather than rely on the `app` global.
  - Our implementation is simple, but it works well, runs on pretty much any browser ever shipped, and follows the spirit of DI. Our implementation also avoids the use of a separate module loader library --> https://www.jvandemo.com/a-10-minute-primer-to-javascript-modules-module-formats-module-loaders-and-module-bundlers/




## IV. Summary

- We have seen two powerful JS code patterns that will make your code more robust, and work on pretty much any shipping browser!



