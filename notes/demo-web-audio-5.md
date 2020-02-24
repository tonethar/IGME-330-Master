# Web Audio V - The WebAudio Convolver Node

## I. Overview
- Today's demo is zipped in myCourses and here: https://igm.rit.edu/~acjvks/courses/shared/330/web-audio/convolver-demo/convolver_demo.html
- This demo looks at how to create *convolution reverb* effects with the WebAudio [`ConvolverNode`](https://developer.mozilla.org/en-US/docs/Web/API/ConvolverNode)
- "A convolution reverb can be used to simulate an acoustic space with very high quality. It can also be used as the basis for creating a vast number of unique and interesting special effects. This technique is widely used in modern professional audio and motion picture production, and is an excellent choice to create room effects in a game engine."
  -  https://www.w3.org/TR/2015/WD-webaudio-20151208/convolution.html 
  - https://en.wikipedia.org/wiki/Convolution_reverb
- These effects can be used to modify a sound such that it sounds like it took place on the telephone, a small room, and auditorium, a forest, and so on.
- To accomplish this the ConvolverNode utilizes *Impulse Response* (IR) sound files - which have captured a specific acoustic space:
  - you can create your own IR files [YouTube - How to Create Your Own Custom Impulse Responses](https://www.youtube.com/watch?v=g-mG2H4fvGg)
(for example)

- https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/ch06.html#s06_4

<hr><hr>

**[Previous Chapter <- Web Audio IV](demo-web-audio-4.md)**
