# Hashes as keys


## I. A problem that needs to be solved

- In our *Web App of Awesomeness* project, when a user first "favorites" a web service result it will be sent to the cloud (Firebase's Realtime database in this case) and stored under a unique *path*. The `likes` property of the result will also be initialized at a value of `1`
  - a [Path](https://firebase.google.com/docs/reference/rules/rules.Path) in Firebase is "Directory-like pattern for the location of a resource" 
  - examples of paths include `users/abc1234` and `dog-favorites/dog-1` 
  - you can kind of think of a Firebase path of being composed of a "folder name" (ex. `users/` and `dog-favorites/` above) and a "unique key" (`abc1234` and `dog1` above)
  - but you might have noted that `dog1` doesn't seem very *unique*, and thus might not be a good *key*, and you would be 100% right about that
- In our Web App project, any time that any another user favorites the same web service result, we want to increase the `likes` property value by `1`

- *Hashing* was briefly discussed in IGME-106 - see slide #17 of this [Dictionaries](https://github.com/tonethar/IGME-330-Master/blob/master/presentations/Dictionaries.pdf) presentation
