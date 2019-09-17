# HW - Audio Visualizer - Part I

## I. Overview
In part I of this HW, you will be learning about the HTML5 [WebAudio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API), and how to utilize it to create an audio visualizer. Topics explored:

1. [Audio Routing Graph](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Basic_concepts_behind_Web_Audio_API#Audio_graphs)

![image](_images/audio-routing-graph.jpg)

2. [AnalyzerNode](https://developer.mozilla.org/en-US/docs/Web/API/AnalyserNode)
  - sampling & bins
  - frequency data - `analyserNode.getByteFrequencyData(data);`
  - waveform data  - `analyserNode.getByteTimeDomainData(data);`
  
3. [JavaScript Typed Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays) - frequency and waveform data is passed *by reference* to these non-resizable typed arrays.

4. [CORS Restrictions](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) - ("Cross-origin Resource Sharing") means that you can't run the visualizer start files locally off of your hard drive. You might see an error message like this:

**`MediaElementAudioSource outputs zeroes due to CORS access restrictions for file:///Users/...../soundfile.mp3`**

**Solutions to CORS issues:**
- Run the code off of a web server, which you can do by uploading your code to Banjo
- Use an IDE like [Brackets](http://brackets.io) - which creates a local web server for you to run your code on
- [You can also create a web server using Python](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/set_up_a_local_testing_server) on your local machine
- NodeJS can also run a local web server for you: https://www.npmjs.com/package/http-server
- [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) turns off CORS by default, so you don't need a web server

## II. Submission
- the instructions are here: [Audio-Viz-ICE-1.pdf](_files/Audio-Viz-ICE-1.pdf) 
- the start files are zipped up in mycourses
- also see the mycourses.rit.edu dropboxes for due date

