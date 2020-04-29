# Simple Proxy Server

## I. Overview 

- the **shout-proxy.php** server from [HW-php-web-service-5.md](./HW-php-web-service-5.md) was used to download data from the SHOUTIFY web service
- the SHOUTIFY web service is problematic (and not typical) because it requires POST requests, where any additional parameters must be passed in a separate file
- what if the web service you have just uses plain old GET requests (where the web service parameters are encode in the query string) - how do you handle it?
- much more simply! see below!

## II. The web service we need to download
- The google books API is free and easy to use - go check it out now - here we are passing in a `q` parameter with a value of `books`:
  - https://www.googleapis.com/books/v1/volumes?q=western
  - see the first screenshot below
  - but there's one major issue with this web service - CORS is NOT turned on. We know this because the `Access-Control-Allow-Origin: *` header is missing (see the second screenshot below)
  
  <hr>
  
  ![screenshot](_images/simple-proxy-server-1.jpg)
  
  <hr>
  
  ![screenshot](_images/simple-proxy-server-2.jpg)
   
  <hr>
   
   ## III. 
  
  
  
