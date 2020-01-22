# HW - Algorithmic Botany


## I. Overview

 - Today we'll
 - In botany, phyllotaxy is the arrangement of leaves on a plant stem - these spirals form a distinctive class of patterns in nature.
 
 Links:
 - Coding Train [Coding Challenge #30: Phyllotaxis](https://thecodingtrain.com/CodingChallenges/030-phyllotaxis.html)
 - https://en.wikipedia.org/wiki/Phyllotaxis
 - http://www.algorithmicbotany.org
 - http://www.algorithmicbotany.org/papers/abop/abop-ch4.pdf
 
 
## II. Instructions

- Watch the video
- Grab the start file

1. Add your `window.onload = init;` call to the right place.

2. Create a "script scoped" variable named `n` that keeps track of the number of dots (petals) as we draw them. "script scoped" means that it is declared at the "top level" outside of any functions.

`let n = 0;`

3. Also go ahead and declare the "divergence angle" in "script scope":

`const divergence = 137.5;`

4. Now create a `loop()` function that looks like this, and call it from the end of the `init()` function:

```js
function loop(){
 	setTimeout(loop,1000/30);
  
  
  n++;
}
```

5. Each frame we need to draw a new dot (pedal) by calulating its polar coordinates (a distance from the center - `r` below, and an angle `a` below). Add the following to the top of `loop()` - after the call to `setTimeout()`:

```js
// each frame draw a new dot
// `a` is the angle
// `r` is the radius from the center of the flower
// `c` is the "padding" between the dots
let a = n * dtr(137.5);
let r = c * Math.sqrt(n);
console.log(a,r);
```

6. `c` is a "script scoped" variable - go declare and initialize it now:

`const c = 4;`

7. 
