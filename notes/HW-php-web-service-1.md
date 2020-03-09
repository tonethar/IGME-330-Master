# PHP Web Service - I

## I. Overview

- In this series, we will *build our own web service* using the PHP programming language
- You have *used* web services before - by writing HTML/JS apps to download data from *existing web services*, and then formatted and displayed the results for your users
- You did this back in IGME-230/235 - go review those notes now:
  - [Web Apps 10 - Web Services](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-10.md)
  - [Homework: GIF Finder](https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md)
  - [Web Service App - Examples & Starters](https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-service-app-starters.md)
  
### What's a web service, again?
  - The beginning of Wikipedia's [web service](https://en.wikipedia.org/wiki/Web_service) entry is very general and states: "a service offered by an electronic device to another electronic device, communicating with each other via the World Wide Web"
  - More specifically, in this class:
    - the service we will build and use in this class will return data in the JSON (**J**ava**S**cript **O**bject **N**otation) format 
    - the service will be a simple *read-only* web service that will return data, but cannot be written to or updated by the user of the service
    - we will build a "client" (an HTML/JavaScript app) to download the web service via the [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) object and then display the results to a user

## II. Review




## II. Example #1 


## III. Example #2
- Here's another very simple web service, the [Dog API](https://dog.ceo/dog-api/)
- It has 2 major [endpoints](https://rapidapi.com/blog/api-glossary/endpoint/) - the first returns a URL to an image of a random dog. The documentation for this endpoint is here: 
  - https://dog.ceo/api/breeds/image/random
- and the actual endpoint (that gives you the data) is here:
  - https://dog.ceo/api/breeds/image/random
  - when we open this url up in a browser, we can see that this endpoint gives us a random url to a picture of a dog, formatted basically as a JavaScript object literal - which is the JSON (**J**ava**S**cript **O**bject **N**otation) format.
  
  ![screenshot](./_images/HW-php-web-service-1.jpg)
  
 - JSON consists of *key* : *value* pairs, where the key is a string, and the value is one of these types: 
   - `Number`  - `123`, `1.23` etc
   - `String` - "Hello World" etc
   - `Boolean` - 'true' or 'false'
   - `Array` - `[1,2,3]`, `["Hello", "World"]` etc
   - `Object` -  *key* : *value* pairs - `{"name" : "Fred"}`
   - `null`
