# About this Canvas Sprites Tutorial Series (IGME-330)
## I. Overview
Parts I-III of this series of tutorials/lecture notes will get you started creating animated canvas sprites for your *Project 1 : Audio Visualizer* and *Project 2: Game or Experience* assignments for IGME-330. We will also look at several techniques used to create JavaScript objects utilizing *protoypical inheritance* and `Object.create()`, as well as ES6 classes. 

Parts IV & V will look at ways of making our JS code loosely coupled and modular, and thus easier to write and maintain as applications become more complex and their size grows.

Part VI will look at how to *transpile* our JavaScript code from ES6 to ES5, which is more widely supported by older browsers.

## II. Prerequisite Knowledge
- It assumed that you understand the foundational JavaScript concepts covered here: [About this Web App Tutorial Series](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-0.md#section4)
- You also should be familiar with basic [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) operations such as:
   - obtaining a 2D drawing context
   - *drawing state* variables such as `fillStyle`, `lineStyle`, `globalAlpha`
    - creating paths, lines, curves, and arcs
    - `stroke()` and `fill()`
- and Canvas API concepts:
    - drawing state stack
    - `save()` and `restore()`
    - tranformations: `translate()`, `rotate()`, `scale()`

## III. How to get the most out of these tutorials
- Try out the code samples! Tweak and modify them! Most of the code samples are 100% complete. You just need to copy the code and paste it into a text editor. You can then make changes to the code and preview them in a web browser (we will be using Chrome)
- Be sure to answer all of the questions at the end of each section, and to do the review exercises.

## IV. The Tutorials
1. [Intro to Canvas Sprites](./canvas-sprites-1.md)
    - Canvas animation without objects
    - Canvas sprites via JS Object literals
    - Create multiple objects with a "factory function"
1. [`Object.create()` & Delegation](./canvas-sprites-2.md)
    - JavaScript does not have classes
    - Prototype-based inheritance and the "prototype chain"
    - Extending behavior - delegation
    - Overriding behavior - shadowing
    - OLOO - "Objects linked to other objects"
    - `Object.create()` & `Object.assign()`
    - `CircleSprite`, `SquareSprite`, `ImageSprite`
1. [Canvas & ES6 Classes](./canvas-sprites-3.md)
    - ES6 Classes are "syntactic sugar"
    - ES6 Inheritance
    - Side-by-side look at ES6 classes and `Object.create()`:
        - you get nearly the same thing back from the JS runtime!
1. [JavaScript & ES6 Modules](./canvas-sprites-4.md)
    - Why do we need modularized code?
    - A very cluttered *script scope*
    - `export` & `import`
    - ES6 modules example
    - *Module scope*
    - Converting "Bouncing Sprites" to use ES6 modules
1. [JavaScript & the ES5 *Revealing Module Pattern*](./canvas-sprites-5.md)
    - The Revealing Module Pattern
    - Attaching modules to a global object
    - Converting "Bouncing Sprites" to the ES5 module pattern
1. [Transpiling ES6 to ES5](./canvas-sprites-6.md)
    - What is *transpiling*?
    - Babel
    - Node.js, NPM & webpack
    - Transpiling "Bouncing Sprites" from ES6 to ES5
    
    
## V. Demos
- Canvas *Particles & Spritesheet* Demo:
    - [Zipped Files](_files/particles-spritesheet.zip)
    - Working version: http://igm.rit.edu/~acjvks/courses/2018-spring/330/code-examples/js-module-demos/particles-spritesheet/
    - Concepts: ES6 Modules, ES6 classes, inheritance, [configuration objects](https://code.tutsplus.com/tutorials/whats-a-configuration-object-and-why-bother-using-it--active-11580), `Object.assign()`, default exports, spritesheets, particle systems, playing sound, CTM rotations

## VI. Homework Assignments
See mycourses dropboxes for due dates.
- IGME-330 Project 1 - Audio Visualizer
- [Cage Clicker HW](./HW-cage-clicker-1.md)
- IGME-330 Project 2 - Game or Interactive Experience


