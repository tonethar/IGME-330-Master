# Homework - Improved GIF Finder

- A really nice feature that all web apps have is ability to allow the user to "page" through large numbers of results
- Unfortunately, in our current version of [GIF Finder](https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md), did you notice that we always get the same 25 "cat" GIFs back when we search? Let's fix that!

## Your Mission
- First, review the [GIF Finder](https://github.com/tonethar/IGME-230-Master/blob/master/notes/HW-gif-finder.md) assignment from IGME-230 - and you may just want to re-create it from scratch to refresh your memory of how it works
- Add a "Find More!" button to your GIF Finder HW - here are some hints:
  - the `offset` API parameter is what controls the "start index" of the results. Because we have not supplied a value for this, it always defaults to `0` - see screenshot below:
  
 ![screenshot](./_images/improved-gif-finder/webservice-demo-3.png)
  
- so we need to pass an `offset` parameter to the query string, and increase the `offset` every time the "Find More!"  is clicked - hints:
  - Declare a script variable - `let offset = 0;`
  - Append its value to the query string  - `url += "&offset=" + offset;`
  - Increase the value of `offset` by the `limit` value every time the "Find More!" button is clicked, and then do a search
  - Re-set the value of `offset` to `0` every time the "Find some GIFs!" button is clicked
  - `e.target.id` is a good way to figure out which button called `searchButtonClicked()`
  - Display the `offset` value somewhere on the screen (see the screenshot)
  - "Gotchas":
    - when you pull the `limit` value from the form, it is of type `String`. Before you can perform mathematical operations with it, you will need to convert it to a `Number`
    - you should probably set the `disabled` property of the "Find More!" to `true` when the app starts up, and then set it to `false` after the first successful search
  - Here is a completed example:   
    
![screenshot](./_images/improved-gif-finder/webservice-demo-4.png)
