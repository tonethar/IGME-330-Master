# 5 - Firebase - *deleting* elements from the cloud

## I. `remove()` - the *D* in CRUD
- You will use the `remove()` function to delete resources - it is documented here - https://firebase.google.com/docs/database/web/read-and-write
- You will need to `import remove` just like you imported `ref`/`set`/`push` etc before you were able to use them
- The (simplest) syntax looks like this - `remove(ref)`
- You can also delete by specifying `null` as the value for another write operation such as `set()` or `update()`
  - you can use this technique with `update()` to delete multiple children in a single API call

<hr>

## II. Creating an "admin" folder

- Suppose you wanted to create an "administrator" page - where a user (like you) that was logged in could edit and delete Firebase records
- Creaing login pages/user names/passwords usually involves server-side programming and the creation of session variables - which goes beyond the scope of this course
- The simplest way to create a protected admin folder on banjo is to use `.htaccess` files and RIT's 



<hr><hr>

**[Previous Chapter <- Firebase Part IV - Creating a `likes` counter for Dog names](firebase-4.md)**
