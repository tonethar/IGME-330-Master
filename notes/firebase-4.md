# 4 - More Firebase - creating a `likes` counter for Dog names

- ***There is a video of this Firebase demo here --> [Demo - Firebase "Likes" Counter (13:15)](https://rit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=d89db2ea-9682-4aef-bb54-ae46002bf7ec)***

## I. Overview
- What we are going to build is "likes counter" for user submitted dog names
  - every time a user submits a new dog name, it is added to the `favorites/` path, and given a property of `likes: 1`
  - if this dog name already exists in Firebase, the `likes` property of that dog name is incremented by `1`
  - here is a screenshot of the completed example app (on the left), and the Firebase console (on the right)

<hr>

![screenshot](https://github.com/tonethar/IGME-330-Fall-2021/blob/main/_images/gab-dog-1.jpg)

<hr>

## II. Start Code

**gab-dog-1-start.html**

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>GabDog</title>
  <style>
    *{
      font-family: sans-serif;
    }
  </style>
  <script type="module">

// TODO: ADD YOUR imports and Firebase setup code HERE

//

const writeFavNameData = name => {
  const db = getDatabase();
  const favRef = ref(db, 'favorites/' + name);
  set(favRef, {
      name,
      likes: 1
  });
};

const favoritesChanged = (snapshot) => {
  // TODO: clear #favoritesList
  snapshot.forEach(fav => {
    const childKey = fav.key;
    const childData = fav.val();
    console.log(childKey,childData);
    // TODO: update #favoritesList
  });
};

const init = () => {
  const db = getDatabase();
  const favoritesRef = ref(db, 'favorites/');
  onValue(favoritesRef,favoritesChanged);
	
  btnSubmit.onclick = () => {
    writeFavNameData(nameField.value);
  };
};

init();

</script>
</head>
<body>
  <h1>GabDog&trade;</h1>
  <h3>We want to know - what's a good dog name?</h3>
  <p>Name --> <input value="Rover" id="nameField"></p>
  <button id="btnSubmit">Send Name to Server</button>
  <hr>
  <h3>Popular Names</h3>
  <ol id="favoritesList"></ol>
 </body>
</html>
```

<hr>

### III. Notes

**gab-dog-1.html**

#### 1) - Get the basics working

- Add the Firebase/Firebase Realtime Database setup code
- Display the favorite dogs in `#favoritesList` - see screenshot above for an idea of what it should look like - but in this version, we can't record any more "likes" than 1
- The fact we can't increment `likes` on existing dog names is a problem - so let's fix it!

<hr>

#### 2) - Get "`likes ++`" working the "super easy" way

- We'll use the [`ServerValue.increment()`](https://firebase.google.com/docs/reference/kotlin/com/google/firebase/database/ServerValue#increment_1)
- You'll need to `import` this function to use it - add `increment` to your ".../firebase-database.js" import
- Make `writeFavNameData()` look like this - it's only one small change to the code:

```js
const writeFavNameData = name => {
  const db = getDatabase();
  const favRef = ref(db, 'favorites/' + name);
  set(favRef, {
    name,
    likes: increment(1)
  });
};
```

- test it - incrementing `likes` should now work!

<hr>

**gab-dog-2.html**

#### 3) - Get "`likes ++`" working the "harder" way
- This technique will use `get()` and `update()`
- It's not technically needed for this example (because of `increment(1)` above), but this is good to know how to do in case you want to perform updates other than incrementing
- Make a copy of **gab-dog-1.html** and name it **gab-dog-2.html**
- You will need to import `get` and `update` in your ".../firebase-database.js" import
- Here is the new version of `writeFavNameData()` - we will walk though how this code works:

```js
// This is the "harder" way and not necessary for incrementing a counter
// But this code is useful if you want to `get()` a value just once
// and/or do "batch" updates of non-numeric values with `update()`
const writeFavNameData = name => {
  const db = getDatabase();
  const favRef = ref(db, 'favorites/' + name);

  // does it already exist?
  // get will just look once
  get(favRef).then(snapshot => {
    let favorite;
    if (snapshot.exists()) {
      // if it's already in "favorites/" - update the number of likes
      favorite = snapshot.val();
      console.log("found - current values=",favorite);
      const likes = favorite.likes + 1;
      const newData = {
        name,
        likes
      };
      const updates = {};
      updates['favorites/' + name] = newData;
      update(ref(db), updates);
    } else {
      // if it does not exist, add to "mostFavorited/"
      console.log(`No favorite of key='${name}' found`);
      console.log("favorite=",favorite);
      set(favRef, {
        name,
        likes: 1
      });
    }
  }).catch((error) => {
    console.error(error);
  });
}
```


<hr>

### IV. Documentation
- `increment(value)`
  - *Returns a placeholder value that can be used to atomically increment the current database value by the provided delta.*
  - https://firebase.google.com/docs/reference/kotlin/com/google/firebase/database/ServerValue#increment_1
- `get(path)`
   - *Gets the most up-to-date result for this query.*
   - https://firebase.google.com/docs/reference/js/database.md#get
   - returns a *Promise* - remember those?
 - `update(path,values)`
   - *Writes multiple values to the Database at once.*
   - https://firebase.google.com/docs/reference/js/database.md#update
   - returns a *Promise* - remember those?

<hr><hr>


**[Previous Chapter <- Firebase Part III - Highscore Viewer](firebase-3.md)**

**[Next Chapter -> Firebase Part V - Firebase - Deleting elements from the cloud](firebase-5.md)**
