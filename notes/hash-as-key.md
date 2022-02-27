# Hashes as keys


## I. A problem that needs to be solved

- In our *Web App of Awesomeness* project, when a user first "favorites" a web service result it will be sent to the cloud (Firebase's Realtime database in this case) and stored under a unique *path*
  - a [Path](https://firebase.google.com/docs/reference/rules/rules.Path) in Firebase is "Directory-like pattern for the location of a resource" 
  - examples of paths include `users/abc1234` and `dog-favorites/dog-1` (the second example isn't a very good path, which we will discuss below)
- In our Web APp project, any time that another user favorites the same web service result, we want to increases the likes counter 
