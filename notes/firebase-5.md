# 5 - Firebase - *deleting* elements from the cloud

## I. `remove()` - the *D* in CRUD
- You will use the `remove()` function to delete resources - it is documented here - https://firebase.google.com/docs/database/web/read-and-write
- You will need to `import remove` just like you imported `ref`/`set`/`push` etc before you were able to use them
- The (simplest) syntax looks like this - `remove(ref)`
- You can also delete by specifying `null` as the value for another write operation such as `set()` or `update()`
  - you can use this technique with `update()` to delete multiple children in a single API call

<hr>

## II. But first, creating an "admin" folder

- Suppose you wanted to create an "administrator" page - where a user (like you) that was logged in could edit and delete Firebase records
- Creating login pages/user names/passwords usually involves server-side programming and the creation of session variables - which goes beyond the scope of this course
- The simplest way to create a protected **admin/** folder on banjo is to use `.htaccess` files and RIT's single sign on authentication system - then you can specify exactly which banjo users have have access to your **admin/** folder
  - RIT's banjo documentation for this is here: https://rit.edu/webdev/authenticating-and-authorizing-rit-users
- Here is a walkthrough:

1) On banjo, somewhere in `www/` or one of its sub-directories, create a folder named **admin**

2) Create a `.htaccess` file inside of **admin** and add the following to it (replacing `abc1234` and `xyz9876` with the user ids you'd like to give permission too)

```
ShibRedirectToSSL 443
AuthType shibboleth
ShibRequireSession on
require user abc1234 xyz9876
```

- ***BTW - if you need a reminder-up on what `.htaccess` files are, here are the relevant IGME-235 notes- https://github.com/tonethar/IGME-235-Shared/blob/master/hw/htaccess.md***


3) Now banjo will only let authorized users who are logged in to access to the **admin** folder

- Test this by by creating a **New Incognito Window** (Chrome) or **New Private Window** (Firefox) and then pointing this window at the **admin/** folder
- Because you are not logged into RIT in this Private Window,  you should be prompted to login - **RIT Login -  Login to people.rit.edu**
- Type in an ***incorrect*** username/password - you should see an error message and then be unable to view the **login/** folder
- Type in the ***correct*** username/password - now you should be able to log in and view the **login/** folder
- Now close the Private Window and open a regular browser window. Most likely you are already logged into RIT, so you should be able to view the **login/** folder (which is currently empty, BTW, other than the "invisible" **.htaccess file**

<hr>

## III. Creating an admin.html file

<hr><hr>

**[Previous Chapter <- Firebase Part IV - Creating a `likes` counter for Dog names](firebase-4.md)**
