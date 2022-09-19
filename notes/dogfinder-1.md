# Dogfinder App - Part I

## I. Overview

- In this series we are going to be building a "dog finder" app, which will allow the user to view and favorite various dog pictures
- This will be a good starting point for your project 1

## II. API
 
- This API is about as "developer friendly" as they get:
  - there's no API key required
  - it only has a few endpoints
  - the returned JSON is easy to parse, with only 2 top level keys:  `"message"` and ``"status"``
- API Docs at: https://dog.ceo/dog-api/
- Random image - all breeds: https://dog.ceo/api/breeds/image/random
- Random Image - specific breed: https://dog.ceo/api/breed/affenpinscher/images/random
- List of all breeds - https://dog.ceo/api/breeds/list/all

## III. Start code

- Your start files are **home.html** and **index.js** from [HW - Bulma I - Intro to Bulma](https://github.com/tonethar/IGME-330-Master/blob/master/notes/HW-bulma-1.md)
  - if you didn't complete that assignment - head there now to work on it!
- verify that the hamburger menu functions:
  - re-size the window to less than 1024px wide to see the hamburger menu
  - clicking on the hamburger icon should toggle the visibility of the navigation menu 
    - if it doesn't work, then check the console
    - you can also debug your code - add a breakpoint to the **index.js** code 
    
    
## IV. Get started - set up the site and navigation

1) Put **home.html** and **index.js** in a folder named ***lastname*-p1-starter** (where *lastname* is your actual last name)

2) Change the contents of the `<title>` tag (up in the `<head>` section) to "DogFinder" (without the quotes) 

3) In the "navbar brand" change the font awesome icon from `fa-hotdog` to `fa-dog`

4) We want to change the background color of the hero to blue - modify `<div class="hero is-large is-primary p-2">` to `<div class="hero is-large is-info p-2">`

5) Add `<!DOCTYPE html>` to the top of **home.html** (so that the page will validate properly)

- now head to https://validator.w3.org/ and be sure that **home.html** validates

6) Duplicate **home.html** 3 times and name the copies:

- **app.html**
- **favorites.html**
- **documentation.html**

6) Now change the contents of each page's `<title>` tag to read "Dogfinder Home", "Dogfinder App" and so on

8) Now change the "hero" on the **home.html** page to read "Dogfinder Home" and "Your first stop for cute dog photos!"

9) Now change the "footer" on the **home.html** page to display your actual RIT email address

10) Now add "you are here" cues to the navigation systems for all 4 pages:

- In the **home.html** file, in the navbar, add the `has-text-weight-bold` Bulma class right after the `navbar-item` class
  - Test it - the "Home" text should now be **bold**
- Now head to the **app.html** file, and in the navbar:
  - add `href="home.html"` to the "Home" link so that it functions, and `is-hoverable` to its class attribute
  - delete `href="app.html"` from the "App" link
  - in the "App" link `class` attribute, replace `is-hoverable` with `has-text-weight-bold`
  - Test it - you should be able to click on the "Home" and "App" links in the menubar, and switch back and forth between the pages, where the text of the current page is bold and "not clickable"
- get the **favorites.html** and **documentation.html** pages functioning the same way
  - now all the pages should function as described above

11) In **app.html**, replace the entire "columns" div (which is all the HTML below the `<nav>` area) with:


```html

```

12) Put a `<style>` tag at the top of **app.html** - here it is for your copy/paste pleasure:

```html
<style>
  select#field-limit{
    width:2.5rem;
  }
  h2.subtitle{
    font-family:'Underdog',sans-serif;
  }
</style>
```

13) Now create a **styles/** folder and put a file named **default-styles.css** in it - it will look like this:

```css
@import url('https://fonts.googleapis.com/css2?family=Underdog&display=swap');

ol{
  list-style-position: inside;
}
```

14) Add a `<link>` tag to the `<head>` section of **app.html** that links to this stylesheet


15) In **favorites.html**, `<link>` to the default stylesheet, and replace the entire "columns" div with:

```html
<!-- Main Page -->
<main class="px-1 py-1">
  <div class="has-background-info mr-1 p-1"> 
    <div class="is-large p-4">
      <!-- Row #1 -->
      <div class="title has-text-light">Dogfinder Favorites</div>
      
      <!-- Row #2  -->
      <div class="box mt-2">
        <h2 class="subtitle has-text-weight-bold mb-0">Instructions</h2>
        <ol>
          <li>Checkout your favorite dog photos below!</li>
        </ol>
      </div>

      <!-- Row #3 -->
      <div class="box has-background-info-dark"> 
        <div class="is-large p-1">
          <p id="element-status" class="has-text-warning mb-2">No favorites yet</p>
          <div id="element-card-holder">
            <!-- Favorites go here! -->
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
```

16) In **documentation.html**, `<link>` to the default stylesheet, and replace the entire "columns" div with:


```html
<!-- Main Page -->
<main class="px-1 py-1">
  <div class="has-background-info mr-1 p-1"> 
    <div class="is-large p-4">
      <!-- Row #1 -->
      <div class="title has-text-light">Dogfinder Documentation</div>
      
      <!-- Row #2  -->
      <div class="box mt-2">
        <h2 class="subtitle has-text-weight-bold mb-0">Resources</h2>
        <ol>
          <li>Link #1</li>
          <li>Link #2</li>
        </ol>
      </div>
    </div>
  </div>
</main>
```


17) When you are done, it will look like this:


![screenshot](_images/df-1.png)
    
  




 


