# Machine Learning with ml5 - pre-trained models

## I. What is Machine Learning

- "A field of study that gives computers the ability to learn without being explicitly programmed" - [Arthur Samuel](https://en.wikipedia.org/wiki/Arthur_Samuel)
- https://en.wikipedia.org/wiki/Machine_learning
- We will be looking at the [ml5](https://ml5js.org/) machine learning API
  - this API "wraps" Tensorflow (which you have probably heard of) and makes model loading and training new models easier
- Components of Machine Learning: 
 - 1. Algorithms  - "neural network"
 - 2. Models - they can be *pre-trained* like ImageNet (which we will use today) or we can train them ourselves (for example with [Teachable Machine](https://teachablemachine.withgoogle.com/))
 - 3. Datasets
   - we will be looking at *supervised learning* in this class - which makes use of *labeled* datasets where we provide the API with training data that consists of an *input* (for example a "vectorized" image or piece of text) and the desired *output* value (ex. a label such as "dog") 
- The trained model is only as "good" as the dataset it's given:
  - https://towardsdatascience.com/a-dataset-is-a-worldview-5328216dd44d
- Another technique is *transfer learning* - which is the reuse of a pre-trained model on a new problem - which is actaully what Teachable Machine is doing

<hr>

## II. Image Classification with MobileNet

- Using a pre-trained model like MobileNet  - it only has a finite number of images it was trained with - https://github.com/ml5js/ml5-library/blob/main/src/utils/IMAGENET_CLASSES.js
- https://www.image-net.org/index.php

<hr>

## III. Get Started

1) Head to **Quickstart: Plain JavaScript** here: https://learn.ml5js.org/#/ 

2) Copy the code into a file **imagenet-1.html**

3) Run the code using a web server (Liveserver etc) and be sure that you have a console log that shows that ml5 has loaded correctly

4) Look at - https://learn.ml5js.org/#/reference/image-classifier?id=usage  - to see how we create a new `imageClassifier()` and connect it either a pre-existing model or one from Teachable Machine

5) Follow along with the class example

- Here are some images you can use [ml-5-images.zip)](_files/ml-5-images.zip)

<hr>

## IV. Resources
- https://ml5js.org/
- https://github.com/ml5js/ml5-library/tree/main/examples/javascript
