# Web Audio Study Guide - Chapter 3

## Contents
<!--- Local Navigation --->
I. [Overview](#section1)

II. [Questions on Chapter 3 - Volume and Loudness](#section2)

III. [Example Code](#section3)

IV. [Homework](#section4)

<a id="section1"></a>

## I. Overview

- For this chapter we will look at utilizing a *gain* node, which is used to alter the *volume* of the sound. The main site for the book is here - https://webaudioapi.com
- We will also see how to create an `<audio>` element (rather than a `AudioBuffer`) that can be used to play a sound file - which simplifies the setup code dramatically (the disadvantage to this approach is that we can only play one sound at a time): 
  - docs for the `<audio>` element: https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement
  - most of the properties and methods and events for `<audio>` are here: https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement
- We will also see how to give the user the ability to control the experience with a slider and a checkbox

<a id="section2"></a>

## II. Questions

1. Define *loudness*

2. Define *volume*

3. Define *gain*

4. What will a *gain* value of 1 do to the amplitude of a sound wave?

5. What does *dBSPL* stand for?

6. Web Audio uses *dBFS* -  which stands for?

7. *dBFS* is a measure of *gain*. Thus a gain of 1 is the sound's full volume, a gain of 0.5 is the sound's reduced to 1/2 volume (amplitude), and a gain of 0 is silence. (*no answer required*)


### II-A. Equal Power Crossfading

8. A *linear fade* between 2 sounds can sound unbalanced because of a ______________

9. An *equal power crossfade* curve, in which the corresponding gain curves are neither linear nor exponential, will ______________

10. See examples of crossfades in Figure 3-2 and Figure 3-3. Also check out the crossfade example here (view source to see the code, *no answer required*): https://webaudioapi.com/samples/crossfade/


### II-B. Clipping and Metering

11. Note that mixing sounds together or utilizing too much gain can cause the amplitude of the waves to become too large and *clipping* will result - see Figure 3.5. Also see the `checkClipping(buffer)` function for code that can detect clipping. Check out the clipping example here  (view source to see the code, *no answer required*): https://webaudioapi.com/samples/metering/

### II-C. Dynamic Range

12. In audio, *dynamic range* refers to the difference between ______________

13. According to the author, which music genres tend to have a small dynamic range and be uniformly loud?

13. *Dynamics Compressors* can also be used to help mitigate issues caused by clipping or a clip having too much dynamic range. See the example linked from here: https://developer.mozilla.org/en-US/docs/Web/API/DynamicsCompressorNode - note: this example seems to run in FireFox only (*no answer required*)

<a id="section3"></a>

## III. Example Code

- We're solely illustrating the concept of gain in the code below
- Note the use of the `<audio>` element, which simplifies loading a sound
- We are also using a checkbox and a slider
- We are also hooking into the `<audio>` element's `ontimeupdate` event to display the current progress of the track
- The working version of the below code is here: http://igm.rit.edu/~acjvks/courses/shared/330/web-audio/sg/gain-demo.html


```html
<!DOCTYPE html>
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
	<style>
		body{
			font-family:sans-serif;
		}
		button{
			font-size: 1.5rem;
			margin-right: 1rem;
		}
	</style>
</head>
<body>
<h1>Audio Player</h1>
<p><button id="playButton">Play</button><button id="stopButton">Stop</button></p>
<p><input type="checkbox" id="muteCheckbox"> Mute</p>
<p>0 <input type="range" min="1" max="100" value="20" id="volumeSlider"> 100</p>
<p id="currentTimeElement">Current Time: ??</p>
<script>
let audio;
let gainNode;

window.onload = init;

function init() {
  // 1 - create a new <audio> element - we won't need to add it to the page for it to work
  audio = new Audio();
  audio.src = 'sounds/gain/chrono.mp3';
  
  // 2 - create our audio context
  let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  
  // 3 - make the <audio> element the source for our source node
  let sourceNode = audioCtx.createMediaElementSource(audio);
  
  // 4 - create a gain node
 	gainNode = audioCtx.createGain(); // the default `gain.value` is 1
  
  // we now have 3 nodes (source,gain,destination) - so let's connect them
  sourceNode.connect(gainNode);
  gainNode.connect(audioCtx.destination);
  
  // 5 - set up event handlers for buttons
  playButton.onclick = _ => audio.play();
  stopButton.onclick = _ => {
  	audio.pause();
  	audio.currentTime = 0;
  };
  
  // 6 - set up event handler for checkbox
  muteCheckbox.onchange = e => {
  	if(e.target.checked){
  	 	gainNode.gain.setValueAtTime(0, audioCtx.currentTime);
  	} else {
  		let value = volumeSlider.value/100;
  		gainNode.gain.setValueAtTime(value, audioCtx.currentTime);
  	}
  };
  
  // 7 - set up event handler for slider
  volumeSlider.oninput = e =>{
  	gainNode.gain.value = e.target.value/100;
  }
  
  // 8 - set up `ontimeupdate` event handler for <audio> element
  audio.ontimeupdate = e =>{
  	currentTimeElement.innerHTML = `Current Time: ${e.target.currentTime.toFixed(3)}`;
  }
  
  // 9 - this code sets the starting gain to the value of the slider
  volumeSlider.dispatchEvent(new Event("input"));
  
  // 10 - this code sets the starting text in the <p> to the `.currentTime` of the <audio> element
  audio.dispatchEvent(new Event("timeupdate"));
 
}
</script>
</body>
</html>
```

<a id="section4"></a>

## IV. Homework

***None!***

<hr><hr>

**[Previous Chapter <- Web Audio Chapter II](web-audio-chapter-2.md)**

**[Next Chapter -> Web Audio Chapter IV](web-audio-chapter-4.md)**
