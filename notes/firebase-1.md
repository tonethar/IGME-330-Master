# 1 - Intro to Firebase 

- Here we will look at setting up a Firebase *Realtime Database*

## I. Overview
- About Firebase
- https://console.firebase.google.com


## II. Setting up a *Realtime Database*


### II-A. Create a new project

- Head to https://console.firebase.google.com/ and click the *Add Project* button, this will create a pop-up window where you will name your project

![screenshot](_images/firebase-1.jpg)


### II-B. Name the project

- Name the project **high-scores** and click the **Create Project** button

![screenshot](_images/firebase-2.jpg)

### II-C. Add a *Firebase for Web* App to your project

- You should now be on the **Project Overview** screen
- Click on the *Firebase for Web* button on the right
- This creates a new web app for this project. Note that there are other options for creating Androif and iOS Apps. The idea here is that the project will have one set of data, and you could have multiple apps (web, Android, iOS) that SHARE this data

![screenshot](_images/firebase-3.jpg)

### II-D. Copy the code snippet

- A pop-up window will appear that contains the JavaScript set-up code you will need to enable Firebase on a web page
- Go ahead and create an HTML file named **firebase-test.html** and copy/paste this JS code into the &lt;head> section of the document

![screenshot](_images/firebase-4.jpg)

### II-E. Create a Realtime Database

- After you have copied the code, close the pop-up window
- To change to the *Database* screen, click on the **Database** tab on the left 
- Then scroll down the page, and stop at the **Or choose Realtime Database** heading
- Click the **Create Database** button, which will open a pop-up window

![screenshot](_images/firebase-5.jpg)


### II-F. Set the security rules for your database

- Choose **Start in test mode**
- Click the **Enable** Button
- You can modify these rules later under the "Rules" tab

![screenshot](_images/firebase-6.jpg)


### II-G. Verify

- You should now have created an empty *Realtime Database*

![screenshot](_images/firebase-7.jpg)


### II-H. Test your Realtime Database
- Write code in **firebase-test.html** to write some values to your database
- add the following to the &lt;script> tag, right after the code that you previously copy/pasted:

```js
  console.log(firebase); // verify that firebase is loaded
  
  // #1 - get a reference to the databse
  let database = firebase.database();
  
  // #2 - refer to a root node named `scores`
  let ref = database.ref('scores');
 
 // #3 - create some data
  let data = {
  	name:"Mad Max",
  	score:99999
  };
  
  // #4 - send data!
  ref.push(data);
```

### II-I. See the changes!

- Head back to your high-scores database, you should see the high score has been posted
- If you reload your HTML, the data will be posted multiple times, each time with a unique UUID

![screenshot](_images/firebase-8.jpg)


## III. Wrap up

<hr><hr>

**[Next Chapter -> Firebase Part II - High Score App](firebase-2.md)**
