# Node.js and Web Services - 2

## Overview

THis time we are going to look at how to download a different web service, in this case an "inspirational design quote" service. Although this sounds really similar to what we did last time, there are differences that will make this more challenging:
- we are going to create a **package.json** file this time
- the data is in the JSON format so we will need to parse it before displaying it
- the web service takes parameters, such as the number of results:
  - this means we will need to format the URL differently
  - we will need to loop though the results
  - we will need to give the user of this script the ability to choose how many results they want (i.e. pass argments to the web service)
- the documentation on this web service is here: https://quotesondesign.com/api-v4-0/

## Contents

<!--- Local Navigation --->
I. [Preview our new web service](#section1)

II. [Working with the package.json file](#section2)


<a id="section1"></a>

## I. Preview our new web service

- Open up a new window in Chrome and open this URL:

```
http://quotesondesign.com/wp-json/posts?filter[orderby]=rand&filter[posts_per_page]=1
```

- which gives you 1 random inspirational quote, in an array, that looks like this:

![screenshot](_images/node-web-services-2.jpg)

- as you can see above, we are probably most interested in the `.title` and `.content` properties
- one wrinkle is that the content has HTML in it - which we are going to need to strip out for this command line application
- If your JSON isn't as nicely formatted as mine, it's because I am using the Chrome JSON Viewer extension which you can get here: https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh

<a id="section2"></a>

## II. Working with the package.json file

### A. Get started:

- create a new folder named **quote**
- copy over your completed **index.js** file from Part I


### B. Create a node project the usual way
- this time we are going to follow the usual practice and create a node project with **npm** - go ahead and change directory to the **quote** folder and type:

```js
npm init -y
```

This will create your **package.json** file with default metadata about your project, which are in an object literal, which should look something like this:

```js
{
  "name": "quote",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

### C. Download the **request** module 

This time, we are going to download the **request** module, and then *save* this dependency into the **package.json** file. Type the following in (Mac users will need `sudo` again):

```js
npm install request --save
```

- This will download and install the **request** module and other dependencies to the **node_modules** folder just like last time
- The `--save` flag is what tells npm to add a dependency to **package.json**, which you can see if you open the file:

```js
"dependencies": {
    "request": "^2.88.0"
  }
```

- note that we didn't get the warnings about the missing **package.json** file like we did last time

### D. Test the script

- Run the script to be sure that it still works as before:

```js
node init.js
```
 
 - Which should print out another Chuck Norris joke such as:
 
 ```
"Chuck Norris can do a roundhouse kick faster than the speed of light. This means that if you turn on a light switch, you will be dead before the lightbulb turns on."
 ```
 
### E. Test package.json

- delete your **node_modules** folder
- if you run your script again - `node init.js` - it fails! - because the **request** module is nowhere to be found
- to re-install the **request** module files - just type `npm install` - which will re-download the **request** module and its dependencies because it is listed in the `dependencies:` key of **package.json**
- run your script again - `node init.js` - it succeeds!



<hr><hr>

**[Previous Chapter <- Node.js and Web Services (chapter 1)](node-and-web-services-1.md)**

**[Next Chapter -> Node.js and Web Services (chapter 3)](node-and-web-services-3.md)**
