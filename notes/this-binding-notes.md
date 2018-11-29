# `this` Binding Notes

## Overview
- in 230 we discussed how the value of `this` in a function depends on how it is called -> https://github.com/tonethar/IGME-230-Master/blob/master/notes/web-apps-6.md
- if a function is called by an event handler, the value of `this` is the object that triggered the event (a button in an `onclick` handler,  or the `window` in an `.onload` handler for example)



## Reference
- [MDN - `Function.bind()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
