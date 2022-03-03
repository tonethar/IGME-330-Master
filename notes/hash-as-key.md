# Creating unique and repeatable keys by *hashing*


## I. A problem that needs to be solved

1) In our *Web App of Awesomeness* project, when a user first "favorites" a web service result, it will be sent to the cloud (Firebase's Realtime database in this case) and stored under a unique *path*. The `likes` property of that result will also be initialized at a value of `1`
  - a [Path](https://firebase.google.com/docs/reference/rules/rules.Path) in Firebase is "Directory-like pattern for the location of a resource" 
  - examples of paths include `users/abc1234` and `dog-favorites/dog-1` 
  - you can kind of think of a Firebase path of being composed of a "folder name" (ex. `users/` and `dog-favorites/` above) and a "unique key" (`abc1234` and `dog1` above)
  - but you might have noted that `dog1` doesn't seem very *unique*, and thus might not be a good *key*, and you would be 100% right about that

2) In our Web App project, any time that any another user favorites the same web service result, we want to increase the `likes` property value by `1`
  - but if one user favorites a particular Poodle, and the app assigns an arbitrary key of `dog11` (because this is the user's 11th favorite), and sends it off to Firebase ...
  - and then later on another user located somewhere else in the world favorites the same Poodle, this time with a key of `dog99` (because the same dog is the user's 99th favorite), and sends it off to Firebase ...
  - we'll end up with duplicate records on Firebase - two different keys - each with a `likes` count of `1` ...
  - rather than what we want, which is ONE Poodle record on Firebase, with a `likes` count of 2

<hr>


## II. Solution - the first time we favorite a web service, assign a unique (and repeatable) *key*

1) For your particular application, depending on the web service, this could be quite simple to solve. Many web services assign unique identifiers to each individual web service result. For example, the Giphy API has a unique identifier for each GIF named (wait for it) ... `id`!

```
{
  "data": [
    {
      "type": "gif",
      "id": "H4DjXQXamtTiIuCcRU",
      "url": "https://giphy.com/gifs/cats-cute-cat-catception-H4DjXQXamtTiIuCcRU",
      ...
    },
    {
    "type": "gif",
      "id": "9gISqB3tncMmY",
      "url": "https://giphy.com/gifs/cat-star-wars-9gISqB3tncMmY",
     ... and so on
```

- If your web service has an attribute named `id` or `guid` or something like that, you can probably send that over to Firebase as the *key* for each result
- This will work because the web service will return the same `id` for a particular cat GIF, no matter which user favorites that cat.
- Thus the key will be the same (repeat) for a particular GIF, no matter which user does the searching and favoriting

<hr>

## III. What if your web service does not provide a unique and/or repeatable key? 

- One solution is to create your own unique key with a *hashing* function
- Hashing was briefly discussed in IGME-106 - see slide #17 of this [Dictionaries](https://github.com/tonethar/IGME-330-Master/blob/master/presentations/Dictionaries.pdf) presentation:
  - "Hashing is the process of converting a string into a key that represents the original string"
  - A very simple hashing algorithm would be to add the ASCI key codes of all of the letters of a string together
  - Problem: "I am Lord Voldemort" gives the SAME hash as "Tom Marvolo Riddle " (because they are anagrams)
 - A good hashing algorithm needs to have the following characteristics:
   - It must be *deterministic* - meaning that when given a specific string of characters, it will always return the same result
   - It should minimize duplication of output values (called "collisions")
   - It is desirable that the output of a hash function have fixed size - we'll limit ours to 32-bit `+/- 2,147,483,647`
 - Although there are a lot of server-side JS implementations of common crytography (hashing) algorithms such as `sha1` or `md5`, there are not any that are implemented natively in the browser, so we'll need to write our own.

<hr>

## IV. Sample Code

**hashing.html**

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hashing</title>
  <script>
  // BAD - because we are just adding together the character codes,
  // the same letters, but in different order, give us the same key!
  // also, our hash length is variable depending on the length of the string
  const badHashCode = (str) => {
    let hash = 0;
    if (str.length == 0) {
        return hash;
    }
    for (let i = 0; i < str.length; i++) {
        let char = str.charCodeAt(i);
        hash += char;
    }
    return hash;
  }

  // Better - the hashes are all the same length and
  // and different letter order gives different results
  // Why multiply times 31?
  // https://stackoverflow.com/questions/299304/why-does-javas-hashcode-in-string-use-31-as-a-multiplier
  const hashCode = (str) => {
    let hash = 0;
    if (str.length == 0) {
        return hash;
    }
    for (let i = 0; i < str.length; i++) {
        let char = str.charCodeAt(i);
        hash = hash * 31 + char;
    }
    return hash;
  }

  // Here is the one-liner of the above code - it does the same thing
  // and is a little bit faster due to the bitshifting instead of multiplication
  // https://stackoverflow.com/questions/51960331/why-5-bit-left-shift-in-hashing-function
  const hashCode2 = (str) => {
    return str.split("").reduce((prevHash, currVal) => (((prevHash << 5) - prevHash) + currVal.charCodeAt(0)) | 0, 0);
  };


  console.log(`badHashCode("tony") = '${badHashCode("tony")}'`);
  console.log(`badHashCode("ynot") = '${badHashCode("ynot")}'`);
  console.log(`badHashCode("I am Lord Voldemort") = '${badHashCode("I am Lord Voldemort")}'`);
  console.log(`badHashCode("Tom Marvolo Riddle ") = '${badHashCode("Tom Marvolo Riddle ")}'`);
  console.log(`hashCode("") = '${hashCode("")}'`);
  console.log(`hashCode2("") = '${hashCode2("")}'`);
  console.log(`hashCode("TJ") = '${hashCode("TJ")}'`);
  console.log(`hashCode2("JT") = '${hashCode2("JT")}'`);
  console.log(`hashCode("tony") = '${hashCode("tony")}'`);
  console.log(`hashCode2("tony") = '${hashCode2("tony")}'`);
  console.log(`hashCode("ynot") = '${hashCode("ynot")}'`);
  console.log(`hashCode2("ynot") = '${hashCode2("ynot")}'`);
  console.log(`hashCode("andy") = '${hashCode("andy")}'`);
  console.log(`hashCode2("andy") = '${hashCode2("andy")}'`);
  console.log(`hashCode2("https://www.rit.edu/experiential-learning") = '${hashCode2("https://www.rit.edu/experiential-learning")}'`);
  console.log(`hashCode2("https://www.amazon.com/Cookin-Coolio-Star-Meals-Price/dp/1439117616/") = '${hashCode2("https://www.amazon.com/Cookin-Coolio-Star-Meals-Price/dp/1439117616/")}'`);
  </script>
</head>
<body></body>
</html>
```

<hr>

## V. Tips & Resources

- If you end up using a hashing algorithm to generate a unique key for a resource, you may want to add a prefix - maybe your project's "initials" to the beginning of the hash. That way the key is not numeric, because if you are storing these keys in localStorage, numeric object keys can look like array indexes, which could cause problems with `JSON.parse()` or `JSON.stringify()`
- If you are looking for a very low chance of collisions, here are some links to some JavaScript implementations of `sha1`, `sha256`, and `md5` - on this page - https://stackoverflow.com/questions/6122571/simple-non-secure-hash-function-for-javascript
- More:
  - https://stackoverflow.com/questions/7616461/generate-a-hash-from-string-in-javascript
  - https://stackoverflow.com/questions/194846/is-there-any-kind-of-hash-code-function-in-javascript

