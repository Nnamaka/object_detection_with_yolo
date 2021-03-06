# Object Detection with Yolo
Detect Hand gestures with yolo

<span align="left">
  <img width="600" heigt="300" src="https://github.com/Nnamaka/object_detection_with_yolo/blob/main/Thankyou.png">
</span>

# RoboFlow
Roboflow was used to preprocess and serve my custom dataset for Hand-gestures
<p align="left">
  <img src="https://github.com/Nnamaka/object_detection_with_yolo/blob/main/Roboflow.png">
</p>

# Steps

## Step 1.

Install <a href="https://github.com/ultralytics/yolov5">Yolo</a> from its github repo
<pre>
!git clone https://github.com/ultralytics/yolov5
</pre>
Install its requirments
<pre>
%cd yolov5
%pip install -qr requirements.txt
%pip install -q roboflow
</pre>


## Step 2.

Get Dataset from Roboflow.
Towards the end when you are about done processing your dataset on Roboflow, Your API key is provided with a code snippet.
<pre>
from roboflow import Roboflow
rf = Roboflow(api_key="your api key in here")
project = rf.workspace("gestures-kejav").project("hand_gestures-iwirp")
dataset = project.version(1).download("yolov5")
</pre>

## Step 3.

Train your model
<pre>
!python train.py --img 416 --batch 8 --epochs 150 --data {dataset.location}/data.yaml --weights yolov5s.pt --cache
</pre>

## Step 4.

Evaluate your model to see how its doing. 
Tensorboard can be used to evaluate your Yolo model performance. 
<pre>
%load_ext tensorboard
%tensorboard --logdir runs
</pre>

## Step 5.

Make inference with your model to see how good its predictions are.
<pre>
!python detect.py --weights runs/train/exp/weights/best.pt --img 416 --conf 0.1 --source {dataset.location}/test/images
</pre>

View the results by running the following code
<pre>
import glob
from IPython.display import Image, display

#change your the extension variable to your image type
extension = '.jpg'
for imageName in glob.glob('/content/yolov5/runs/detect/exp/*' + extension):
    display(Image(filename=imageName))
    print("\n")
</pre>


# Conclusion

The Yolo framework has taken care of literally everything from training, evaluation and inference. 
When you clone the Yolo Repo, it comes with utility scripts that takes care of common functionality that the developer would have rather been writting scripts for.
Yolo is a great model to use for custom object detection tasks. The final trained model can be converted further to compatible formats for deployment on Web, Mobile or Edge devices.


# Credit

Credit goes to the YOLO team. Lebelimg and Roboflow.
