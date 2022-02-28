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

- If your web service has an attribute named `id` or `guid` or something like that, you can probably send that over to Firebase as the key
- This will work because the web service will return the same `id` for a particular cat GIF, no matter which user favorites that cat.
- Thus the key will repeat

<hr>

## III. What if your web service does not provide a unique and/or repeatable key? 

- One solution is to create your own key with a *hashing* function
- Hashing was briefly discussed in IGME-106 - see slide #17 of this [Dictionaries](https://github.com/tonethar/IGME-330-Master/blob/master/presentations/Dictionaries.pdf) presentation:
  - 
