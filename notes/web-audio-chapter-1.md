# WebAudio Study Guide - Chapter 1

## Overview

The WebAudio API can be used to build a variety of audio-related applications and games, that utilize advanced music synthesis and visualizations.

- Some handy links:
  - Amazon page for book - https://www.amazon.com/gp/product/1449332684
  - Sample code from book - https://webaudioapi.com/samples/
  - Web Audio Documentation:
    - https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API
    - https://www.w3.org/TR/webaudio/

## Chapter 1 - Fundamentals

1. Which technology does the author claim was the first cross-platform way to play audio on the web?

2. The Web Audio API is built around the concept of an ________________. The audio context is a directed graph of ________________ that defines how the audio stream flows from its ________________ (often an audio file) to its ________________ (often your speakers). As audio passes through each node, its properties can be ________________. The simplest audio context is a connection directly from a ________________ to a ________________ 

3. Note the more complicated web audio graph in Figure 1-2. What do the terms "wet" and "dry" mean in the context of the processing of audio sound signals? (google it!)

4. *Note the cross-platform way of obtaining an AudioContext - in this class we'll use the following version (no answer required)*:

```js
	let audioCtx = new (window.AudioContext || window.webkitAudioContext);
```

5. Give at least 2 examples of each of the following node types:

- Source nodes:

- Modification nodes:

- Analysis nodes:

- Destination nodes:

6. *Note*:
- *Figure 1.3 is the simplest possible audio graph that actually does something besides simply playing the sound (no answer required)*
- *Figure 1-4. Multiple sources with individual gain control as well as a master gain (no answer required)*

7. 
