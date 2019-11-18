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
  - You should also see your `scores2` data has been pulled down from firebase and logged to the console (the second log) 
  - Now open up **firebase-high-score.html** and save some new high score data - both to existing users and new users - you should see the `console.log()` fire again and display the new data 

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
    - listens for data changes at a particular *location* (i.e. node/reference)
    - is the primary way to read data from a database
    - the callback will be triggered for the initial data and again whenever the data changes
    - use `ref.off()` to stop receiving updates
  - `scores2` in the node we are listening to for changes
  - `dataChanged` is the "success" function that will be called when the data changes
    - note that `data.val()` is an object (not an array) with named keys like `MADMAX`, `MADMAX2` etc, so we won't be able to `for..of` it later on like we do with arrays
  - `firebaseError` is the "error" function that will be called if there is an error (if the app is offline, for example)

<hr>

## IV. Our `dataChanged` callback function

- when the app (page) first loads, this is called to get an initial list of scores
- when the data on the `score2` JSON node changes, the changes will be pushed out by firebase to interested applications (i.e. those that setup an "on value" handler for that node

### IV-A. Display the score data

- We will display this data in an "old school" fashion, via DOM manipulation
- For project 3, you are required to have an admin page like this one, but it will instead use Vue.js to update the page

Make **dataChanged()** look like this:

```js
function dataChanged(data){
  let obj = data.val();
  console.log(obj);
  let bigString="";
  for (let key in obj){   // use for..in to interate through object keys
    let row = obj[key];
    bigString += `<li>${row.userID } :  ${row.score}</li>`;
    console.log(row);
  }	
  scoresList.innerHTML = bigString;
}
```

- above, recall that `obj` is an object, not an array, so we instead use a `for..in` loop to iterate through the object keys 
- **You should now see the contents of the `score2` node in the web browser window:**

![screenshot](_images/firebase-13.jpg)

<hr>

### IV-B. Loop through the score data a different way

- Alternatively, you could use `Object.keys()` and a `for..of` loop to do the same thing. Replace the `for..in` line above with this:

`for (let key of Object.keys(obj)){ // use for..of to interate through object keys`

<hr>

## V. Listen for changes to only one object

- Sometimes you are only interested in whether or not a single JSON object changed a value. To accomplish this you just have to change the node (`ref`) that your `on` handler is observing:

```js
firebase.database().ref("scores2/MADMAX").on("value", madmaxChanged, firebaseError);

function madmaxChanged(data){
  let obj = data.val();
  console.log(`madmaxChanged = ${obj}`);
  console.log(`userName = ${obj.userID}`);
  console.log(`score= ${obj.score}`);
}
```

- Here we will only get a single "High Score" object back
- When you first load the page, you will see a log like this:

```
madmaxChanged = [object Object]
userName = MADMAX
score= 60
```

- and when you update the MADMAX score either in the firebase console, or in **firebase-high-score.html**, you will see a log like this:

```
madmaxChanged = [object Object]
userName = MADMAX
score= 110
```

<hr>

## VI. Try it yourself

- add an &lt;h1> to the page that updates to display the MADMAX score (only) whenever that score changes
- change our &lt;ul> to an &lt;ol>, and sort the scores from high to low
- Future challenge once you learn some Vue.js: change this app to use Vue.js to update the interface (i.e. get rid of `document.querySelector()` and DOM manipulation)

<hr>

## VII. Wrap up
- that's all you need to know about firebase to fulfill the project 2 requirements - but there's a lot more you could do, such as writing some rules to secure your data (i.e. don't let someone hack your JavaScript to overwrite your `scores` nodes): 
  - https://firebase.google.com/docs/database/security/quickstart
  - https://firebase.google.com/docs/database/security/
  - https://medium.com/@dftaiwo/understanding-the-power-of-firebase-security-rules-part-1-f46aae773a24
  - https://stackoverflow.com/questions/37482366/is-it-safe-to-expose-firebase-apikey-to-the-public
  - https://stackoverflow.com/questions/35418143/how-to-restrict-firebase-data-modification
  - https://medium.com/google-cloud/how-secure-is-your-firebase-ec4eb882f34b
  - https://javebratt.com/hide-firebase-api/
  
<hr><hr>

**[Previous Chapter <- Firebase Part II - Highscore App](firebase-2.md)**

**[Next Chapter -> Firebase Part IV - Draw & Share](firebase-4.md)**
