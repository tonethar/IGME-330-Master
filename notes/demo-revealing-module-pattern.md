# Demo - ES5 Revealing Module Pattern

## I. Overview
- Here we will learn how to create multiple **modules** in our code by utilizing IIFEs, where the various units of JavaScript can run without interference from the other units
- In the first part of today's demo, we will take a previous demo where all of the JS code is contained in the HTML file and split the code between 3 JS files, which will improve the readability and organization of the code.
  - However, as far as the JavaScript runtime is concerned, all of this code is still intermingled in the global and "script" scopes.
- In the second part of today's demo, we will fix this issue by implementing the ***revealing module pattern***. 
  - This pattern uses multiple IIFEs to first hide away all the code in a file that we wish to be *private* and not visible to the outside, and then to only export those variables and functions that we wish to be *public*.
  
 ## II. Start Files
- The start file for this presentation is the completed version of the the "Demo - Sprite Literals and Canvas Image Data", we did recently, and it is here --> [filter-plus-bitmap-manip-example.zip](./_files/filter-plus-bitmap-manip-example.zip)

## III. Demo

### Part One - move the code to separate files:

Follow along if you can - or try it out later!

1. Create a folder named `src`
