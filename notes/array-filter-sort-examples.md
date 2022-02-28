# `array.filter()` & `array.sort()` Examples

## I. Overview
- Use [`array.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) and [`array.sort()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) - to alter the array of results that the user sees in your app
- `array.filter()`
  - *"The `filter()` method creates a new array with all elements that pass the test implemented by the provided function"*
  - `const newArray = oldArray.filter(num => num < 5)` creates a new array that contains only those elements from `oldArray` that have a value creater than `5`
- `array.sort()`
  - *"The `sort(compareFunction)` method sorts the elements of an array in place and returns the sorted array"*
  - ex `numberArray.sort((a,b) => b - a)`
  - if `compareFunction` is supplied, all non-undefined array elements are sorted according to the return value of the compare function
    - if the return value is `> 0` -	sort b before a
    - if the return value is `< 0` -	sort a before b

<hr>

## II. Code

```html

```
