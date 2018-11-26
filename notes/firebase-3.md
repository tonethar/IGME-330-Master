# 3 - Firebase Highscore Viewer

## I. Overview

- Here we going to create an "admin page" that will subscribe to score updates from Firebase's Realtime Database!

<hr>

## II. Start code

- The code below will create the interface for this "admin" page
- Be sure to add your firebase setup code to #1 and #2 below
- Test the app, you should see something like the screenshot below:
  - There won't be anything in our unordered list other than the "No data yet!" text
  - You should see the firebase object logged to the console

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
	
**Screenshot:**
	
![screenshot](_images/firebase-12.jpg)
	
</script>
</body>
</html>
```

<hr><hr>

**[Previous Chapter <- Firebase Part II - Highscore App](firebase-2.md)**
