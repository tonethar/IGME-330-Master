# Intro to React

---

## I. Overview
- React - *The library for web and native user interfaces*
- Home page:  https://react.dev/
- Thinking in React (Components, state, state flow): https://react.dev/learn/thinking-in-react
- https://react.dev/learn
  
---

## II. React playground

- React Code Sandbox to play in: https://react.new
- Let's try it out!
- Function components are pretty simple - they return a string of JSX (similar to HTML) that React will then render into "vanilla" HTML
- Let's create 2 new components:
  - a `Smiley` component that takes no parameters
  - a `Message` component that takes a `props` parameter with a `text` property

---

## III. React in the browser
- React's JSX component syntax will not run in the browser directly, and first needs to be transpiled into plain-old HTML
- The simplest way to do this is to let the browser do the transpiling for us by importing React and Babel libraries from a CDN
- ***Note: While this way is the simplest way to get started with React, it's not appropriate for production code, and it is unlikely that this approach will be supported in the long-term***
- React CDN Links:
  - https://legacy.reactjs.org/docs/cdn-links.html
- Babel CDN Links - `babel-standalone` - a build of Babel for use in non-Node.js environments:
  - https://babeljs.io/docs/babel-standalone
  - https://cdnjs.com/libraries/babel-standalone
- Let's try out some more React (rendering lists, displaying images) with this code:
- Challenges:
  - add a `text` attribute to the `Header` component (similar to how `Footer` does it)
  - *destructure* the `props` parameter of `Footer` into `year` and `name` parameters
  - create an `Image` component (for the tiger image) and give it `src`, `altText` and `height` attributes
  - create a `List` component with a `data` attribute
 
**react-cdn.html**

```html
  <!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.2/babel.js" integrity="sha512-o1yFsi2kuKpw+gYcRZ2wqM+nolBeFrGEZCBsroxwbw9jZhFsacJSWCphWzApZ0x7ZKQJLTaook5vyJdBFUmumw==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <style>
      body{
        font-family: sans-serif;
      }
      footer{
        color: darkgray;
      }
    </style>
    <title>React starter with a CDN</title>
  </head>
  <body>
    <!-- We will render the `App` component here -->
    <div id="root"></div>

    <!-- Note `type="text/babel"` -->
    <script type="text/babel">
      
      // `Header` component
      // Simple "one liner" function component that returns a <header>
      const Header = () =>  <header><h1>Famous Tigers</h1></header>;
    
      // `Footer` component
      // This utilizes a `year` attribute that is passed in when the component is created
      // note the explicit `return` and the required use of parens to "wrap" the JSX
      const Footer = props => {
        return (
          <footer>
            <p>&copy; {props.year} {props.name}</p>
          </footer>
        );
      };

      // `Main` component
      // Note the required `key` attribute added to the `<li>` elements below
      // https://react.dev/learn/rendering-lists#keeping-list-items-in-order-with-key
      const Main = props => {
        return (
          <main>
            <img
              height={150}
              src={props.url}
              alt="ROAR!!"
            />
            <ul>
              {props.tigerObjects.map((obj) => (
                <li key={obj.id}>
                  {obj.title}
                </li>
              ))}
            </ul>
          </main>
        );
      };

      // Some data
      const imageURL = "https://www.rit.edu/marketing/brandportal/images/1505/brand-elements/identity/3-color-white.png";
      
     // https://en.wikipedia.org/wiki/List_of_fictional_big_cats_in_animation
      const tigerNames = [
        "Aslan",
        "Battle Cat",
        "Cringer",
        "Mufasa",
        "Nala",
        "Snagglepuss"
      ];

      // Associate an `id` with each tiger name
      // which React needs for a `key` value when rendering a list 
      // FYI - https://dev.to/shiv1998/why-not-to-use-index-as-key-in-react-lists-practical-example-3e66
      const tigerObjects = tigerNames.map(
        (name, index) => ({
          id: index,
          title: name
        })
      );

      // `App` component
      // App will contain all of the other components
      // `<>` is used as a generic "wrapper" for all the elements - https://react.dev/reference/react/Fragment
      // The attribute values we pass into each component show up in the 
      // `props` parameter of each component, as properties of the `props` object
      const App = () => {
        return (
          <>
            <Header />
            <Main
              tigerObjects={tigerObjects}
              url={imageURL}
            />
            <Footer
              year={new Date().getFullYear()}
              name="Ace Coder"
            />
          </>
        );
      };

      // Finally, render the `App` component and inject the HTML into #root
      // Newer way: 
      // - https://react.dev/reference/react-dom/client/createRoot
      // - https://react.dev/reference/react-dom/client/createRoot#root-render
      // Older way:
      // - https://legacy.reactjs.org/docs/react-dom.html#render

      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
  </body>
</html>
```

---
  
## IV. Production React - Transpiling the React using `npm`, react, webpack and so on

- You can `npm i` the react, webpack, babel packages ...
- You'd also need to create a buncha config files ...
  - ... and do a lot of googling to figure out the proper settings ..
- Here's an (out of date) example - so just look, don't try:
  - https://www.tutorialspoint.com/reactjs/reactjs_environment_setup.htm
- NB: in IGME-430 we usually build our "toolchains" like this, from scratch 
- Let's move on ...
  
---

## V. Bootstrapping a React project the easy way

- The two most popular ways to quickly and easily create React apps are:
  -  `create-react-app` - https://create-react-app.dev/
  -  Vite (pronounced "veet") - https://vitejs.dev/ - ... which is the current favorite of the "Cool Kids" ...

---

## VI. Creating a "Todo" app with React and Vite

- Let's go though the first part of this YouTube video by [Web Dev Simplified](https://www.youtube.com/@WebDevSimplified) together:
  - [YouTube: Learn React With This One Project](https://www.youtube.com/watch?v=Rh3tobg7hEo)
  - Files: https://github.com/WebDevSimplified/react-todo-list/

**Completed version:**

![Screenshot](_images/intro-react-1.png)

---

### VI-A. Create a Vite project

- Create folder named **todo-app** and `cd` into it
- Type: `npm create vite@latest`
  - for *Project name*: **type a period** (`.`) to create a project in current **todo-app** folder
  - for *Framework*: choose **React**
  - for *Variant*: choose **JavaScript**
- `npm i`
- `npm run dev`
- Head to localhost to see app running in browser
  - click the "Count" button to try out `useState()`

---

### VI-B. Examine code and create "Hello World"
- Look in **index.html**, **main.js**, and **App.jsx** to see what they do
  - let's talk about the `useState()` code that the counter uses - we'll see more use of this React "hook" later
- Look in **package.json**
- Get rid of most of the web files, but keep:
  - **App.jsx**
  - **index.html**
  - **main.jsx**
    - remove this line from **main.jsx** - `import './index.css'`
- Make **App.jsx** look like this:

```jsx
const App = () => {
  return "Hello World";
};

export default App;
````

- Head to browser to see "Hello World" in window

---

### VI-C. Start building

- Create **src/styles.css**
- Here's the CSS - https://github.com/WebDevSimplified/react-todo-list/blob/main/src/styles.css
- Import these styles at the top of **App.jsx** with `import "./styles.css";`
- To get a `<form>` with a text `<input>` displaying, make the `App` component look like this:

```jsx
import "./styles.css";

const App = () => {
  return (
    <form className="new-item-form">
      <div className="form-row">
        <label htmlFor="item">New Item</label>
        <input type="text" id="item" />
      </div>
    </form>
  )
};

export default App;
```

- Check the browser to be sure the text input is displaying, then move on
- Now add a button to the bottom of the form (right before `</form>`)
  - `<button className="btn">Add</button>`
- Check the browser to be sure the button is also displaying, then move on
- Add an `<h1>` right AFTER the closing `</form>` tag:
  - `<h1 className="header">Todo List</h1>`
  - ERROR! React components require a *root element*!
  - go ahead and put the `<form>` and `<h1>` into an enclosing "fragment" - `<>...</>`
- Check the browser to be sure everything is displaying, then move on
- Add a list and a list item after the `<h1>`:

```jsx
<ul className="list">
  <li>
    <label>
      <input type="checkbox" />
      Item 1
    </label>
    <button className="btn btn-danger">Delete</button>
  </li>
</ul>
```

- Check the browser to be sure it is displaying, then move on

---

### VI-D. Create some state and setters/getters with `useState()`

- `useState` is a React Hook that lets you add a state variable to your function component
  - https://react.dev/reference/react/useState
- Hooks are features that allow you to “hook into” the features of React state and lifecycle from function components

- Add `import { useState } from "react";` to the top of **App.jsx**
- Add `const [newItem, setNewItem] = useState("test");` right before the `return` statement
  - note the array destructuring assignment above
  - `newItem` is a now declared as a variable
  - `setNewItem` is a setter (created by React) that I call whenever I want to change the value of `newItem`
  - `"test"` is the initial value for `newItem`
- Add `value={newItem}` attribute to the `<input>`
  - this *binds* the `newItem` variable's state (value) to the `<input>` field
  - but not the other way around
- Check the browser to be sure that "test" is displaying in the  `<input>` field, then move on
- Add interactivity to the text `<input>`:
  - add: `onChange={e => setNewItem(e.target.value)}` as an attribute to the `<input>`
  - try typing a new value into the `<input>`, although you can't see it yet, the value of `newItem` is being changed on every keystroke
  - go ahead and put in a `console.log()` in the correct place to see that this is true
- Let's add another `useState()` "hook" to keep track of our items:
  - type: `const [todos, setTodos] = useState([]);`

---

### VI-E. Get the "Add Todo" and "Display Todo List" functionality working

- To get the **Add** button working, add this attribute to the **`<form>`** (NOT the `<button>`):
  - `onSubmit={handleSubmit}`
  - note that React events and attributes are *camel cased* - `onSubmit`, `onClick` etc to distinguish them from vanilla DOM events which are lowercase only
  - there are errors in the console - `handleSubmit` isn't declared yet - so move on
- Now declare the `handleSubmit` function, it goes right under the 2 `useState()` declarations in the `App` component

```jsx
const handleSubmit = e => {
  e.preventDefault();
  // this adds a new todo object to the end of the array
  setTodos(currentTodos => {
    return [
      ...currentTodos,
      {
        id: crypto.randomUUID(),
        title: newItem,
        completed: false
      }
    ]
  });
  setNewItem(""); //clear out input
};
````

- Now **display** the todos by looping through `todos`:
  - note that React needs for a `key` value when rendering a list
    - https://react.dev/learn/rendering-lists
    - https://dev.to/shiv1998/why-not-to-use-index-as-key-in-react-lists-practical-example-3e66
  - replace the `<ul></ul>` code with this:

```jsx
<ul className="list">
  {todos.map(todo => {
    return <li key={todo.id}>
    <label>
      <input type="checkbox"  checked={todo.completed}/>
      {todo.title}
    </label>
    <button className="btn btn-danger">Delete</button>
  </li>
  })}
</ul>
```

- Check the browser, click the **Add** button to be sure that multiple items can be appended to the list, then move on ...

---

### VI-E. Carry on!
 - ***Ok we are going to stop there - this is around 26:00 out of 42 minute video - you can and should finish it on your own!***
   - in the remaining portion of the video, much of the code will be factored *out* of the `App` component, and *into* `TodoItem`, `TodoList` and `NewTodoForm` components
   - data persistance will also be added with `window.localStorage`
 - How do you "publish" the app and put it on the web?
   - press control-c to quit the "npm run vite" server
   - type `npm run build`
   - now you will see the **dist/** folder has been populated with an **index.html** file, a **.js** file and a **.css** file - this is the "transpiled and bundled" version that's ready for distribution
     - you can test it locally by running just this **dist/** folder on Live Server
     - PS - if you put these files on banjo, you'll need to first fix the `href` attributes of the `<script>` and `<link>` tags
       - hint: add a `.` to the beginning of the `src` and `href` urls 
