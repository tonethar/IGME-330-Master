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

**array-filter-sort.html**

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Array sort/filter</title>
  <script>
    class Dragon{
      constructor(type,age){
        this.type = type;
        this.age = age;
      }
    }
    const dragons = [];
    dragons.push(new Dragon("Red",100));
    dragons.push(new Dragon("Chromatic",5000));
    dragons.push(new Dragon("Fire",25));
    
    console.log("All dragons:");
    dragons.forEach(d => console.log(d));

    // Filter
    const dragonsOlderThan50 = dragons.filter(d => d.age > 50);
    console.log("dragonsOlderThan50:");
    dragonsOlderThan50.forEach(d => console.log(d));

    // Sort by age ASC
    const sortAge = (a, b) => a.age - b.age;
    dragons.sort(sortAge);
    console.log("dragons sortAge:");
    dragons.forEach(d => console.log(d));

    // Sort alpha ASC
    const sortAlpha = (a, b) => a.type < b.type ? -1 : 1;
    dragons.sort(sortAlpha);
    console.log("dragons sortAlpha:");
    dragons.forEach(d => console.log(d));
  </script>
</head>
<body>
  
</body>
</html>
```
