# ES6 Module Pattern (2225)

## Contents
<!--- Local Navigation --->
I. [Why do we need modularized code?](#section1)

II. [ES6 Module Syntax](#section2)

III. [Try it out!](#section3)

IV. [Reference](#section4)

V. [Review Questions](#section5)


<hr>

<a id="section1">

## I. Why do we need modularized code?
Applications that are written in a **modular** fashion are [loosely coupled](https://en.wikipedia.org/wiki/Loose_coupling), with minimal [dependencies](https://en.wikipedia.org/wiki/Dependency_hell) between modules, which makes the process of designing and maintaining them much easier and less error prone. 

**Modular programming** is the process of subdividing a computer program into separate sub-programs. Modules have the following characteristics:
- enforce logical boundaries between components and improve maintainability
- are implemented through *interfaces* (i.e. publicly available methods or properties)
- are designed in such a way as to minimize *dependencies* between different modules

Writing modular code has many benefits:
- it allows many programmers to collaborate on the same application because a small team deals with only a small part of the entire code
- the same code can be used in many applications
- errors can easily be identified, as they are localized to a file, class or function
- the scoping of variables can be easily controlled

The above is adapted from https://www.techopedia.com/definition/25972/modular-programming

We have been getting away with writing "non modular" JavaScript code so far because our programs have been fairly small. But as the size of the program increases, and if more than one developer works on an application, a modular programming architecture becomes essential.

**Today we will apply ES6 module syntax to an application and see these benefits in action.**



<hr>

 <a id="section2">

## II. ES6 Module Syntax

[Exploring ES6](http://exploringjs.com/es6/ch_modules.html#sec_overview-modules) has a nice overview of ES6 modules:

- JavaScript has had modules for a long time - however, they were implemented via libraries, not built into the language
- ES6 is the first time that JavaScript has built-in modules
- ES6 modules are stored in files
- ***There is exactly one module per file and one file per module***

### II-A. `export` and `import`
[export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) is used when creating JavaScript modules to export functions, objects, or primitive values from the module so they can be used by other programs with the import statement.

[import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) is used to import *bindings* (to functions, objects or primitive values) which are exported by another module.

<a id="important-restrictions"/>

### II-B. \*\* Important Restrictions \*\*

ES6 modules have 2 restrictions:
- as of Fall 2022, they are supported by *recent versions* (the last 3 years or so) of all major browsers - see this compatibility chart: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Browser_compatibility)
- they need be hosted on a web server to function, and thus won't work if opened from the desktop of your computer. How can you deal with this restriction?
  - Most IDEs have a "Live Preview" or "Live Server" mode that launches a web server. Figure out how to get than working for your preferred tool:
    - VSCode Live Server:
      - https://ritwickdey.github.io/vscode-live-server/
  - OR, put all of your files on banjo and test them from there (kinda a pain to do all the time)
  - OR, use Python and the `SimpleHTTPServer` module to launch a web server locally - installation and usage instructions are here (the lab machines already have Python installed) -->  https://developer.mozilla.org/en-US/docs/Learn/Common_questions/set_up_a_local_testing_server
  - OR, if you are familiar with node and npm, check out the `http-server` module:
    - but be sure to turn off caching with `http-server -c-1` --> https://www.npmjs.com/package/http-server


<hr>

<a id="section3">
	
## III. Try it out!
	
- A  zipped version is here --> [statz.zip](_files/statz.zip)
- Remember than ES6 modules will only run off of a web server (VSCode's "Live Server" is the easiest way to do this)

<hr>

<a id="section4">
  
## IV. Reference
- What's a *namespace*?
  - https://en.wikipedia.org/wiki/Namespace
- ES6 Module resources
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
  - http://exploringjs.com/es6/ch_modules.html#sec_mixing-named-and-default-exports
  - http://2ality.com/2014/09/es6-modules-final.html
  - https://jakearchibald.com/2017/es-modules-in-browsers/\
  - https://hacks.mozilla.org/2015/08/es6-in-depth-modules/
  - https://blogs.windows.com/msedgedev/2016/05/17/es6-modules-and-beyond/
  - https://www.ecma-international.org/ecma-262/6.0/#sec-imports

<hr>

<a id="section5" />

## V. Review Questions
1. Define the software development term [*loosely coupled*](https://en.wikipedia.org/wiki/Loose_coupling).
2. Give 3 advantages of using modules when coding substantial JavaScript applications.
3. Give 3 things that could go wrong if you don't use modularized code.
4. Is the `"use strict"` declaration necessary for ES6 modules to run in strict mode?

