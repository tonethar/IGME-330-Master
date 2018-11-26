# 3 - Firebase Highscore Viewer

## I. Overview

- Here we going to create an "admin page" that will subscribe to score updates from Firebase's Realtime Database!

<hr>

## II. Start code

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
<ul id="scoresList"></ul>

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

<hr><hr>

**[Previous Chapter <- Firebase Part II - Highscore App](firebase-2.md)**
