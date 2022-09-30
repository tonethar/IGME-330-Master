# Dogfinder App - Part III

- Overview: Let's improve the app page by creating "cards" for our results, and improving the styling


## I. Improve the `XHR` Error handling

- Problem: If the dog API server is down, or the user's browser is offline, the `xhr.onerror` handler will fire:
  - right now, that error handler is updating the UI with a message, but it's not turning off the button "spinner" 
  - to see this issue in action, change the beginning of the `baseURL` constant (in **app.js**) from `https` to `htt` - then do a search. Check the console to see the error message, and also note that the button spinner never turns off.
  - let's fix that!
  - Head to **ajax.js** and make the `xhr.onerror` handler look like this:
  
  
  ```js
  xhr.onerror = (evt) => {
    console.log(`ERROR: ${evt}`);
    callback(evt);
  };
  ``` 
  
  
  - also, head to **app.js**, and at the end of the `showResults()` `catch{}` block, add a `return` statement so that we bail out of the function after catching the error (can't believe I forgot that one)
  - click the button (keeping `baseURL` malformed) and you should now see "There was some kind of error!" printed in the console, and that the button "spinner" effect has been removed
  - make sure the app still works! Change the beginning of `baseURL` back to `https` and then click the search button - the app should function correctly as before
  
 <hr>
    
## II. Get the "limit" control working

- Most APIs have a `limit` parameter that indicates the maximum number of results you want returned
  - Fun Fact: why not name this `max` or `num` or ? The limit term actually comes from SQL - in this case the `LIMIT` clause - https://www.w3schools.com/mysql/mysql_limit.asp
  - Another Fun Fact: most APIs accept the limit parameter in the URLs' *query string* like this `music-service.php?band=rush&limit=5`
  - But the Dog API we have chosen uses a style called [RESTful](https://www.tutorialspoint.com/restful/restful_introduction.htm) - where the parameters like term and limit are part of the URL. After doing a search, take a look in the console at the URL we are downloading, note how the `breed` and limit are part of the URL, and that there isn't a query string
  - Now let's get to it!
  
  1) Make sure that `limitParam` is set to a value of `"1"`
  
  ```js
  let limitParam = "1";
  ```
  
  
  2) We need to initialize the `onchange` event for the "limit" control. Add the following code to the **app.js** `init()` function:
  
  ```js
  fieldLimit.onchange = (evt) => {
    limitParam = evt.target.value;
  };
  ```
  
  3) Now choose 5 on the limit control and click search - you should get 5 results back.
  
  - BTW - this was so easy to do because the `dogURL()` function handles the updating of the url with the new limit value for us
  
  <hr>
  
  ## III. Improving the look of our results with a *card*
  
  - coming soon ...
   
  
	
  
