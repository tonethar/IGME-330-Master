# Web Audio Study Guide - Chapter 2

## Contents
<!--- Local Navigation --->
I. [Overview](#section1)

II. [Questions on Chapter 2 - Perfect Timing and Latency](#section2)

III. [Example Code](#section3)

IV. [Homework](#section4)

<a id="section1"></a>

## I. Overview

- This is a very short chapter that discusses how [web audio's](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) precise timing enables you to schedule events at specific times in the future.
- The main site for the book is here - https://webaudioapi.com

<a id="section2"></a>

## II. Questions

1. What is the property that will give you the current time (i.e. "where the playhead is") for the audio context?

2. Write a line of code that would start playing an `AudioBufferSourceNode` instance named `source1` immediately

3. Write a line of code that would start playing an `AudioBufferSourceNode` instance named `source1` in 3 seconds

4. True or False. Once a source node has finished playing back, it can’t play back more. To play back the underlying buffer again, you need to create a new source node (`AudioBufferSourceNode`) and call `start()`

5. Take a look at the code below. How many `AudioBufferSourceNode`s can we create to point at each audio array buffer (`ArrayBuffer`) instance - just one, or more than one?

<a id="section3"></a>

## III. Example Code

- The last thing we want to take a look at from this chapter is *Scheduling Precise Rhythms* and the simple and widely known known drumkit pattern mentioned in the text.
- Here is a working version of the code below: http://igm.rit.edu/~acjvks/courses/shared/330/web-audio/sg/rhythm.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title></title>
</head>
<body>
<button id="startButton">Click to hear beat</button>
<script>
window.onload = init;
let audioCtx;
let beat;

const trackPaths = { // we'll name our sound files to make it easier to keep track of them
    kick: 'sounds/rhythm/kick.wav',
    snare: 'sounds/rhythm/snare.wav',
    hihat: 'sounds/rhythm/hihat.wav'
 };
 
 function init(){
  // 1 - create a new `AudioContext`
  audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  
  // 2 - create a new instance of our sound file loader and then load the files
  // `tracksLoaded()` will be called once the audio files are loaded
  new BufferLoader(audioCtx,trackPaths,tracksLoaded).loadTracks();
}

function tracksLoaded(bufferObj){
	// 3 - set up event handler for button
	// RhythmSample will create new source nodes and play them every time we click the button 
	startButton.onclick = _ =>{
		beat = new RhythmSample(bufferObj.kick,bufferObj.snare,bufferObj.hihat);
		beat.play();
	}
}

/*
  Class RhythmSample:
    - has references to 3 `ArrayBuffer` binary arrays
    - `createSourceNodeAndPlay()` creates audio source nodes that point at these arrays and schedules a start time for the node
*/
	
class RhythmSample{
	constructor(kick,snare,hihat){
		this.kick = kick;
		this.snare = snare;
		this.hihat = hihat;
	}
	
  play(){
    // 4 -  We'll start playing the rhythm 100 milliseconds from "now"
    let startTime = audioCtx.currentTime + 0.100;
    let tempo = 80; // BPM (beats per minute)
    let eighthNoteTime = (60 / tempo) / 2;

    // 5 - Play 2 bars of the following:
    for (let bar = 0; bar < 2; bar++) {
      let time = startTime + bar * 8 * eighthNoteTime;
      // 6 - Play the bass (kick) drum on beats 1, 5 - both of these source nodes are using the same `ArrayBuffer` binary data
      this.createSourceNodeAndPlay(this.kick, time);
      this.createSourceNodeAndPlay(this.kick, time + 4 * eighthNoteTime);

      // 7 - Play the snare drum on beats 3, 7 - both of these source nodes are using the same `ArrayBuffer` binary data
      this.createSourceNodeAndPlay(this.snare, time + 2 * eighthNoteTime);
      this.createSourceNodeAndPlay(this.snare, time + 6 * eighthNoteTime);

      // 8 - Play the hi-hat every eighth note
      for (let i = 0; i < 8; ++i) {
        this.createSourceNodeAndPlay(this.hihat, time + i * eighthNoteTime);
      }
    }  
  }
  
  createSourceNodeAndPlay(buffer, time) {
  	// 9 - Create an `AudioBufferSourceNode`
		let source = audioCtx.createBufferSource();
		
	// 10 - Set its buffer (binary audio data)
		source.buffer = buffer;
		
	// 11 - Connect the source node to the destination
		source.connect(audioCtx.destination);
		
	// 12 - Start playing the sound
		source.start(time);
  }
}


/**** We already saw what this class was doing in chapter 1 ****/
class BufferLoader{
	constructor(ctx, trackPaths, callback) {
		this.ctx = ctx;
		this.trackPaths = trackPaths; // ex. {"trackName" :"trackURL", ...}
		this.callback = callback;
		this.trackBuffers = {};	      // will be populated with {"trackName" : buffer, ...}
		this.loadCount = 0;
		this.numToLoad = Object.keys(this.trackPaths).length;
	}
	
	loadTracks(){
	  for (let trackName of Object.keys(this.trackPaths)){
	    let trackURL = this.trackPaths[trackName];
	    this.loadBuffer(trackName,trackURL);
	  }
	}
	
	loadBuffer(trackName,trackURL) {
		const request = new XMLHttpRequest();
		request.responseType = "arraybuffer";
		request.open("GET", trackURL, true);
		request.send();
		
		/* Callbacks */
		request.onerror = e => console.error('BufferLoader: XHR error');

		request.onload = e => {
			const arrayBuffer = request.response;
			
			const decodeSuccess = buffer => {
				if(buffer) {
					this.trackBuffers[trackName] = buffer;

					if (++this.loadCount == this.numToLoad){
						this.callback(this.trackBuffers);
					}
				}else{
					console.error('error decoding file data: ' + url);
					return;
				}
			};
			
			const decodeError = e => {
					console.error('decodeAudioData error', e);
			};
			
			this.ctx.decodeAudioData(arrayBuffer,decodeSuccess,decodeError);
		};
		
	} // end method loadBuffer()
	
} // end class BufferLoader

</script>
</body>
</html>
```

- We are going to skip the rest of this chapter because the concepts of the `GainNode` and `OscillatorNode` will be covered in depth in future chapters

<a id="section4"></a>

## IV. Homework

***NONE!***

<hr><hr>

**[Previous Chapter <- Web Audio Chapter I](web-audio-chapter-1.md)**

**[Next Chapter -> Web Audio Chapter III](web-audio-chapter-3.md)**
