# PHP Web Service Part V - creating a proxy server


[Overview](#overview)

[I. Get Started](#get-started)

<hr><hr>

<a id="overview" />

## Overview

- Here we are going to learn how to create a web *proxy server* with PHP, and also get a little more practice with using the [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) API to download data
-  *a proxy server is a server application or appliance that acts as an intermediary for requests from clients seeking resources from servers that provide those resources* - https://en.wikipedia.org/wiki/Proxy_server#Web_proxy_servers
- Below we will learn how to create such a server and have PHP fetch a web service that the browser (i.e the XHR object) is unable to directly access/ THis could happen for the follwoing reasons:
  - the web service does not have [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) enabled ("cross origin resource sharing") - which means that the browser will not allow the client-side XHR or [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) objects to download data from that service
    - recall that if a web service wants to "turn CORS on" it needs to send this HTTP response header:
      - `Access-Control-Allow-Origin: *`
  - the web service is only available via `http` (rather than `https` - the "s" stands for *secure*), which means our banjo.rit.edu server will not our app to use that service
- You might be wondering - how common is it for web services to have CORS turned off?
  - one popular API - [Yelp](https://www.yelp.com/developers/documentation/v3/get_started) - has CORS turned off, and requires developers to send their API key as an HTTP header, which means you have to use a server-side script of some kind to accomplish this.
  - another advantage of using a proxy-server is that the developer can "hide" their web service API key on the server, rather than having it exposed in the client-side JavaScript
  

<hr>

<a id="get-started" />

## I. Get Started - a little XHR review

- First, let's practice getting a web app working with simple web service that doesn't require a proxy server. We'll let you try this on your own

1) Grab the **joke-client.html** code from the bottom of [PHP Web Service Part III - Coding get-random-joke.php](./HW-php-web-service-3.md#client-app) and put it in a file named **bored-client.html**

2) Now utilize the `http://www.boredapi.com/api/activity` web service to download a random activity for bored people. Go ahead and open that URL up in a web browser to see what the JSON looks like. Here are the app requirements: 

    - when the user clicks the button, a random activity will be downloaded
    - the value of the "activity", "type", and "price" keys will be displayed to the user
    - when the user clicks the button, the old activity will be removed and a new one will be shown
  
3) The final result will look something like this:

<hr>

![screenshot](./_images/HW-php-web-service-19.jpg)

<hr>

4) When you are done, ZIP **bored-client.html** and POST it to the myCourses dropbox

<hr>

<a id="intro-shoutcloud" />

## II. Introducing SHOUTCLOUD - a "service" that XHR can't download

1) Now make another copy of **joke-client.html** and name it **shout-client.html**

2) We are going to be using this web service - http://shoutcloud.io - which doesn't do anything for us we couldn't just write one line of JavaScript to do. But it's a great example for us here because it's designed to be hard to access:
    - it doesn't have CORS turned on
    - it requires us to use the [HTTP POST method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
  
3) Let's test the service to see what it can do. Because it requires the POST method, if we try it in the browser's location box we get this:

`404 page not found`

- **instead, we'll look at it using `curl` on the command line:**

```
curl -X POST -d '{"INPUT": "IGME-330 sure is a cool class!"}' -H 'Content-Type: application/json' HTTP://API.SHOUTCLOUD.IO/V1/SHOUT`

{"INPUT":"IGME-330 sure is a cool class!","OUTPUT":"IGME-330 SURE IS A COOL CLASS!"}
```

- **and the [Postman](https://www.postman.com) application:**

<hr>

![screenshot](./_images/HW-php-web-service-20.jpg)

<hr>

- as you can see, we pass in a string, and we get back a JSON object with an "OUTPUT" string that has converted the "INPUT" string to ALL CAPS (yeah that's all it does...)

<hr>


4) So let's try this service out in **shout-client.html** by changing the value of the `url` variable to `HTTP://API.SHOUTCLOUD.IO/V1/SHOUT` - and then clicking the button which calls the service

5) This is what we'll get back in the console:

    - `Access to XMLHttpRequest at 'http://api.shoutcloud.io/V1/SHOUT' from origin 'null' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.`
    - so yeah, CORS isn't turned on. If we go back and look at the header in the Postman app example above, we'll see that `Access-Control-Allow-Origin: *` is not present
  
6) So we need to create a PHP proxy server - let's move on ...

## III. Creating *shout-proxy.php*

1) Here's our first attempt - you are going to have to post this up on banjo:


**shout-proxy.php**

```php
<?php
  $url = "HTTP://API.SHOUTCLOUD.IO/V1/SHOUT";
  $string = file_get_contents($url);
  echo $string;
?>
```
 - Normally, this code would work fine because PHP's [`file_get_contents()`](https://www.php.net/manual/en/function.file-get-contents.php) defaults to using the `GET` method when contacting a web server, which is what most web services use
 - However, SHOUTCLOUD's API expects the client to use POST method, which is different:
   - parameters are sent in the *query string* when using GET, but are sent in a *separate file* when using POST
   - here is a brief explanation of HTTP methods --> https://www.w3schools.com/tags/ref_httpmethods.asp
   
2) This fails with the following message!

`Warning: file_get_contents(HTTP://API.SHOUTCLOUD.IO/V1/SHOUT): failed to open stream: HTTP request failed! HTTP/1.1 404 Not Found in shout-proxy.php on line 3`

3) Here is our fix, note that we have to do a little more work to configure `file_get_contents()`:

```php

```


<hr><hr>

**[Previous Chapter <- PHP Web Service - Part IV](HW-php-web-service-4.md)**
