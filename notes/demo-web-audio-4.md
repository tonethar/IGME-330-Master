# Web Audio IV - *Audio Concepts Review*

## I. Overview
- Let's review some of the slides from the IIM audio lecture:
  - [IGME-110 - Week-11a-Audio-Lecture.pdf](./_files/Week-11a-Audio-Lecture.pdf)
- We are also going to take going to take a look at Chapter 1 - *Fundamentals* of this online book -  *Web Audio API: Advanced Sound for Games and Interactive Apps*
  - https://webaudioapi.com/book/Web_Audio_API_Boris_Smus_html/toc.html
  - [Web Audio Study Guide - Chapter 1 - *Fundamentals*](./web-audio-chapter-1.md)


## II. IIM Slides

- Slides #3-#5
  - Sound waves are variations of pressure in a *medium* such as air
  - Typical waveform graphs are two-dimensional, but in the real world sound waves are three-dimensional. Waveform graphs usually visualize a sound wave progressing up and down from from left to right, but real sound waves travel in an expanding sphere from the source.
  - High amplitude values represent areas of increased air pressure. 
  - The end result of manipulating sounds is a series of high and low pressure zones
  - Sources: 
    - https://www.mediacollege.com/audio/01/sound-waves.html
    - https://www.soundproofingcompany.com/soundproofing_101/what-is-sound
- Slides #6 - #13
  - Starting with Thomas Edison's demonstration of the first phonograph in 1877, it has been possible to capture sound pressure waves onto a physical medium (Phonographic record, tape, etc) and then reproduce the sound later by reproducing the same pressure waves - this is called *analog* recording
  -  Analog recording suffers from the problem of *noise*. Each time an analog recording is copied, more noise is introduced, decreasing the accurancy of the reprodution (fidelity)
  - *Digital recording* works by sampling the audio wave at evenly-spaced timepoints, and then representing each sample as a discrete number. These can be copied perfectly without introducing any additional noise
  - *Sample rates* are measured in hertz (Hz), or cycles per second. This value is the number of samples captured per second in order to represent the waveform.
  - Recording sound from an analog-to-digital-converter (like a modern microphone) converts a time-varying voltage signal into a discrete-time signal, a sequence of real numbers
  - Sources:
    - https://manual.audacityteam.org/man/digital_audio.html
    - https://en.wikipedia.org/wiki/Digital_recording
- Slide #15
  - Here *sampling rate* and the *Nyquist Theorem* is discussed - accurate reproduction of a waveform requires at least 2 samples per cycle
  - The human ear is sensitive to sound patterns with frequencies between approximately 20 Hz and 20000 Hz. Sounds outside that range are inaudible. Therefore a sample rate of 40000 Hz is the absolute minimum necessary to reproduce the full range of audible sounds. (Not coincidentally, CD Quality sound is 44.1 kHz)
  - Higher sample rates allow higher audio frequencies to be represented. Provided that the sample rate is more than double the highest audio frequency present, the waveform can be reconstructed exactly from the digital samples. 
  - So we end up with these 3 important properties of waves - *wavelength*, *amplitude* & *frequency*:
    - https://www.mediacollege.com/audio/01/wave-properties.html
- Slide #16
  - *Quantization* is how each sampled real number (the *amplitude* i.e *loudness* of each sample) is replaced with an approximation from a finite set of discrete values:
    - examples: 4-bit (0-15), 8-bit (0-255)
  - Sources:
    - https://en.wikipedia.org/wiki/Quantization_(signal_processing)
 - We'll let you review the rest of these slides are your own   
    
 ## III. 
 
 - Slide #17 in the presentation above mentioned *headroom*
 
 

<hr><hr>

**[Previous Chapter <- Web Audio III](demo-web-audio-3.md)**

**[Next Chapter -> Web Audio V](demo-web-audio-5.md)**
