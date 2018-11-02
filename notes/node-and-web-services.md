# Node.js and Web Services

## I. Overview

- By this point you have seen how we can easily access JSON web services from the web browser using JavaScript:
  - [Web Apps Part 10 - Web Services](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-10.md)
  - [HW-gif-finder.md](https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md)
  - [Web Service App - Examples & Starters](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-service-app-starters.md)
- We can also download web pages and services from the command line using [Node.js](https://nodejs.org/en/) - let's work through a few examples, giving us more of a chance to work with both web services and Node.js

## II. Install Node.js and npm (if you need to)

- **Node.js** is a command-line JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
  - https://nodejs.org/en/
- **npm** is the package (i.e. "library") manager for JavaScript
  - https://www.npmjs.com
  
 **1) Install Node.js and the Node Package Manager (npm)**
 
- **Note: Mac OS users will often be required to have `sudo` typed at the beginning of any commands whenever they are installing applications or packages.**
 
- You could install Node.js with nvm (the *Node Version Manager*) like this:
 
 ```js
 curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
 ```
 
 - and then: 
 
 ```js
 nvm install node
 node -v
 npm install npm@latest -g
 ```
 
 **Or**
 
 - You can head to https://nodejs.org/en/download/ and grab an installer - instructions are here:
 
 https://docs.npmjs.com/getting-started/installing-node
 
 - When **Node.js** is installed, it also installs **npm** (*Node Package Manager*). Head to the command prompt to verify that npm is installed by typing:
 
 ```js
 npm -v
 ```
 
 - After that, you can run the updater on npm itself by typing:
 
 ```js
 npm install npm@latest -g
 ```
 
 ***At this point you shoukd be ready to go!***
 
## III. Downloading a simple JSON web service
