# Web Audio Study Guide - Chapter 3

## Contents
<!--- Local Navigation --->
I. [Overview](#section1)

II. [Questions on Chapter 3 - Volume and Loudness](#section2)

III. [Example Code](#section3)

IV. [Homework](#section4)

<a id="section1"></a>

## I. Overview

- For this chapter we will look at utilizing a *gain* node, which is used to alter the *volume* of the sound
- We will also see how to create an `<audio>` element (rather than a `AudioBuffer`) that can be used to play a sound file - which simplifies the setup code dramatically (the disadvantage to this approach is that we can only play one sound at a time): 
  - docs for the `<audio>` element: https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement
  - most of the properties and methods and events for `<audio>` are here: https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement

<a id="section2"></a>

## II. Questions

1. Define *loudness*

2. Define *volume*

3. Define *gain*

4. What will a *gain* value of 1 do to the amplitude of a sound wave?

5. What does *dBSPL* stand for?

6. Web Audio uses *dBFS* -  which stands for?

7. dBFS is a measure of gain. Thus a gain of 1 is the sound's full volume, a gain of 0.5 is the sound's reduced to 1/2 volume (amplitude), and a gain of 0 is silence. (*no answer required*)


### II-A. Equal Power Crossfading

8. A *linear fade* between 2 sounds can sound unbalanced because of a ______________

9. An *equal power crossfade* curve, in which the corresponding gain curves are neither linear nor exponential, will ______________

10. See examples of crossfades in Figure 3-2 and Figure 3-3. Also check out the crossfade example here (view source to see the code, *no answer required*): https://webaudioapi.com/samples/crossfade/


### II-B. Clipping and Metering

11. Note that mixing sounds together or utilizing too much gain can cause the amplitude of the waves to become too large and *clipping* will result - see Figure 3.5. Also see the `checkClipping(buffer)` function for code that can detect clipping   (*no answer required*)

### II-C. Clipping and Metering

12. 

<a id="section3"></a>

## III. Sample Code

- We're solely illustrating the concept of gain in the code below
- Note the use of the `<audio>` element, which simplifies loading a sound
- We are also using a checkbox and a slider
- Working version of the below code is here: http://igm.rit.edu/~acjvks/courses/shared/330/web-audio/sg/gain-demo.html


```html
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
<script>
let audio;
let gainNode;

window.onload = init;

function init() {
  audio = new Audio();
  audio.src = 'sounds/gain/chrono.mp3';
  
  let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  let sourceNode = audioCtx.createMediaElementSource(audio);
 	gainNode = audioCtx.createGain(); // the default `gain.value` is 1
  
  sourceNode.connect(gainNode);
  gainNode.connect(audioCtx.destination);
  
  playButton.onclick = _ => audio.play();
  stopButton.onclick = _ => {
  	audio.pause();
  	audio.currentTime = 0;
  };
  
  muteCheckbox.onchange = e => {
  	if(e.target.checked){
  	 	gainNode.gain.setValueAtTime(0, audioCtx.currentTime);
  	} else {
  		let value = volumeSlider.value/100;
  		gainNode.gain.setValueAtTime(value, audioCtx.currentTime);
  	}
  };
  
  volumeSlider.oninput = e =>{
  	gainNode.gain.value = e.target.value/100;
  }
  
  volumeSlider.dispatchEvent(new Event("input"));
 
}
</script>
</body>
</html>

```

<hr><hr>

**[Previous Chapter <- Web Audio Chapter II](web-audio-chapter-2.md)**
