# General description
This is the repository of Yudai and Cyrus' Project for CMSC 25422 taught by Prof. Nick Feamster.
Here, we implemented and evaluated different machine learning models to detect spying of webcams via Network traffic.

Please open and run our Jupyter notebook for more details.

# Implementation of Webcam Spy Attack: OpenCV+Flask
To setup the spying conditions, we followed an exisiting implementation [Reference], and implemented our custome web application based on Flask that broadcasts the webcam's live stream to a local network.


## Put appropriate number in cv2.VideoCapture()

``` cv2.VideoCapture(1) ```
change the number until you find the camera.

## Stream to local network via Flask
``` app.run(host='192.168.0.166')```
put your own IP address

# Using and Reading Sphinx
In this project, we use nbsphinx to embed jupyter notebook inside webpages.

## Building the Sphinx Application
First go into the venv. Under /sphinx, run in your terminal:
    source env/bin/activate
Then under /sphinx, run in your terminal:
    sphinx-build -t html source build
Use any web server to hold the webpages built under /sphinx/build

## Accessing the Sphinx Documentation
Under /sphinx/build, open index.html with a live web server. That would be the home page of our sphinx project. You would then be able to access other parts of the documentation.


## [Reference](https://github.com/NakulLakhotia/Live-Streaming-using-OpenCV-Flask)
