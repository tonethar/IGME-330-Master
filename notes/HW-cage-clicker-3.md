# HW - *Cage Clicker* Part III

In this chapter we will add:
  - the ability to click the sprites
  - incidental sound
  

## I. Clicking Sprites

- The `doMousedown` function is already handling navigating from the *start screen* to the main game screen - that code is in the `case GameState.START` section
- We now want to get the code handling clicking on the *main game screen*. Every time the use presses the mouse button, we will check to see if they clicked a sprite

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
  
2. To test this, reload the page, and test the main game screen by clicking all of the sprites. You should earn one point for each "cage", and -1 point for each non-cage. Giving you a final score of -2.


## II. Playing Sound

- In the completed version of the game we have 1 sound playing for clicking a "cage", and another playing when clicking a non-cage. Let's get this working

1. TO play sound, we are going to use the Howler JS library - you can read about it here: https://howlerjs.com

To import this library, add this line of code to the &lt;head> section of *index.html*, which will pull in Howler from a CDN:

```js
<script src="https://cdnjs.cloudflare.com/ajax/libs/howler/2.0.9/howler.min.js"></script>
```

2. In the `init()` function of *main.js*, add the following code:

```js
// Load Sounds
hitSound = new Howl({
	src: ['sounds/shoot.wav'],
	volume: 0.2
});

hitWrongSound = new Howl({
	src: ['sounds/bonk.mp3'],
	volume: 0.1
});

missSound = new Howl({ // not using yet
	src: ['sounds/miss.mp3'],
	volume: 0.2
});
```

- You will also have to declare these variables outside of the `init()`function, up top with the others

3. Uncomment the `hitWrongSound.play();` and `hitSound.play();` lines in `doMousedown`

4. Test it - you should now thes sounds play when you click the sprites



<hr><hr>

**[Previous Chapter <- Cage Clicker Part II](HW-cage-clicker-2.md)**

**Next Chapter -> Cage Clicker Part IV**
