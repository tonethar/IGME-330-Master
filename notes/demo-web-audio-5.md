# Web Audio V - The WebAudio Convolver Node

## I. Overview
- Today's demo is zipped in myCourses and here: https://igm.rit.edu/~acjvks/courses/shared/330/web-audio/convolver-demo/convolver_demo.html
- This demo looks at how to create *convolution reverb* effects with the WebAudio [`ConvolverNode`](https://developer.mozilla.org/en-US/docs/Web/API/ConvolverNode)
- *Linear Convolutions* are mathematical operations on two functions (represented in this case by arrays of numbers) that produce a third function (another array of numbers) expressing how the shape of one is modified by the other
- *"A convolution reverb can be used to simulate an acoustic space with very high quality. It can also be used as the basis for creating a vast number of unique and interesting special effects. This technique is widely used in modern professional audio and motion picture production, and is an excellent choice to create room effects in a game engine."*
  -  https://www.w3.org/TR/2015/WD-webaudio-20151208/convolution.html 
  - https://en.wikipedia.org/wiki/Convolution_reverb
- These effects can be used to modify a sound such that it sounds like it took place on the telephone, a small room, in an  auditorium, a forest, and so on
- To accomplish this the `ConvolverNode` utilizes *Impulse Response* (IR) sound files - which have captured a specific acoustic space:
  - *"The idea for producing room effects is to play back a reference sound in a room, record it, and then (metaphorically) take the difference between the original sound and the recorded one. The result of this is an impulse response that captures the effect that the room has on a sound. These impulse responses are painstakingly recorded in very specific studio settings, and doing this on your own requires serious dedication. Luckily, there are sites that host many of these pre-recorded impulse response files (stored as audio files) for your convenience."*
    - https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/ch06.html#s06_4
  - you can also create your own IR files [YouTube - How to Create Your Own Custom Impulse Responses](https://www.youtube.com/watch?v=g-mG2H4fvGg)
- The code to accomplish this in WebAudio is simple, and looks like this:

```js
let convolver = audioCtx.createConvolver();
convolver.buffer = linkToImpulseResponseSoundBuffer;
source.connect(convolver);
convolver.connect(audioCtx.destination);
```

- note that in the example code, we are loading **both** our source audio ("Captain Picard") and our IR file as *buffers* (raw bytes). In your code, you can load your source file normally as in the AV HW, and will only need to load the specific IR file you are using as a buffer.



<hr><hr>

**[Previous Chapter <- Web Audio IV](demo-web-audio-4.md)**

**[Next Chapter -> Web Audio VI](demo-web-audio-6.md)**
