# HW - Web Components-6 - Building a "pubsub" object aka "Publish/Subscribe"

## I. Overview

- The "PubSub" sofware design pattern (aka Publisher/Subscriber) is a pattern that allows developers to create code modules that can communicate with each other without depending directly on each other. "Subscribers" (Observers) are notified automatically when a "publisher" - basically an object - wants to notify its subscribers that there has been a change in *state* 
- PubSub allows our code modules to be loosely coupled, minimizing the dependencies between them. This improves code reliability, maintenance, and reusability 
- https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern
- Related patterns:
  - Observer Pattern - https://en.wikipedia.org/wiki/Observer_pattern
  - Notification Center - https://developer.apple.com/documentation/foundation/notificationcenter
  - Broadcaster - \
  - And hopefully you already know about the seminal "Gang Of Four" book [Design Patterns: Elements of Reusable Object-Oriented Software (1994)](https://en.wikipedia.org/wiki/Design_Patterns#Behavioral)
  - And, we touched on these Game Programming Design Patterns in IGME-235 (rhe book is a free download) - https://gameprogrammingpatterns.com/

<hr>

## II. Our "pubsub" object

- Below is the source code and comments for our `pubsub` object
- Bs you can see, there's not much code here, but it really will get the job done

![screenshot](_images/_wc/HW-wc-16.png)


![screenshot](_images/_wc/HW-wc-17.png)

<hr>

### III-A. Let's save you a little bit of typing

- Here is a stub, with mostly the comments preserved, you can type the rest in on your own:

**pubsub.js**

```js
<!--   The following should probably be in an external file named  pubsub.js, and then brought in with a regular <script> tag -->
	<script>
		// This `pubsub` global object is an implementation of the classic "Observer" (or "Notification Center") software design pattern
    // I made `pubsub` global so that it could be used with ES6 modules, or with older client-side JS syntax
		// The code is adapted from this article - https://docs.microsoft.com/en-us/previous-versions/msdn10/hh201955(v=msdn.10)
		// 1- Below is an IIFE - "Immediately Invoked Function Expression - pronounced "Iffy"
  (function() {
    // 2 - `pubsub` is an object we going make global at the end of this IIFE
	  // Why are we using an object literal instead of a class? Because we only need ONE instance 

 
		 // 3 - `topics` is a map (object literal) that stores topic names that can be broadcast or listened for
		 // `topics` can also be thought of as "events" or "messages"
		 // but to keep with the Publish/Subscribe metaphor, we'll just call them `topics`
		 // `topics` also stores references to "subscribers"
		 // "subscribers" are blocks of code that will be executed whenever the specific topic they are "interested in" is published

	
		 // 4 - unique identifier for each subscriber
		 let subUid = -1;
	
		 // 5- Publish or broadcast topics of interest
		 // and send the specific topic name and an info object
		 // In this example, the <my-list> component will be the publisher

	
		// 6 - Subscribe to events of interest with a specific topic name and a
		// callback function, to be executed when the topic (i.e. the event) is observed
		 
				// sends back a unique id, which can be used to later .unsubscribe if desired,
				// similar to how `window.setInterval()` sends back an intervalId
	
		 // 7 - Unsubscribe from a specific topic, using the subscription uid

		// 8 - logs out the topics, and the subscriptions that belong to each one

		// 9 - put `pubsub` into global namespace

 }());
``` 

<hr>

## III. Using the `pubsub` object

- ***publishing*** (broadcasting) a "lengthchanged" event could look like this:

```
pubsub.publish("lengthchanged", {target: this, length: this.length});
```

- ***subscribing to*** (listening) for a "lengthchanged" event would look like this:

```js
const logger =  (topicName, info) => {
  console.log( `Topic Name: ${topicName} - info:`, info);
};

const updateLengthOnPage = (topicName, info) => {
  if(info.target == colorList){
    outputText.innerHTML = info.length;
  }
};

pubsub.subscribe("lengthchanged",logger); // send data to a logging function
pubsub.subscribe("lengthchanged",updateLengthOnPage); // update DOM
```
		
<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components V**](HW-wc-5.md)  |  [**IGME-330**](../README.md) | :-\
