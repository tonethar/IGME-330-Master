# HW - *Cage Clicker* Part III

In this chapter we will add:
  - the ability to click the sprites, 

## I. Clicking Sprites

- The `doMousedown` function is already handling navigating from the start screen to the main game screen (though the `case GameState.START`)
- We now want to get it handling clicking on the main grame screen. Every time the use presses the mouse button, we will check to see if they clicked a sprite

1. Add the following to the `doMousedown` function, under `case GameState.MAIN:`

```js
// we are going to loop through the array backwards so we check the sprites that are "on top" first
for (let i = sprites.length - 1; i >= 0; --i) {

	let s = sprites[i];
	if (s.getRect().containsPoint(mouse)){
		if (s.speed == 0) continue; // don't score the sprite if it's already been clicked
		if (s.type != levelTarget){
			// don't score the sprite if it is the wrong type
			levelScore --;
			totalScore --;
			s.speed = 0;
		//	hitWrongSound.play(); // we will write the sound code later
			break; // break out of loop so that we only penalize one sprite per click
		}
		s.speed = 0;
		cageCount ++;
		levelScore ++;
		totalScore ++;
	//	hitSound.play(); // we will write the sound code later
		break; // break out of loop so that we only score one sprite per click
	}
} // end for loop
```


**[Previous Chapter <- Cage Clicker Part II](HW-cage-clicker-2.md)**

**Next Chapter -> Cage Clicker Part IV**
