# HW - *Cage Clicker* Part IV

- In this chapter we will finish up the game.
- The game works fine, but it has a real problem, it's fairly easy to get a perfect score, but only if the player is patient enough to wait for a "safe" time to click. 
- This is a tedious and boring way to play a game - so let's fix this issue!

## I. Reason for adding a countdown timer

- To make the game more interesting, we are going to give the player a certain number of seconds per level to click on all of the cages.
- If they successfully do so before the time is up, then they will get full points. 
- But if they fail to click on all of the cages in time, penalty points will begin to accrue, 1 per second.
- Thus the "tedious and boring" strategy of waiting for the perfect moment to click a cage will fail, and the player will instead be forced to take risks.

## II. Getting Started

1. To get going on our countdown timer, go ahead and add these 3 variables to the top section of *main.js*:

```js
let startTime;
let lastTimeRemaining = 0; // time remaining in integer seconds
let displayTime;
```

2. To draw the time remaining, add this code to `drawHUD()` at `GameState.MAIN`:

```js
// draw level timer
let displayColor = "white";
if (displayTime < 0) displayTime = 0;
if (displayTime <= 3) displayColor = "yellow";
if (displayTime == 0) displayColor = "red"
fillText(ctx,`Time remaining: ${displayTime}`, 10, screenHeight-20, "14pt courier", displayColor);
```

## III. Improvements to this game

There are many, many improvements you could make to this game, here are some possibilities:





<hr><hr>

**[Previous Chapter <- Cage Clicker Part III](HW-cage-clicker-3.md)**
