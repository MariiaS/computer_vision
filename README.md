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
