# HW - Video - Building a Resilient Web

## Instructions
- Watch the this LinkedIn Learning course here (1.25x video speed recommended): https://www.linkedin.com/learning/building-a-resilient-web/
- Copy/paste the questions below into a MS Word DOC and answer them

## 1 - The Resilient Web - an Introduction

1) According to Jeremy Keith's Resilient Web Design book  - what is the "Core Purpose of the web"?

1) What is supposed to happen if a browser encounters a document with HTML and CSS errors?

1) JavaScript errors should _____________________________
- List the 5 "Known unknowns" of the web
- If a web site is resilient, how should disabling JavaScript and the default stylesheet of that web page effect it?
- What are the 4 HTML design principles as specified by the W3C? Briefly summarize each. 
- HTML and CSS are *declarative* languages - what does that mean?
- JavaScript is an *imperative* language - what does that mean?
- Which kind of language is more *resilient* and more fault tolerant?


## 2 - The Robust Web

- What are the three core materials of the web?
- Priority of constituents. Place the following constituents in their order of priority, highest to lowest. authors, implementors, specifiers, theoretical purity, users
- As the tools we use to write imperative code "distance" us from the code that the user sees, what is "introduced"?
- Which "web stack" layer is the "presentation" layer?
- What is the difference between a "robust" website and a "resilient" one? Which is preferred?
- Do web sites need to be "robust" meaning that they "look the same everywhere"?
- What do users "care about"?


## 3 - The Fragile Web

- Give 2 examples of ways to make sure that *web impermanence* does not result in information loss
- Give the 3 items from "Morten's Accessibility Checklist"
- Give one advantage to the "One-way Binding" that HTML links use
- Resiliency means the ___________  is met for all users in all circumstances
- Large media files mean _________________
- List 3 best practices for resilient images
- List 3 best practices for resilient audio and video
- Resiliency means ensuring the information transfer ______________


## 4 - Resilience Basics
- Progressive enhancement is serving a baseline solution to all browsers and then progressively enhancing the experience with whatever advanced feature the user's browser makes available. *(No answer required)*
- Pure HTML is as resilient as you can get it. And taking full advantage of what the language has on offer means building resilience into the core. So before you build a JavaScript component make sure there isn't already an HTML element you can use. *(No answer required)*
- The whole point of the web is to make information accessible to whomever wants access. *(No answer required)*
- The best place to start is with proper semantic HTML. *(No answer required)*
Using progressive enhancement in CSS, we can serve up both robust CSS that works for everyone and take advantage of all the latest and greatest features on offer without having to downgrade the experience for any one user.  *(No answer required)*
- What does `@supports` do?
- What is a JavaScript *polyfill*?
- Babel, webpack, et cetera, all automatically ________ modern code for older browsers enabling us to write modern code for all browsers knowing it'll work everywhere. 
- Link persistency - how can you get the server to send all of these status codes? .htaccess files! You covered these in IGME-235. You can also potentially use meta-refresh or JS - https://en.wikipedia.org/wiki/Meta_refresh *(No answer required)*
- What does a JavaScript *service worker* do?
- What are *web components*?
- If you serve the browser with a custom element and the browser is unable to interpret it as a web component, it will interpret it as a _______________
- Make sure the content and information, the intent the component is meant to communicate, is resilient and persistent even if the component doesn't work or JavaScript fails. That way, you can use web components safely and in a resilient way. *(No answer required)*

## 5 - JavaScript Frameworks
- What does CSR stand for?
- What does SSR stand for?
- Using server side rendering and hydration in a JavaScript framework like React (with Gatsby), you can make the framework part of progressive enhancement and at the same time make the site and all its information resilient *(No answer required)*
- Developer experience is secondary to end-user experience when it comes to the web platform and JavaScript frameworks can invisibly shift this priority of constituents if we're not careful. As we build a resilient web together, we must make careful decisions around how and when we use JavaScript front-end frameworks so we get the most effective use out of them without the frameworks standing in the way of resilience. This boils down to charting out what my website or application needs and what tools the web platform already provides. *(No answer required)*


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



## Reference
- https://resilientwebdesign.com
- https://www.w3.org/TR/html-design-principles/ 
- https://alistapart.com/article/understandingprogressiveenhancement/

