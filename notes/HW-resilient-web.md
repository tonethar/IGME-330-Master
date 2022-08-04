# HW - Video - Building a Resilient Web

## Instructions
- Watch the this LinkedIn Learning course here (1.25x video speed recommended): https://www.linkedin.com/learning/building-a-resilient-web/
- Copy/paste the questions below into a MS Word DOC and answer them

<hr><hr>

## 1 - The Resilient Web - an Introduction

1) According to Jeremy Keith's Resilient Web Design book  - what is the "Core Purpose of the web"?

1) What is supposed to happen if a browser encounters a document with HTML and CSS errors?

1) JavaScript errors should _____________________________

1) List the 5 "Known unknowns" of the web

1) If a web site is resilient, how should disabling JavaScript and the default stylesheet of that web page effect it?

1) What are the 4 HTML design principles as specified by the W3C? Briefly summarize each. 

1) HTML and CSS are *declarative* languages - what does that mean?

1) JavaScript is an *imperative* language - what does that mean?

1) Which kind of language is more *resilient* and more *fault tolerant*?


## 2 - The Robust Web

1) What are the three core materials of the web?

2) *Priority of constituents*. Re-order the following constituents to their order of priority, *highest to lowest*:

    - *authors*
    - *implementors*
    - *specifiers*
    - *theoretical purity*
    - *users*

3) As the tools we use to write imperative code "distance" us from the code that the user sees, what is "introduced"?

4) Which "web stack" layer is the "presentation" layer?

5) What is the difference between a "robust" website and a "resilient" one? Which is preferred?

6) Do web sites need to be "robust" meaning that they "look the same everywhere"?

7) What do users "care about"?


## 3 - The Fragile Web

1) Give 2 examples of ways to make sure that *web impermanence* does not result in information loss

1) Give the 3 items from "Morten's Accessibility Checklist"

1) Give one advantage to the "One-way Binding" that HTML links use

1) Resiliency means the ___________  is met for all users in all circumstances

1) Large media files mean _________________

1) List 3 best practices for resilient images

1) List 3 best practices for resilient audio and video

1) Resiliency means ensuring the information transfer ______________


## 4 - Resilience Basics
XX) Progressive enhancement is serving a baseline solution to all browsers and then progressively enhancing the experience with whatever advanced feature the user's browser makes available. *(No answer required)*

XX) Pure HTML is as resilient as you can get it. And taking full advantage of what the language has on offer means building resilience into the core. So before you build a JavaScript component make sure there isn't already an HTML element you can use. *(No answer required)*

XX) The whole point of the web is to make information accessible to whomever wants access. *(No answer required)*

XX) The best place to start is with proper semantic HTML. *(No answer required)*

XX) Using progressive enhancement in CSS, we can serve up both robust CSS that works for everyone and take advantage of all the latest and greatest features on offer without having to downgrade the experience for any one user.  *(No answer required)*

1) What does `@supports` do?

2) What is a JavaScript *polyfill*?

3) Babel, webpack, et cetera, all automatically ________ modern code for older browsers enabling us to write modern code for all browsers knowing it'll work everywhere. 

4) Link persistency - how can you get the server to send all of these status codes? .htaccess files! You covered these in IGME-235. You can also potentially use meta-refresh or JS - https://en.wikipedia.org/wiki/Meta_refresh *(No answer required)*

5) What does a JavaScript *service worker* do?

6) What are *web components*?

7) If you serve the browser with a custom element and the browser is unable to interpret it as a web component, it will interpret it as a _______________

XX) Make sure the content and information, the intent the component is meant to communicate, is resilient and persistent even if the component doesn't work or JavaScript fails. That way, you can use web components safely and in a resilient way. *(No answer required)*

## 5 - JavaScript Frameworks
1) What does CSR stand for?

2) What does SSR stand for?

XX) Using server side rendering and hydration in a JavaScript framework like React (with Gatsby), you can make the framework part of progressive enhancement and at the same time make the site and all its information resilient *(No answer required)*

XX) Developer experience is secondary to end-user experience when it comes to the web platform and JavaScript frameworks can invisibly shift this priority of constituents if we're not careful. As we build a resilient web together, we must make careful decisions around how and when we use JavaScript front-end frameworks so we get the most effective use out of them without the frameworks standing in the way of resilience. This boils down to charting out what my website or application needs and what tools the web platform already provides. *(No answer required)*


## 6 - Building a resilient web application
- The first and primary goal is achieving the user's goal, whatever goal that may be. *(No answer required)*
- Resilience tests include:
  - user goal can be achieved with JavaScript disabled
  - user goal can be achieved on a slow connection
  - user goal can be achieved using an old feature phone
  - user goal can be achieved in offline mode
  - content is accessible using alternative input modalities and screen readers
  - the site and app meets or exceeds accessibility standards

*(No answer required)*

- To sum up, what is the user's goal? How do we ensure the user can meet this goal? And how do we test to prove the above? *(No answer required)*
- The user might never access the website or web app at all, but instead consume its content through some other application of their choosing. To be able to support this type of behavior, our content must be resilient, and that resiliency must start with standard functional semantic HTML. Keep the HTML you're building front of mind at all times, because in many cases that might be the only thing the user ever sees. *(No answer required)*
- Accessibility is arguably the most important aspect of the web *(No answer required)*
- The most significant step towards embracing progressive enhancement in your work is to accept that a website or app should not look or function the same in all environments. Instead, it should adapt to whatever environment it finds itself in and provide the same service in that context using whatever features are available. *(No answer required)*
- Make link management part of that responsibility and define a link management strategy. *(No answer required)*

<hr><hr>

## Reference
- https://resilientwebdesign.com
- https://www.w3.org/TR/html-design-principles/ 
- https://alistapart.com/article/understandingprogressiveenhancement/

