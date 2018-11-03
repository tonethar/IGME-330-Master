# Node.js and Web Services

## Overview

- By this point you have seen how we can access JSON web services from the web browser using JavaScript:
  - [Web Apps Part 10 - Web Services](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-10.md)
  - [Homework: GIF Finder](https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md)
  - [Web Service App - Examples & Starters](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-service-app-starters.md)
- We can also download web pages and services from the **command line** using [Node.js](https://nodejs.org/en/) - below we will work through a few examples, giving us more of a chance to work with both web services and Node.js
- We will also see how we can create symbolic links and easily run these programs as command line tools

## Contents

<!--- Local Navigation --->
I. [Install Node.js and npm (if you need to)](#section1)

II. [Downloading a simple "text" web service](#section2)

III. [Downloading a JSON web service](#section3)

<a id="section1"></a>

## I. Install Node.js and npm (if you need to) 

- **Node.js** is a command-line JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, **npm**, is the largest ecosystem of open source libraries in the world.
  - https://nodejs.org/en/
- **npm** is the package (i.e. "library") manager for JavaScript
  - https://www.npmjs.com
  
To see if you already have node and npm installed on your computer, type the following in the console:

```js
node -v
npm -v
```
  
### A) How to install Node.js and the Node Package Manager (npm)
 
- ***Important Note: Mac OS users will often be required to have `sudo` typed at the beginning of any commands whenever they are installing applications or packages.***
 
- You could install Node.js with **nvm** (the *Node Version Manager*) like this:
 
 ```js
 curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
 ```
 
 - and then: 
 
 ```js
 nvm install node
 node -v
 npm install npm@latest -g
 npm -v
 ```
 
 **OR**
 
 - You can head to https://nodejs.org/en/download/ and grab an installer - instructions are here:
 
 https://docs.npmjs.com/getting-started/installing-node
 
 
### B) Test that node and npm are installed
 
 - When **Node.js** is installed, it also installs **npm** (*Node Package Manager*). Head to the command prompt to verify that npm is installed by typing:
 
 ```js
 node -v
 npm -v
 ```
 
 - After that, you can run the updater on npm itself by typing (Mac users will need `sudo` again):
 
 ```js
 npm install npm@latest -g
 ```
 
 - ***At this point you should be ready to go!***
 
<a id="section2"></a>
  
## II. Downloading a simple "text" web service

- we are going to keep this as bare-bones as possible (not even using `npm`), so we will just download a joke from a "random Chuck Norris joke" web service. The web service will return the joke data in plain text format:
  - https://github.com/sameerkumar18/geek-joke-api

### A. Get started:
  - create a folder named **joke**
  - inside of the **joke** folder, create a file named **index.js**
  
### B. Add the following to **index.js**:

```js
// #1 - import the request module, which is used to download data over http
const request = require('request');

// #2 - set the value of the `options` object, which contains configuration data,
// including the URL we are interested in downloading
// https://nodejs.org/docs/latest-v9.x/api/http.html#http_http_request_options_callback
const options = {
    url: 'https://geek-jokes.sameerkumar.website/api',
    method: 'GET'
}

// #3 - make the request
// the second parameter below is a callback function (an ES6 arrow function in this case)
// which is called when the data is downloaded
request(options, (err, response, body) => {
		// if there's no error, and if the server's status code is 200 (i.e. "Ok")
    if(!err && response.statusCode == 200)
    		// log out the plain-text joke - no parsing required!
        console.log(body)
});
```
  
### C. Open your console, and change directory to the **joke** folder. Run the app by typing:

```js
node index.js
```

### D. FAILURE!

- You should see a series of error messages that begin with **`Error: Cannot find module 'request'`** 
- This is happening because you never downloaded the files that node needs to actually import the **request** module code.

### E. Download the **request** module by typing this (Mac users will need `sudo` again):

```js
npm install request
```

- Downloading of files now should begin. Once downloading has completed, you will see a few warnings about a file named **package.json** missing - we will address this in the next section.
- You should now see a folder named **node_modules** - open it up and you will that that there are approximately 50 sub-folders, including one named **request**. These additional folders are all of the modules that the **request module** is dependent on.
- You will see one more file **package-lock.json**  - this file keeps track of all of the project modules and dependencies - you won't need to worry about for our examples - but if you wish you can read about it here: https://docs.npmjs.com/files/package-lock.json

### F. Try to run the app again by typing:

```js
node index.js
```

**SUCCESS! - You should see a joke in the console - something like:**

```
"The First rule of Chuck Norris is: you do not talk about Chuck Norris."
```

### G. Next Steps

- There isn't too much more to do with this example right now, but once you have finished this entire chapter, come back to this example and:
  - use `npm init -y` to create a **package.json** file
  - using the instructions here as a guide, make this script an executable command named `get-joke`: https://medium.com/netscape/a-guide-to-create-a-nodejs-command-line-package-c2166ad0452e


<a id="section3"></a>

## III. Downloading a JSON web service 

We are going to look at how to download another web service, in this case an "inspirational design quote" service. Although this sounds really similar to what we did last time, there are differences that will make this more challenging:
- we are going to create a **package.json** file this time
- the data is in the JSON format so we will need to parse it before displaying it
- the web service takes parameters, such as the number of results:
  - this means we will need to format the URL differently
  - we will need to loop though the results
  - we will need to give the user of this script the ability to choose how many results they want

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
- to re-install **request** - just type `npm install` - which will re-download the **request** module because it is listed in the `dependencies:` key of **package.json**
- run your script again - `node init.js` - it succeeds!


### XXX. Add the following to **index.js**:


