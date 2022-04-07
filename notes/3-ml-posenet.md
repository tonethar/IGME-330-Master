# 3 - Machine Learning with ml5 - Pose Detection

## I. Overview
- **PoseNet** is a machine learning model that allows for Real-time Human Pose Estimation
  - https://learn.ml5js.org/#/reference/posenet

<hr>

## II. API

- The pose data we get back from the API looks like this - an `x`, a `y`, and a `confidence` value for multiple locations of a body
- Below we can see that these lcoations are named:

```json
pose:
  keypoints: (17) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]
  leftAnkle: {x: 599.1597746318416, y: 494.98787727801255, confidence: 0.0012563241180032492}
  leftEar: {x: 453.69841223097035, y: 243.16036951681053, confidence: 0.5885285139083862}
  leftElbow: {x: 656.4851325959083, y: 524.3184439217534, confidence: 0.01574356108903885}
  leftEye: {x: 427.34051656166406, y: 210.8243997180508, confidence: 0.9987946152687073}
  leftHip: {x: 511.92643577486626, y: 513.2484204481548, confidence: 0.0015425400342792273}
  leftKnee: {x: 605.6700555823656, y: 440.8782258386278, confidence: 0.0018843129510059953}
  leftShoulder: {x: 546.5062336606275, y: 383.60506347181274, confidence: 0.9093210697174072}
  leftWrist: {x: 644.0373194356837, y: 507.3040159945358, confidence: 0.005719129927456379}
  nose: {x: 398.29327215944284, y: 233.91148429900295, confidence: 0.999527096748352}
  rightAnkle: {x: 157.13915843444113, y: 498.5294403640213, confidence: 0.0026795780286192894}
  rightEar: {x: 292.11110987088097, y: 235.13465614170417, confidence: 0.9823558926582336}
  rightElbow: {x: 100.91644287109375, y: 499.3624140223641, confidence: 0.016158990561962128}
  rightEye: {x: 361.0062862648574, y: 203.81996600080555, confidence: 0.9998224973678589}
  rightHip: {x: 240.868740156003, y: 515.7029599438382, confidence: 0.0039060795679688454}
  rightKnee: {x: 139.3682766331773, y: 480.2924581446073, confidence: 0.008052365854382515}
  rightShoulder: {x: 189.40683802741975, y: 372.3791877954386, confidence: 0.9166773557662964}
  rightWrist: {x: 125.657828958118, y: 508.26836493228666, confidence: 0.004718870855867863}
  score: 0.37980522320140153
```

- There is also a `skeleton` array that will have values for body locations at the shoulder level or lower

```json
pose: {score: 0.39227001670309725, keypoints: Array(17), nose: {…}, leftEye: {…}, rightEye: {…}, …}
skeleton: Array(1)
  0: Array(2)
    0:
      part: "leftShoulder"
      position: {x: 584.6195324849526, y: 264.7412002504104}
      score: 0.8373012542724609
    1:
      part: "rightShoulder"
      position: {x: 157.6269431800694, y: 254.8937783445366}
      score: 0.9107379913330078
```


<hr>

## III. Code



<hr><hr>

**[Previous Chapter <- 2 - Machine Learning with ml5 - Object Detection](2-ml-object-detection.md)**
