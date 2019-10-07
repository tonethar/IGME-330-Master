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

2. The Web Audio API is built around the concept of an _______________. The audio context is a directed graph of _______________ that defines how the audio stream flows from its _______________ (often an audio file) to its _______________ (often your speakers). As audio passes through each node, its properties can be ______________. The simplest audio context is a connection directly from a ______________ to a _______________

3. Note the more complicated web audio graph in Figure 1-2. What do the terms "wet" and "dry" mean in the context of the processing of audio sound signals? (google it!)

4. *Note the cross-platform way of obtaining an `AudioContext` - in this class we'll use the following version (no answer required)*:

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

7. In terms of physics, sound is a _______________ wave (sometimes called a pressure wave) that travels through air or another medium. 

8. Mathematically, sound can be represented as a _______________, which ranges over pressure values across the domain of _______________.

9. According to the author, what is the most common *sample rate* and *bit depth* for typical digital audio?

10. The process of converting analog signals into digital ones is called _______________ or _______________

11. According to the author, what is the typical sample rate for a telephone system?

12. What is the benefit (and associated trade-off) of increasing the sample rate of a sound?

13. *Pulse-code modulation* (PCM) treats sounds as _______________

14. When we load/analyze/manipulate an existing sound file using WebAudio, the loading code for a sound that is in a *lossy* or *lossless* format is the same. But it is still important to know the differences

- With _______________ compression the bits are identical before and after the compression process

- With _______________ compression some bits are thrown away (the ones we hope the user won't hear anyway)

- Give an example of a *lossless* audio file format _______________

- Give an example of a *lossy* audio file format _______________

15. 


