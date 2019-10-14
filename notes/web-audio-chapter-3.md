# Web Audio Study Guide - Chapter 3

## Contents
<!--- Local Navigation --->
I. [Overview](#section1)

II. [Questions on Chapter 3 - Volume and Loudness](#section2)

III. [Example Code](#section3)

IV. [Homework](#section4)

<a id="section1"></a>

## I. Overview


<a id="section2"></a>

## II. Questions


<a id="section3"></a>

## III. Sample Code


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
<script>
let audio;
let gainNode;

window.onload = init;

function init() {
  audio = new Audio();
  audio.src = 'sounds/gain/chrono.mp3';
  
  let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  let sourceNode = audioCtx.createMediaElementSource(audio);
 	gainNode = audioCtx.createGain();
 	gainNode.gain.value = 1; // the default
  
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
  		gainNode.gain.setValueAtTime(1, audioCtx.currentTime);
  	}
  };
 
}
</script>
</body>
</html>
```

<hr><hr>

**[Previous Chapter <- Web Audio Chapter II](web-audio-chapter-2.md)**
