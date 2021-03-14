# Project: Automatic Signal Detector

## Main goal: detect the face in real-time from the camera in an optimized way.

The first part of the project contains the face detection based on cascades, located in file *haarcascade_frontalface_default.xml*, which is loaded directly from the github with *wget* command. 

As a source for the face detection, the image is taken from the camera in the real time using js library. 
To optimize the search in order to not to search through the whole image area, we are introducing the function *compute_optimized_search_region()*, which will compute the sub-region in which we want to detect the face. The subregion is a red square, and face area is a green square, expected to be inside the red square. 

Besides that, we are also limiting the search area by the image dimensions, so that the sub-region didn't go beyond the image borders. 


### Main libraries:
1. OpenCV (cv2) - OpenCV-Python is a library of Python bindings designed to solve computer vision problems.
2. eval_js - Translates JavaScript to Python code. Js2Py is able to translate and execute virtually any JavaScript code.
3. Javascript - js library used for readin the image from the camera in real-time 
4. NumPy - a Python library that provides a simple yet powerful data structure: the n-dimensional array. 

### Second part of the project includes Meanshift and Camshift algorithms to track objects in videos (live stream from camera in this case)

We are going to try Meanshift and then as it's not perfect for our tesk with moving back and forth target, we will try Camshift. After this we will remove the face area and will try to detect the hand, as it's supposed to have the same hystogram as our face. 
Steps:

**Meanshift**

1. First we need to setup the target, it is our face. In our case we select a bounding box around the face, and we use function detect_faces(), which using cascades detects a face area. We confirm the selected bounding box.
2. Then we find the histogram of the face so that we can backproject the target on each frame for calculation of meanshift. For histogram, only Hue is considered
3. To avoid false values due to low light, low light values are discarded using cv2.inRange() function. We use this mask to take into account only pixels which are not too bright and not too dark.

**CamShift**

So, the main issue with Meanshift that it doesn't change dynamically the rectangle of detected area, which is not great when the object moves back and forth. That's why we will use the CamShift, the idea behind it is: it applies meanshift first, once meanshift converges, it updates the size of the window.

