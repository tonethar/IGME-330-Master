# Canvas 2D Essential Skills #2 - Begin making screensaver




## II. Handy Helper Functions

These will be useful as we build our screen saver.

```js
 // handy helper functions!
    function getRandomColor(){
      function getByte(){
        return 55 + Math.round(Math.random() * 200);
      }
      return "rgba(" + getByte() + "," + getByte() + "," + getByte() + ",.8)";
    }

    function getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }
 ```
 
 
 
 <hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**#2 - Paths & Lines & Arcs**](2-canvas-paths-lines-arcs.md) |  [**IGME-330**](../README.md) | [**Skill #4 - TBA**]()
