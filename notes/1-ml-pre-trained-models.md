# 1 - Machine Learning with ml5 - pre-trained models

## I. What is Machine Learning

- "A field of study that gives computers the ability to learn without being explicitly programmed" - [Arthur Samuel](https://en.wikipedia.org/wiki/Arthur_Samuel)
- https://en.wikipedia.org/wiki/Machine_learning
- We will be looking at the [ml5](https://ml5js.org/) machine learning API
  - this API "wraps" [Tensorflow](https://www.tensorflow.org/overview) (which you have probably heard of) and makes model loading, training new models and memory management a lot easier
- Components of Machine Learning: 
 - 1. Algorithms  - *neural network* algorithms designed to recognize patterns
 - 2. Models - they can be *pre-trained* like ImageNet (which we will use today) or we can train them ourselves (for example with [Teachable Machine](https://teachablemachine.withgoogle.com/))
 - 3. Datasets
   - we will be looking at *supervised learning* in this class - which makes use of *labeled* datasets where we provide the API with training data that consists of an *input* (for example a "vectorized" image or piece of text) and the desired *output* value (ex. a label such as "dog") 
- The trained model is only as "good" as the dataset it's given:
  - https://towardsdatascience.com/a-dataset-is-a-worldview-5328216dd44d
- Another technique is *transfer learning* - which is the reuse of a pre-trained model on a new problem - which is actually what Teachable Machine is doing

<hr>

## II. Image Classification with MobileNet

- Using a pre-trained model like MobileNet  - it only has a finite number of images it was trained with - https://github.com/ml5js/ml5-library/blob/main/src/utils/IMAGENET_CLASSES.js
- https://www.image-net.org/index.php

<hr>

## III. Get Started

1) Head to **Quickstart: Plain JavaScript** here: https://learn.ml5js.org/#/ 

2) Copy the code into a file **imagenet-1.html**

3) Run the code using a web server (Liveserver etc) and be sure that you have a console log that shows that ml5 has loaded correctly

4) Here are some images you can use [ml-5-images.zip)](_files/ml-5-images.zip)

5) Here is your HTML:

```html
<h1>Image classification using MobileNet</h1>
<p>The MobileNet model labeled this as <span id="result">...</span> with a confidence of <span id="probability">...</span>.</p>
<img id="image" src="ml-5-images/bird.jpg" width="400" />
```

6) Look at - https://learn.ml5js.org/#/reference/image-classifier?id=usage  - to see how we create a new `imageClassifier()` and connect it either a pre-existing model or one from Teachable Machine

7) Follow along with the class example

```js
const image = document.querySelector('#image');
const result = document.querySelector('#result');
const probability = document.querySelector('#probability');

// callback version first
let mobilenet = ml5.imageClassifier('MobileNet',modelLoaded);

function modelLoaded(){
	console.log("Model Loaded ... predicting");
  // ...
}
```

8) Once it's working - try it out with some additional images. You should see that it works very well at identifying certain real-world objects and animals, but it's not so good with other things like people, drawings, art etc ..

<hr>

## IV. Adding Drag & Drop

- What would be a nice improvement to this app is to add drag and drop capability, so that a user drag and drop images from the desktop and get a new prediction
 - below is most of the code you'll need
 - you'll need to create a `predict()` function
 - PS - be sure that your colde only creates the `mobilenet` image classifier ***ONCE!***

```js
let mobilenet = ml5.imageClassifier('MobileNet',modelLoaded);

function modelLoaded(){
	console.log("Model Loaded ... predicting");
	predict();
}

function predict(){
	let results = mobilenet.predict(image,predictionComplete);
}

function predictionComplete(error,results){
	if(error){
		console.log(error);
	}else{
		console.log(results);
		result.innerHTML = results[0].label;
		probability.innerHTML = results[0].confidence.toFixed(4);
	}
}


// drag/drop
const dropbox = document.querySelector("#image");
dropbox.ondragover = onDragover;
dropbox.ondrop = onDrop;

function onDragover(e){
  e.stopPropagation();
  e.preventDefault();
  e.target.classList.add("hover");
}

function onDrop(e){
  e.stopPropagation();
  e.preventDefault();
  e.target.classList.remove("hover");
  const fileList = e.dataTransfer.files;
  readImage(fileList[0]);
}

function readImage(file){
  const reader = new FileReader();
  reader.onload = e => {
    const base64Image = e.target.result;
    dropbox.src = base64Image;
    predict();
  };
  reader.readAsDataURL(file);
}
```

<hr>

## V. Resources
- https://ml5js.org/
- https://github.com/ml5js/ml5-library/tree/main/examples/javascript
- https://wiki.pathmind.com/neural-network#define
