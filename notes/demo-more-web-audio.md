# Demo - More Web Audio

## I. Overview
Here we are going to build on our [Web Audio Demo](./demo-web-audio-1.md) by chaining multiple effect nodes:
- a checkbox to control the *treble* of the sound (a *highshelf* [BiquadFilterNode](https://developer.mozilla.org/en-US/docs/Web/API/BiquadFilterNode))
- a checkbox to control the *bass* of the sound (a *lowshelf* BiquadFilterNode)
- a checkbox and a slider to control the *distortion* of the sound (a [*WaveShaperNode*](https://developer.mozilla.org/en-US/docs/Web/API/WaveShaperNode) filter)
  - waveshaping is non-linear distortion, and can be likened to a distorting amplifier - some frequencies fed into the filter will be suppressed, others will be exagerated, and some new sound components not present in the original signal will be introduced
  - http://magic.hecanjog.com/Sounds/Words/CMJ-1979-Vol3-No2-June/3680281.pdf


## II. Start File

- the start file is the **web-audio-3.html** we built in [Web Audio Demo](./demo-web-audio-1.md)

![screenshot](./_images/web-audio-3.jpg)

## III. Done Version

- Below we have added 3 checkboxes and a slider

![screenshot](./_images/web-audio-4.jpg)

## IV. HTML & CSS

