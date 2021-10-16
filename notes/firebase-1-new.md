# 1 - Intro to Firebase - the Realtime Database

## I. Overview
- Here we will look at setting up a Firebase *Realtime Database*
  - The Firebase Realtime Database is a cloud-hosted database
  - Data is stored as JSON and synchronized in realtime to every connected client
  - Firebase apps remain responsive even when offline because the Firebase Realtime Database SDK persists your data to disk

<hr><hr>

## II. Setting up a *Realtime Database*

### II-A. Create a new project
- \*\****NOTE: If you run into trouble when you try to set up the Realtime Database (below) with an RIT Gmail account, you may have to instead use your personal Google Account***\*\*
- Head to https://console.firebase.google.com/ 
  - click the **Create Project** or **Add Project** button
  - this will create a pop-up window where you will name your project

![screenshot](_images/_firebase/firebase-NEW-1.jpg)

<hr>

### II-B. Name the project

- Name the project **high-scores** and click the **Continue** button

![screenshot](_images/_firebase/firebase-NEW-2.jpg)

<hr>

### II-C. Turn Off Google Analytics and Create the Project

- Uncheck **Enable Google Analytics**
- Click the **Create Project** button

![screenshot](_images/_firebase/firebase-NEW-3.jpg)

<hr>

- On the next screen, after your **high-scores** project has been created, click the **Continue** Button

<hr>

### II-D. Add a *Web App* to your project

- On the Project Overview Screen, click the **Web** button

![screenshot](_images/_firebase/firebase-NEW-4.jpg)

<hr>

### II-E. Add Firebase to your web app

- Give the app the nickname of **high-scores-database**
- Do NOT check the checkbox to set up Firebase Hosting
- Click the **Register App** button

![screenshot](_images/_firebase/firebase-NEW-5.jpg)

<hr>


### II-F. Copy the code snippet

- Under Add **Firebase SDK** step:
  - choose the **Use a `<script>` tag** radio button
  - go ahead and create an empty HTML file named **firebase-test.html**
  - copy/paste the Firebase JS code into the document, at the bottom of the `<body>` tag
  - when you are done, click the **Continue to console** button at the bottom of the page
  - **Note:** If you need to get this setup code at a later time, go to **Develop > Authentication** in the [Firebase console](https://console.firebase.google.com), select the project, then click **Web Setup**

![screenshot](_images/_firebase/firebase-NEW-6.jpg)

**firebase-test.html**
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Firebase Test</title>
</head>
<body>
</body>
</html>
```

<hr>

### II-G. Create a Realtime Database

- Now you should be on the **Project Overview Screen**
- Go ahead and click on the **Realtime Database** button on the left side of the screen 

![screenshot](_images/_firebase/firebase-NEW-7.jpg)

<hr>

- On the Realtime Database screen, go ahead and click the **Create Database** button

<hr>


### II-H. Choose location and Security rules

- Choose you location (probably the default) and click the **Next** button

![screenshot](_images/_firebase/firebase-NEW-8.jpg)

<hr>

- On the next screen, choose the **Start in test mode** radio button
- Click the **Enable** button

![screenshot](_images/_firebase/firebase-NEW-9.jpg)

<hr>

### II-I. Verify

- You should now have created an empty *Realtime Database*
- Move the mouse over to where the arrow is until you see the **+** button appear

![screenshot](_images/_firebase/firebase-NEW-10.jpg)

<hr>

### II-J. Add a little bit of data to your Realtime Database

- All Firebase Realtime Database data is stored as JSON objects, and you can think of the database as a cloud-hosted JSON tree
- Unlike a SQL database, there are no tables or records
- When you add data to the JSON tree, it becomes a node in the existing JSON structure with an associated key
- You can provide your own keys, such as user IDs or semantic names, or they can be provided for you using `push()`
- The Firebase Realtime Database allows nesting data up to 32 levels deep, but you should avoid nesting data for performance reasons - e.g. when you fetch data at a location in your database, you also retrieve all of its child nodes

<hr>

- Click the **+** button
- Go ahead and add an `owner` **Name** with a **Value** of your name (or nickname)

![screenshot](_images/_firebase/firebase-NEW-11.jpg)

<hr>

- Then click the **Add** button
- Congrats! You'e created your Firebase Realtime Database (finally) and added some data to it!

![screenshot](_images/_firebase/firebase-NEW-12.jpg)

<hr><hr>

## III. Do some coding

- BTW - If you get stuck on anything related to the Realtime Database, the best place to look is in the [Firebase Realtime Database - Installation & Setup in JavaScript](https://firebase.google.com/docs/database/web/start) page

### III-A. Getting ready
- First, open **firebase-test.html** and add this line of code to the end of the `<script>` tag - `console.log(app);`
- Open the page in a browser and check the console - you should see a log

<hr>

### III-B. `import` the Firebase Realtime Database library

- Add the following code, right after the `initializeApp` ES6 `import`

```js
import { getDatabase, ref, set, push, onValue } from  "https://www.gstatic.com/firebasejs/9.1.3/firebase-database.js";
```

- This line of code imports 5 functions from Firebase Realtime Database library so that we can use them
- We will only be using the first 3 symbols for this part: `getDatabase`, `ref` and `set`

<hr>

### III-C. Create a helper function and call it

- Add the following code to the bottom of the `<script>` tag

```js
function writeUserData(userId, name, email) {
  const db = getDatabase();
  set(ref(db, 'users/' + userId), {
    username: name,
    email: email
  });
}

writeUserData("abc1234","Ace Coder","ace@rit.edu");
writeUserData("xyz9876","Ima Student","ima@rit.edu");
```

<hr>

### III-D. Test it

- Reload the browser, you should not see any errors in the console, has anything happened?
- Go check your Realtime Database - you should see something like this - which means that you have successfully pushed data to the "cloud"!

![screenshot](_images/_firebase/firebase-NEW-13.jpg)

<hr>

### III-E. How does the above code work?
- Firebase Documentation --> https://firebase.google.com/docs/reference/js/
- Firebase Realtime Database Documentation --> https://firebase.google.com/docs/reference/js/database.md
- Go read about these now:
  - `initializeApp()` --> https://firebase.google.com/docs/reference/js/app.md#initializeapp
  - `getDatabase` --> https://firebase.google.com/docs/reference/js/database.md#getdatabase
  - `ref` --> https://firebase.google.com/docs/reference/js/database.md#ref
  - `set` --> https://firebase.google.com/docs/reference/js/database.md#set

<hr>

## IV. Documentation and Examples
- Get Started with Firebase for Web Apps --> https://firebase.google.com/docs/web/setup
- Firebase Realtime Database --> https://firebase.google.com/docs/database/
- Firebase Realtime Database - Installation & Setup in JavaScript --> https://firebase.google.com/docs/database/web/start
- Methods: 
  - `initializeApp()` --> https://firebase.google.com/docs/reference/js/app.md#initializeapp
  - `getDatabase` --> https://firebase.google.com/docs/reference/js/database.md#getdatabase
  - `ref` --> https://firebase.google.com/docs/reference/js/database.md#ref
  - `set` --> https://firebase.google.com/docs/reference/js/database.md#set
- Firebase Web Samples --> https://firebase.google.com/docs/samples/#web


<hr><hr>

**[Next Chapter -> Firebase Part II - High Score App](firebase-2.md)**
