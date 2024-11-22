# React Amiibo App

## I. Overview
- Let's see how we can build a React app that consumes a web service
  - we will get more practice with components ...
  - and with React's *"Reactivity"* - meaning *data binding* ...
  - and with 2 of the 3 "core" React hooks:
    - [`useState()`](https://react.dev/reference/react/useState)
      - [State: A Component's Memory](https://react.dev/learn/state-a-components-memory)
    - [`useEffect()`](https://react.dev/reference/react/useEffect)
      - [Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
      - [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)
    - [`useContext()`](https://react.dev/reference/react/useContext)
      - [Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)
  - we will also utilize the [`useMemo`](https://react.dev/reference/react/useMemo) React hook to *cache* a value
- BTW - *You already have some familiarity with React, right?*
  - if not, see the [Intro to React](react-intro.md) notes, especially [Part VI. Creating a "Todo" app with React and Vite](react-intro.md#vi-creating-a-todo-app-with-react-and-vite)
  
---

## II. Amiibo API

- Docs: https://amiiboapi.com/docs/
- Playground: https://amiiboapi.com/
- Sample call: https://www.amiiboapi.com/api/amiibo/?name=mario

---

## III. Get Started

- Create folder named **amiibo-app** and `cd` into it
- Type: `npm create vite@latest`
  - for *Project name*: **type a period** (`.`) to create a project in current **amiibo-app** folder
  - for *Framework*: choose **React**
  - for *Variant*: choose **JavaScript**
- `npm i`
- `npm run dev`
- Head to localhost to see app running in browser
- Get rid of some of the unneeded web files, but keep:
  - **App.jsx**
  - **App.css**
  - **index.html**
    - change the `<title></title>` to "Amiibo Finder"
  - **index.css**
    - to get rid of the vertical centering, comment out or delete `min-height: 100vh;`
  - **main.jsx**
- Make **App.jsx** look like this:

```jsx
import { useState } from "react";
import './App.css'

const App = () => {
  return <>
    <header>
      <h1>Amiibo Finder</h1>
    </header>
    <hr />
    <main>
      <button>Search</button>
      <label>
        Name: 
        <input />
      </label>
    </main>
    <hr />
    <footer>
      <p>&copy; 2023 Ace Coder</p>
    </footer>
  </>;
};

export default App;
```

- View the app in the web browser to be sure it compiles - see below:

---

![screenshot](_images/_react/amiibo-react-app-0.png)
  
---

## IV. Create an XHR helper function

- In **App.jsx**, *above* the `App` component, declare this constant

```js
// app "globals" and utils
const baseurl = "https://www.amiiboapi.com/api/amiibo/?name=";
```

- And implement the `loadXHR()` helper function

```js
const loadXHR = (url, callback) => {
  // set up the connection
  // when the data loads, invoke the callback function and pass it the `xhr` object
};
```

- And here's `searchAmiibo()` - all done:

```
const searchAmiibo = (name, callback) => {
  loadXHR( `${baseurl}${name}`, callback);
};
```

---

## V. Create a callback function

- To test our `searchAmiibo(name, callback)` helper function, let's write a callback function that will be invoked when the amiibo data has downloaded:

```js
 const parseAmiiboResult = xhr => {
    // get the `.responseText` string
   
    // declare a json variable
   
    // try to parse the string into a json object
    
    // log out number of results (length of `json.amiibo`)
    console.log(`Number of results=${json.amiibo.length}`);
    
    // loop through `json.amiibo` and log out the character name
  };
```

---

## VI. Test it

- Now everything should work, check the console to be sure
- Try substituting "luigi", "peach" and "rit" to see what you get back

```js
  // call searchAmiibo() with "mario" and our callback function
  searchAmiibo("mario", parseAmiiboResult); // DONE
```

--- 

## VII. Hook the code up to the UI

- Goal: When we click the button, we want to see the web service results of the typed in search term (character name)
- 1 - We will need a `useState()` call for `term`
  - need to bind the `<input>` `.value` to `term`
  - need to update `term` whenever `.value` changes
- 2 - We need to get button clicking working (fire up `xhr` and download the amiibo data)
  - use `onClick={...}` and wrap the call to `searchAmiibo()` into an arrow function
- 3 - We will need a `useState()` call for `results` (an array of object literals)
  - set the initial value to an empty array - `[]`
- 4 - We need to display the `results`

```jsx
      {results.map(amiibo => (
        <span key={amiibo.head + amiibo.tail} style={{color:"green"}}>
          <h4>{amiibo.name}</h4>
          <img 
            width="100" 
            alt={amiibo.character}
            src={amiibo.image}
          />
        </span>
      ))}
```

- Note the React need for a unique `key` when producing lists like this
- Also note the syntax for the use of an inline `style`
  - but, using a `class` and the `className` attribute for styling is generally preferred in React!

---
  
- Next, we need to update `results` when the amiibo data has loaded
  - move `parseAmiiboResult(xhr)` into the `App` component and make a small addition
- When you are done, you should have a functioning app:

---

![screenshot](_images/_react/amiibo-react-app-1.png)

---

- Now go ahead and move `const searchAmiibo = (name, callback)...` into the `App component`
- Also delete all of the `console.log()` calls - except for the one that's in the `catch` block

---

## VIII. A little refactoring - ajax.js - a "plain old JS" file

- Go ahead and create a file in the **src** folder named **ajax.js**
  - move `const loadXHR = (url, callback) =>...` into it and `export` it
  - now `import` it into **App.jsx** - `import { loadXHR } from "./ajax";`
    - note that we don't need the file extension for the file when we `import` it
  - test the app, it should work as before
  - now the only "global" you have left in **App.jsx** is `const baseurl =...`
 
---

## IX. storage.js
- We are going to utilize `window.localStorage` to save the current search term, so that when the user leaves the app (closes the window, quits the browser, restarts the computer etc), and then later returns, that search term will still be in the `<input>` as if they never left
- Create a new file named **src/storage.js** - and make it look like this:

```js
const storeName = "abc1234-amiibo-app";

const loadJSONFromLocalStorage = () => {
  const string = localStorage.getItem(storeName);
  let json;
  try{
    json = JSON.parse(string);
    if(!json) throw new Error("json is null!");
  }catch(error){
    console.log(`ERROR: ${error} with string: ${string}`);
    json = {};
  }
  return json;
};

export const writeToLocalStorage = (key, value) => {
  console.log(`Calling writeToLocalStorage(${key},${value})`);
  const json = loadJSONFromLocalStorage();
  json[key] = value;
  localStorage.setItem(storeName, JSON.stringify(json));
};

export const readFromLocalStorage = (key) => {
  const json = loadJSONFromLocalStorage();
  console.log(`Calling readFromLocalStorage(${key}) with value=${json[key]}`);
  return json[key];
}
```

- Over in **App.jxs**, `import` it
  - `import { readFromLocalStorage, writeToLocalStorage } from "./storage";`
- N.B. - this code is more than we need to store a single string value, and was deliberately over-engineered so that you could (for example) easily also save an array of search terms (the search *history*), or an array of the most recent amiibo results, or an array of amiibo favorites, etc

---

## X. Utilize storage.js

- We are going to save the search `term` every time the value of `term` changes (which is tied to the `onChange` event handler of the `<input>`)
- We are going to use the `useEffect()` hook to do so
- Go ahead and modify your `react` import to also bring in `useEffect`
  - `import { useEffect, useState } from "react";`
- Add the following code to the `App` component right after the two `useState()` calls

```jsx
useEffect(() => {
  writeToLocalStorage("term", term);
});
```

- `useEffect()` will call the provided function - which saves the value of `term` to local storage - every time the `App` component is re-rendered
- Do a search by clicking the Search button, or type in a different name. Then check `localStorage` in the browser's web inspector (the **Application** tab) to see that the value of `term` is being saved

---

![screenshot](_images/_react/amiibo-react-app-2.png)

---

## XI. Optimization

- Right now `useEffect()` is being called every time the `App` component re-renders (for example, when the Search button is clicked), even if the value of `term` has not changed
  - to make it so that `useEffect()` will only be called when the value of `term` changes, add a *dependencies array* to the end:
 
```jsx
useEffect(() => {
  writeToLocalStorage("term", term);
}, [term]);
```

- Test the app by clicking the Search button and check the console, there should be fewer logs from the storage functions, as they will only be called when `term` changes
  - N.B. In development mode (the mode we are in now), React does some extra re-rendering of components

---

## XII. Load the saved search term and more *optimization* with `useMemo()`

- Now let's load the value of `term` from `localStorage` when the app first loads - go ahead and make the first part of the `App` component look like this:

```jsx
const App = () => {
  const savedTerm = readFromLocalStorage("term") || "";
  const [term, setTerm] = useState(savedTerm);
  const [results, setResults] = useState([]);

  useEffect(() => {
    writeToLocalStorage("term", term);
  }, [term]);

  const parseAmiiboResult = xhr => { ...
```

- We should now see the last search `term` in the `<input>` whenever we reload the web page, or even if we close the window and reopen it
- One problem though - if you check the console you can see that the `savedTerm` code is running too much - every time the component is re-rendered
- To fix this and further optimize our code, we can use another hook [`useMemo`](https://react.dev/reference/react/useMemo) - which *"is a React Hook that lets you cache the result of a calculation between re-renders"*
- Go ahead and change this:

```jsx
const savedTerm = readFromLocalStorage("term") || "";
```

- To this:

```jsx
const savedTerm = useMemo(() => readFromLocalStorage("term") || "", []);
```

- And don't neglect to import `useMemo` at the top of **App.jsx**
- The empty array - `[]` - that is last parameter of `useMemo()` tells React to "only run this code once, when the component first *mounts*"
- Do a search and check the console, there should not be any storage function logs unless we change the search term

---

## XII. Debugging with React Developer Tools

- The console has been giving us helpful React error messages along the way - but there are more powerful developer tools we could use
- Go ahead and install the [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- Now check the Web Inspector - the **Components** tab:

---

![screenshot](_images/_react/amiibo-react-app-3.png)

---

- Above you should see the component hierarchy (just one App component as of now), and the values of the 2 `App` state variables (`term` and `results`) and the value of the single `memo`

---

## XIII. Factor out some code and create separate components

### XIII-A. Footer.jsx

- We'll do the footer together

**src/Footer.jsx**

```jsx
const Footer = ({name, year}) => {
  return <footer>
    <p>&copy; {year} {name}</p>
  </footer>;
};
export default Footer;
```

- Next, `import` it at the top of **App.jsx**
- Finally, replace:

```jsx
<footer>
  <p>&copy; 2023 Ace Coder</p>
</footer>
```

- with:

```jsx
<Footer 
  name="Ace Coder"
  year={new Date().getFullYear()}
/>
```

- Test the app, it should work as before
- If you are getting a ***'name' is missing in props validation*** message, you can either ignore it, use TypeScript, or use the `PropTypes` API
  - to do the latter and tell React what the data types of `name` and `year` are, add the following to **Footer.jsx**:

```jsx
import PropTypes from 'prop-types';

...

Footer.propTypes = {
  name: PropTypes.string.isRequired,
  year: PropTypes.number.isRequired,
}
```

---

### XIII-B. Header.jsx
- Easy!
- Just pass in `title` as a prop!
---

### XIII-C. AmiiboList.jsx
- Easy!
- Keep the "state" in **App.jsx**, and just pass in `results` as a prop

---

### XIII-D. AmiiboSearchUI.jsx
- Easy! (mostly)
- Keep the "state" in **App.jsx**, and just pass in:
  - `term`
  - `setTerm`
  - `searchAmiibo`
  - `parseAmiiboResult`
- as props
- Hint: `PropTypes.func.isRequired` for the 3 functions that are getting passed in

---

**React Web Inspector**

![screenshot](_images/_react/amiibo-react-app-4.png)

---

**App.jsx**

![screenshot](_images/_react/amiibo-react-app-5.png)

---

## XIV. Publish it
- To create a transpiled version (React JSX -&gt; Vanilla JS/HTML that you can put on the web:
  - type ctrl-c to quit `vite`
  - type `npm run build`
  - now you will see the **dist/** folder has been populated with an **index.html** file, a **.js** file and a **.css** file - this is the "transpiled and bundled" version that's ready for distribution
    - you can test it locally by running just this **dist/** folder on Live Server
    - PS - if you put these files on banjo, you'll need to first fix the `href` attributes of the `<script>` and `<link>` tags
      - hint: add a `.` to the beginning of the `src` and `href` urls
- Here's a version running on banjo: https://people.rit.edu/~acjvks/330/fall-2023/react-amiibo.html
  - Be sure to "View Page Source" and "Inspect" the DOM - where's all the JSX?

---

## XV. Discussion
- Decomposing the app UI into distinct *components*
- Discuss difference between the typical DOM apps we've written (e.g. IGME-235 web app, IGME-330's Technobabble) and how a React app works:
  - Code and HTML are no longer separate - there's "inline JS" - which is traditionally frowned on!
  - `document.querySelector()`, `.innerHTML` et al aren't needed very often
- Having a single "source of truth" for each state
  - https://en.wikipedia.org/wiki/Single_source_of_truth
- Sharing state between components by "lifting state up" - https://react.dev/learn/sharing-state-between-components
  - passing functions as parameters - see the `AmiiboSearchUI` component
- *Optimizing* the code with *hooks*
- React Browser Debugger Tools
- Reusable code factored out into regular JS files - e.g. **storage.js** and **ajax.js**

---

## XVI. Anything else?

- This app would benefit from:
  - better CSS/layout - a framework with a `.card` class to display the results would be nice
  - better UI:
    - show a "spinner" when a search is going on, then hide it when the search is complete
    - show the number of results found
    - add tool tips
    - save the contents of the most recent `results` array in `.localStorage`
    - allow users to "favorite" and view previously searched amiibo - and store these in `.localStorage`
    - allow users to "page through" results 5 or 10 at a time
   
---

## XVII. Rubric

- 60% - Get through Part XII. with everything working 
- +10% - get `Footer` working
- +10% - get `Header` working
- +10% - get `AmiiboList` working
- +10% - get `AmiiboSearchUI` working
