# Node.js and Web Services

## I. Overview

- By this point you have seen how we can easily access JSON web services from the web browser using JavaScript:
  - [Web Apps Part 10 - Web Services](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-10.md)
  - [Homework: GIF Finder](https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md)
  - [Web Service App - Examples & Starters](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-service-app-starters.md)
- We can also download web pages and services from the command line using [Node.js](https://nodejs.org/en/) - let's work through a few examples, giving us more of a chance to work with both web services and Node.js

## II. Install Node.js and npm (if you need to)

- **Node.js** is a command-line JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, **npm**, is the largest ecosystem of open source libraries in the world.
  - https://nodejs.org/en/
- **npm** is the package (i.e. "library") manager for JavaScript
  - https://www.npmjs.com
  
 **1) How to install Node.js and the Node Package Manager (npm)**
 
- **Note: Mac OS users will often be required to have `sudo` typed at the beginning of any commands whenever they are installing applications or packages.**
 
- You could install Node.js with **nvm** (the *Node Version Manager*) like this:
 
 ```js
 curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
 ```
 
 - and then: 
 
 ```js
 nvm install node
 node -v
 npm install npm@latest -g
 ```
 
 **OR**
 
 - You can head to https://nodejs.org/en/download/ and grab an installer - instructions are here:
 
 https://docs.npmjs.com/getting-started/installing-node
 
 
**2) Test that node and npm are installed**
 
 - When **Node.js** is installed, it also installs **npm** (*Node Package Manager*). Head to the command prompt to verify that npm is installed by typing:
 
 ```js
 npm -v
 ```
 
 - After that, you can run the updater on npm itself by typing (Mac users will need `sudo` again):
 
 ```js
 npm install npm@latest -g
 ```
 
 - ***At this point you should be ready to go!***
 
## III. Downloading a simple "text" web service

- we are going to keep this as bare-bones as possible (not even using `npm`), so we will just download a joke from a "random joke" web service. The web service will return the joke data in plain text format:
  - https://github.com/sameerkumar18/geek-joke-api

1. Get started:
  - create a folder named **joke**
  - inside of the **joke** folder, create a file named **index.js**
  
2. Add the following to **index.js**:

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
  
3. Open your console, and change directory to the **joke** folder. Run the app by typing:

```js
node index.js
```

4. FAILURE!

YOu should see a series of error messages 
