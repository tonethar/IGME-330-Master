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

- The starter code is really helping you out here as sprites already have a `getRect()` method, and rects already have a `containsPoint()` method. Be sure to take a look at this code in both *Sprite.js* and *Rect.js*
- when we click a sprite:
  - if the Sprite's `.type` is NOT equal to `levelTarget` (which equals `"cage"`) then:
    - set the speed to zero
    - lower the score
    - play a sound (to be done soon)
  - if the Sprite's `.type` IS equal to `"cage"` then:
    - set the speed to zero
    - raise the score
    - up the `cageCount`, which determines when the level is over
  - also check out `loadLevel`, where `levelGoal`, `levelTarget`, `vectorChangeProb` and `levelTimeLimit` are going to be defined with unique values for every level of the game
  
2. Reload the page, and test the main game screen by clicking all  

**[Previous Chapter <- Cage Clicker Part II](HW-cage-clicker-2.md)**

**Next Chapter -> Cage Clicker Part IV**
