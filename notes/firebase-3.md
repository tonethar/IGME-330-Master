# 3 - Firebase Highscore Viewer

## I. Overview

- Here we going to create an "admin page" that will subscribe to score updates from Firebase's Realtime Database!

<hr>

## II. Start code

- The code below will create the interface for this "admin" page
- Be sure to add your firebase setup code to #1 and #2 below
- Test the app, you should see something like the screenshot below:
  - There won't be anything in our unordered list other than the "No data yet!" text
  - You should see the firebase object logged to the console (the first log)
  - You should also see your `scores2` data logged to the console (the second log) 

**firebase-admin.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Firebase Admin</title>
</head>
<body>
<h1>High Scores</h1>
<ul id="scoresList"><li>No data yet!</li></ul>

<!-- #1 - link to Firebase goes here  -->

<script>
  /* #2 - The rest of the Firebase setup code goes here */

  console.log(firebase); // #3 - make sure firebase is loaded
	
  // #4 This is where the magic happens!
  firebase.database().ref("scores2").on("value", dataChanged, firebaseError);
	
  function dataChanged(data){
    console.log(data.val());
  }
	
  function firebaseError(error){
    console.log(error);
  }
	
</script>
</body>
</html>
```

**Screenshot:**
	
![screenshot](_images/firebase-12.jpg)

<hr>

## III. `firebase.database.ref.on`

- Comment #4 above used this line - `firebase.database().ref("scores2").on("value", dataChanged, firebaseError);` - to listen for changes to our firebase database:
  - `firebase.database.ref.on`:
    - is documented here --> https://firebase.google.com/docs/reference/js/firebase.database.Reference?authuser=0#on
    - listens for data changes at a particular location (i.e. node/reference)
    - is the primary way to read data from a Database
    - the callback will be triggered for the initial data and again whenever the data changes
    - use `ref.off()` to stop receiving updates
  - `scores2` in the node we are listening to for changes
  - `dataChanged` is the "success" function that will be called when the data changes
  - `firebaseError` is the "error" function that will be called if there is an error (if the app is offline, for example)

<hr>

## IV. Our `dataChanged` callback function

- when the app (page) first loads, this is called to get an initial list of scores
- when the data on the `score2` JSON node changes, the changes will be pushed out by firebase to interested



<hr><hr>

**[Previous Chapter <- Firebase Part II - Highscore App](firebase-2.md)**
