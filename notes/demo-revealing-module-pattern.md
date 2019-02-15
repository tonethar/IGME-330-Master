# Demo - ES5 Revealing Module Pattern

## I. Overview
- Here we will learn how to create multiple **modules** in our code by utilizing IIFEs, where the various units of JavaScript can run without interference from the other units
- In the **first part** of today's demo, we will take a previous demo where all of the JS code is contained in the HTML file and split the code between 4 JS files, which will improve the readability and organization of the code. There is a lot of re-factoring to do, so this part of the demo will take a while.
  - ***Issue:***: as far as the JavaScript runtime engine is concerned, all of this code is still intermingled in the global and "script" scopes - so variables in different files can still overwrite each other - we need to fix this!
- In the **second part** of today's demo, we will fix this issue by implementing the ***revealing module pattern***. 
  - This pattern uses multiple IIFEs to first hide away all the code in a file that we wish to be *private* and not visible to the outside, and then to only export those variables and functions that we wish to be *public*.
  - ***Issue:***: the code is dramatically better than what we had before, but there is still a problem -  two of the  modules contain hard-code *dependencies* on the 'app` global - so let's move on and fix that!
- In the **third part** of today's demo - we will eliminate these *dependencies* by passing them in as parameters, rather than hard-coding them, which will have the effect of completely *decoupling* our modules, which makes them more re-usable and easier to test and debug. This is a very simple technique, but it comes with fancy names like *inversion of control (IOC)* and *dependency injection (DI)*, which can be summarized as "instantiate and pass in any module dependencies".
  
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

1. 


## IV. Summary

- We have seen two powerful JS code patterns that will make your code more robust, and work on pretty much any shipping browser!



