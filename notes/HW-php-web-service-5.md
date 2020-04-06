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
  

<hr>

<a id="get-started" />

## I. Get Started

- First, let's practice getting a web app working with simple web service that doesn't require a proxy server. We'll let you try this on your own

1) Grab the **joke-client.html** code from the bottom of [](./HW-php-web-service-3.md) and out it in a file named **XXXX.html**

2) Utilize the XXX web service to download 



<hr><hr>

**[Previous Chapter <- PHP Web Service - Part IV](HW-php-web-service-4.md)**
