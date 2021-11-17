# 2 - Machine Learning with ml5 - Object Detection

## I. Overview
- The [ml5 Object Detector API](https://learn.ml5js.org/#/reference/object-detector) can detect multiple specific objects in an image, and give us an `x`, `y`, `width`, `height` and a `confidence` value for each object
- For a model, we will use the Microsoft [COCO - Common Objects in Context](https://cocodataset.org/#explore) - which contains "complex everyday scenes of common objects in their natural context"
- What is the COCO Dataset? - https://viso.ai/computer-vision/coco-dataset/
- List of COCO object classes:

`'person', 'bicycle', 'car', 'motorcycle', 'airplane', 'bus', 'train', 'truck', 'boat', 'traffic light', 'fire hydrant', 'stop sign', 'parking meter', 'bench', 'bird', 'cat', 'dog', 'horse', 'sheep', 'cow', 'elephant', 'bear', 'zebra', 'giraffe', 'backpack', 'umbrella', 'handbag', 'tie', 'suitcase', 'frisbee', 'skis','snowboard', 'sports ball', 'kite', 'baseball bat', 'baseball glove', 'skateboard', 'surfboard', 'tennis racket', 'bottle', 'wine glass', 'cup', 'fork', 'knife', 'spoon', 'bowl', 'banana', 'apple', 'sandwich', 'orange', 'broccoli', 'carrot', 'hot dog', 'pizza', 'donut', 'cake', 'chair', 'couch', 'potted plant', 'bed', 'dining table', 'toilet', 'tv', 'laptop', 'mouse', 'remote', 'keyboard', 'cell phone', 'microwave', 'oven', 'toaster', 'sink', 'refrigerator', 'book', 'clock', 'vase', 'scissors', 'teddy bear', 'hair drier', 'toothbrush'`

- List of COCO keypoint classes (for poses):

`"nose", "left_eye", "right_eye", "left_ear", "right_ear", "left_shoulder", "right_shoulder", "left_elbow", "right_elbow", "left_wrist", "right_wrist", "left_hip", "right_hip", "left_knee", "right_knee", "left_ankle", "right_ankle"`

<hr>

## II. Creating an Object Detector that utilizes the webcam

- ml5 `ObjectDetector` documentation & code example:
  - https://learn.ml5js.org/#/reference/object-detector
  - https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector/COCOSSD_webcam


<hr>

## XX. Resources
- Docs: https://learn.ml5js.org/#/reference/object-detector
- JS code examples: https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector
- https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector/COCOSSD_single_image
- https://github.com/ml5js/ml5-library/tree/main/examples/javascript/ObjectDetector/COCOSSD_webcam
