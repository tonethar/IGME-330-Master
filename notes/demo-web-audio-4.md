# Web Audio IV - *Audio Concepts Review*

## I. Overview
- Let's review some of the slides from the IIM audio lecture:
  - [IGME-110 - Week-11a-Audio-Lecture.pdf](./_files/Week-11a-Audio-Lecture.pdf)
- We are also going to take going to take a look at Chapter 1 - *Fundamentals* of this online book -  *Web Audio API: Advanced Sound for Games and Interactive Apps*
  - https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/toc.html
  - [Web Audio Study Guide - Chapter 1 - *Fundamentals*](./web-audio-chapter-1.md)


## II. IGME-110 IIM Audio Slides

1) Slides #3-#5
    - Sound waves are variations of pressure in a *medium* such as air
    - Typical waveform graphs are two-dimensional, but in the real world sound waves are three-dimensional. Waveform graphs usually visualize a sound wave progressing up and down from from left to right, but real sound waves travel in an expanding sphere from the source.
    - High amplitude values represent areas of increased air pressure within a series of high and low pressure zones
    - Sources: 
      - https://www.mediacollege.com/audio/01/sound-waves.html
      - https://www.soundproofingcompany.com/soundproofing_101/what-is-sound
2) Slides #6 - #13
    - Starting with Thomas Edison's demonstration of the first phonograph in 1877, it has been possible to capture sound pressure waves onto a physical medium (Phonographic record, tape, etc) and then reproduce the sound later by reproducing the same pressure waves - this is called *analog* recording
    -  Analog recording suffers from the problem of *noise*. Each time an analog recording is copied, more noise is introduced, decreasing the accurancy of the reprodution (fidelity)
    - *Digital recording* works by sampling the audio wave at evenly-spaced timepoints, and then representing each sample as a discrete number. These can be copied perfectly without introducing any additional noise
    - *Sample rates* are measured in hertz (Hz), or cycles per second. This value is the number of samples captured per second in order to represent the waveform.
    - Recording sound from an analog-to-digital-converter (like a modern microphone) converts a time-varying voltage signal into a discrete-time signal, a sequence of real numbers
    - Sources:
      - https://manual.audacityteam.org/man/digital_audio.html
      - https://en.wikipedia.org/wiki/Digital_recording
3) Slide #15
    - Here *sampling rate* and the *Nyquist Theorem* is discussed - accurate reproduction of a waveform requires at least 2 samples per cycle
    - The human ear is sensitive to sound patterns with frequencies between approximately 20 Hz and 20000 Hz. Sounds outside that range are inaudible. Therefore a sample rate of 40000 Hz is the absolute minimum necessary to reproduce the full range of audible sounds. (Not coincidentally, CD Quality sound is 44.1 kHz)
    - Higher sample rates allow higher audio frequencies to be represented. Provided that the sample rate is more than double the highest audio frequency present, the waveform can be reconstructed exactly from the digital samples. 
    - So we end up with these 3 important properties of waves - *wavelength*, *amplitude* & *frequency*:
      - https://www.mediacollege.com/audio/01/wave-properties.html
4) Slide #16
    - *Quantization* is how each sampled real number (the *amplitude* i.e *volume* of each sample) is replaced with an approximation from a finite set of discrete values:
      - examples: 4-bit (0-15), 8-bit (0-255), 16-bit (0-65,535)
      - higher *bit depths* give better fidelity
    - Sources:
      - https://en.wikipedia.org/wiki/Quantization_(signal_processing)
   - We'll let you review the rest of these slides on your own   
    
 ## III. Avoid *clipping* your sounds
 
 1) Slide #17 in the presentation above mentioned *headroom* - which is the maximum amount of undistorted signal a system can handle compared to the average level for which the system is designed. When we run out of headroom, distortion happens.
    - There is a discussion of this in the *Volume & Loudness* chapter of the online web audio book - https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/ch03.html
      - *Loudness* is a subjective measure of how intensely our ears perceive a sound
      - *Volume* is a measure of the physical amplitude of a sound wave
      - *Gain* is a scale multiplier affecting a sound’s amplitude as it is being processed
      - When undergoing a gain (such as when we add a [`GainNode`](https://developer.mozilla.org/en-US/docs/Web/API/GainNode) to an audio graph), the amplitude of a sound wave is scaled, with the gain value used as a multiplier. This increases the perceived *loudness* of the sound
      - Sounds will be *clipped* - which will distort the sound - if the waveform exceeds its maximum level:
        - https://en.wikipedia.org/wiki/Clipping_(audio)
     
 <img src="https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/images/waap_0305.png" alt="clipped sound image">
 
2) On your own, you can read about (in the link above):
     - *Using Meters to Detect and Prevent Clipping*
     - *Dynamic Range*
     - *Dynamics Compression* and the [`DynamicsCompressorNode`](https://developer.mozilla.org/en-US/docs/Web/API/DynamicsCompressorNode)
 
 ## IV. Audio Fundamental Terms
 
 - See this chapter on *Fundamentals* --> https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/ch01.html
 - Let's quickly skim the above chapter (5 minutes or so) and answer the questions on the Study Guide here  --> [Web Audio Study Guide - Chapter 1 - *Fundamentals*](./web-audio-chapter-1.md)
 - Here are the correct answers (jumbled up) for all of the questions except Q#5:
   - 8 kHz
   - 16-bit
   - 44.1 kHz
   - AAC or MP3
   - arrays of numbers
   - audio context
   - audio nodes
   - destination
   - destination node
   - FLAC or WAV or AIFF
   - flash
   - function
   - longitudinal 
   - lossy
   - lossless
   - modified or inspected
   - modified sound
   - quality v. file size
   - quantization
   - sampling
   - source
   - source node
   - time
   - unmodified sound
   

<hr><hr>

**[Previous Chapter <- Web Audio III](demo-web-audio-3.md)**

**[Next Chapter -> Web Audio V](demo-web-audio-5.md)**
