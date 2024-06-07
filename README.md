# Hand Gesture Recognition using Google MediaPipe
This is a sample program that recognizes various hand gestures with a simple Multi-layer Perceptron using the detected key points
<br> 

This repository consists of the following contents
* Sample program
* Hand gesture recognition model (TFLite)
* Learning data for hand gesture recognition and notebook for learning

# Requirements
* MediaPipe
* OpenCV
* Tensorflow
* Scikit-learn<br>
This is how to install the dependencies
```bash
pip install -r requirements.txt
```

# Demo
This is how to run the demo using your web cam
```bash
python app.py
```
The following options can be specified when running the demo
* --device<br>Specifying the camera device number (Default: 0)
* --height<br>Height at the time of camera capture (Default: 1080)
* --width<br>Width at the time of camera capture (Default: 1920)
* --use_static_image_mode<br>Whether to use static_image_mode option for MediaPipe inference (Default: Unspecified)
* --min_tracking_confidence<br>Tracking confidence threshold (Default: 0.5)
* --min_detecting_confidence<br>Detection confidence threshold (Default: 0.5)

# Directory
<pre>
app.py
keypoint_classification.ipynb
data
    keypoint_classifier_label.csv
    keypoint.csv
model
    keypoint_classifier.keras
    keypoint_classifier.py
    keypoint_classifier.tflite
utils
    fps_calculation.py
</pre>

### app.py
This is a sample program for inference.<br>
In addition, it collects learning data (key points) for hand gesture recognition<br>

### keypoint_classification.ipynb
This is a model training script for hand gesture recognition

### model
This directory stores files related to hand gesture recognition.<br>
The following files are stored:
* Trained model (keypoint_classifier.tflite)
* Inference module (keypoint_classifier.py)

### data
This directory stores data related to hand gesture recognition.<br>
The following files are stored:
* Label data (keypoint_classifier_label.csv)
* Training data (keypoint.csv)

### utils/fps_calculation.py
This is a module for FPS determination

# Training
You can add and change training data, as well as retrain the model

### 1. Learning data collection
Press "k" to enter the mode to save key points (displayed as [MODE:Logging Key Point]) <br>
<img src="https://user-images.githubusercontent.com/37477845/102235423-aa6cb680-3f35-11eb-8ebd-5d823e211447.jpg" width="60%"><br><br>
If you press "0" to "9", the key points will be added to "data/keypoint.csv" as shown below.<br>
First column: Pressed number (used as class ID), second and subsequent columns: Key point coordinates<br>
<img src="https://user-images.githubusercontent.com/37477845/102345725-28d26280-3fe1-11eb-9eeb-8c938e3f625b.png" width="80%"><br><br>
The key point coordinates are the ones that have undergone the following preprocessing.<br>
<img src="https://user-images.githubusercontent.com/37477845/102242918-ed328c80-3f3d-11eb-907c-61ba05678d54.png" width="80%">
<img src="https://user-images.githubusercontent.com/37477845/102244114-418a3c00-3f3f-11eb-8eef-f658e5aa2d0d.png" width="80%"><br><br>
In the initial state, 8 types of learning data are included: open sign (class ID: 0), close sign (class ID: 1), thumbs up sign (class ID: 2), thumbs down sign (class ID: 3), peace sign (class ID: 4), okay sign (class ID: 5), pointer sign (class ID: 6), rock n roll sign (class ID: 7).<br>
If necessary, delete the existing data of csv to prepare the training data.<br>

### 2. Model training
Open "[keypoint_classification.ipynb](keypoint_classification.ipynb)" in Jupyter Notebook and execute from top to bottom.<br>
To change the number of training data classes, change the value of "NUM_CLASSES = 8" <br>and modify the label of "data/keypoint_classifier_label.csv" as appropriate.<br><br>

### 3. Model structure
The image of the model prepared in "[keypoint_classification.ipynb](keypoint_classification.ipynb)" is as follows.
<img src="https://user-images.githubusercontent.com/37477845/102246723-69c76a00-3f42-11eb-8a4b-7c6b032b7e71.png" width="50%"><br><br>