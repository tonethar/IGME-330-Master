# 1 - Machine Learning with ml5 - Image Classification

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
- Another technique is *transfer learning* - which is the reuse of a pre-trained model on a new problem - which is actually what Teachable Machine is doing
- The trained model is only as "good" as the dataset it's given:
  - https://towardsdatascience.com/a-dataset-is-a-worldview-5328216dd44d
  - ml5 has a *Model and Data Provenance* section for all of the models it uses - https://learn.ml5js.org/#/reference/image-classifier?id=model-and-data-provenance


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

5) Here is your HTML (put it before the `<script>` tag):

```html
<h1>Image classification using MobileNet</h1>
<p>The MobileNet model labeled this as <span id="result">...</span> with a confidence of <span id="probability">...</span>.</p>
<img id="image" src="ml-5-images/bird.jpg" width="400" />
```

6) Look at - https://learn.ml5js.org/#/reference/image-classifier?id=usage  - to see how we create a new `imageClassifier()` and connect it either a pre-existing model or one from Teachable Machine

7) Follow along with this example - here's the code that will get you started - add this to **imagenet-1.html**:

```js
const image = document.querySelector("#image");
const result = document.querySelector("#result");
const probability = document.querySelector("#probability");

let mobilenet = ml5.imageClassifier("MobileNet",modelLoaded);

function modelLoaded(){
  console.log("Model Loaded ... predicting");
  // ...
}
```

- In class, we'll add some code that makes a prediction and then displays the results

8) Once it's working - try it out with some additional images. You should see that it works very well at identifying certain real-world objects and animals, but it's not so good with other things like people, drawings, art etc ..

<hr>

## IV. Adding Drag & Drop

- What would be a nice improvement to this app is to add drag and drop capability, so that a user drag and drop images from the desktop and get a new prediction
 - below is most of the code you'll need
 - make a copy of **imagenet-1.html** and name it  **imagenet-2.html**, and add the following to the bottom
 - you'll need to create a `predict()` function
 - PS - be sure that your code only creates the `mobilenet` image classifier ***ONCE!***

```js
// drag & drop
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

- And here is some CSS that the drag/drop is using:

```html
<style>
.hover{
  border:1px solid coral;
  opacity: .7;
}
</style>
```

<hr>

## V. Resources/Readings
- https://ml5js.org/
- https://github.com/ml5js/ml5-library/tree/main/examples/javascript - all ml5 examples (in VanillaJS)
- https://wiki.pathmind.com/neural-network#define
- https://en.wikipedia.org/wiki/List_of_datasets_for_machine-learning_research
- Humans of AI (Editorial Essay) by Philipp Schmitt: https://humans-of.ai/editorial/
- Excavating AI by Kate Crawford and Trevor Paglen: https://www.excavating.ai/
- Many thanks to [Coding Train YouTube Playlist - A Beginner's Guide to Machine Learning with ml5.js](https://www.youtube.com/watch?v=jmznx0Q1fP0&list=PLRqwX-V7Uu6YPSwT06y_AEYTqIwbeam3y) - an intro to ml5 using p5

<hr><hr>

**[Next Chapter -> 2 - Machine Learning with ml5 - Object Detection](2-ml-object-detection.md)**
