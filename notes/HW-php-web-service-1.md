# PHP Web Service - I

## I. Overview

- In this series, we will build our own web service using the PHP programming language
- This service will be a simple 


## II. Example #1 


## III. Example #2
- Here's another very simple web service, the [Dog API](https://dog.ceo/dog-api/)
- It has 2 major [endpoints](https://rapidapi.com/blog/api-glossary/endpoint/) - the first returns a URL to an image of a random dog. The documentation for this endpoint is here: 
  - https://dog.ceo/api/breeds/image/random
- and the actual endpoint (that gives you the data) is here:
  - https://dog.ceo/api/breeds/image/random
  - when we open this url up in a browser, we can see that this endpoint gives us a random url to a picture of a dog, formatted basically as a JavaScript object literal - which is the JSON (**J**ava**S**cript **O**bject **N**otation) format.
  
  ![screenshot](./_images/php-web-service-1.jpg)
  
 - JSON consists of *key* : *value* pairs, where the key is a string, and the value is one of these types: 
   - `Number`  - `123`, `1.23` etc
   - `String` - "Hello World" etc
   - `Boolean` - 'true' or 'false'
   - `Array` - `[1,2,3]`, `["Hello", "World"]` etc
   - `Object` -  *key* : *value* pairs - `{"name" : "Fred"}`
   - `null`
