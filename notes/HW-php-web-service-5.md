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

![screenshot](./_images/HW-php-web-service-19.jpg)

4) When you are done, ZIP **bored-client.html** and POST it to the myCourses dropbox

<hr>

## II. A service that XHR can't download

1) Now make another copy of **joke-client.html** and name it **shout-client.html**

2) We are going to be using this web service - http://shoutcloud.io - which doesn't do anything for us we couldn't just write one line of JavaScript to do. But it's a great example for us here because it's designed to be hard to access:
  - it doesn't have CORS turned on
  - requires us to use the HTTP POST method
  
3) Let's test the service to see what it can do. Because it requires the POST method, if we try it in the browser's location box we get this:

`404 page not found`

- **instead, we'll look at it using `curl` on the command line:**

```
curl -X POST -d '{"INPUT": "IGME-330 sure is a cool class!"}' -H 'Content-Type: application/json' HTTP://API.SHOUTCLOUD.IO/V1/SHOUT`

{"INPUT":"IGME-330 sure is a cool class!","OUTPUT":"IGME-330 SURE IS A COOL CLASS!"}
```

- **and the Postman application:**

![screenshot](./_images/HW-php-web-service-20.jpg)

- as you can see, we pass in a string, and we get back a string that has been converted to ALL CAPS, yeah that's all it does

<hr><hr>

**[Previous Chapter <- PHP Web Service - Part IV](HW-php-web-service-4.md)**
