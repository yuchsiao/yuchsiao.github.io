---
title: OpenCV in Python
tags: [opencv, computer-vision]
---

OpenCV is great, but it is not so great with the documentation for its Python binding.

Certainly, there are [resourses](http://docs.opencv.org/3.0-beta/modules/refman.html) and
[tutorials](http://docs.opencv.org/3.0-beta/doc/py_tutorials/py_tutorials.html), 
but overall, Python is at most a second-class citizen in the OpenCV world 
due to lack of many API supports (e.g. missing many algorithm interface [here](http://docs.opencv.org/3.0-beta/modules/features2d/doc/feature_detection_and_description.html).
The upside is: Python may also not need some of them either (e.g. the machine learning part can resort to `sklearn`).
The strategy of OpenCV in Python then becomes "identify useful things or find alternatives" until satisfying the need.

This article aims to fit some of such gaps for newbies.

## Error Control

It seems not stated explicitly, but the Python binding has an exception class called `cv2.error`.
The class is not following the overall OpenCV Python binding naming convention so it may be subject to change in the future.

## Display in Jupyter Notebook

### Image

One can use the `imshow` function from `matplotlib.pyplot`: 

```python
import matplotlib.pyplot as plt
import cv2

img_bgr = cv2.imread('sample.jpg')  # OpenCV default: BGR
img_rgb = cv2.cvtColor(cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
plt.axis('off')
plt.show()
```

Note that OpenCV default is BGR for some history reason, whereas `plt.imshow` is in the RGB order.
`cv2.imshow`, on the other hand, is consistent with `cv2.imread` in the BGR order.


### Video

Use ipython magic `clear_output(wait=True)` to update frame

```python
from IPython.display import clear_output
import cv2
import numpy as np
import sys

vid = cv2.VideoCapture(0)

try:
    while(True):
        # Capture frame-by-frame
        ret, frame = vid.read()
        if not ret:
            raise cv2.error("Camera failed to capture")

        # Convert the image from OpenCV BGR format to matplotlib RGB format
        # to display the image
        frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
        
        plt.axis('off')  # Turn off the axis
        plt.imshow(res)
        plt.show()

        # Display the frame until new frame is available
        clear_output(wait=True)
        
except KeyboardInterrupt:
    sys.stdout.write("Keyboard Interrupt\n")
except cv2.error as e:
    sys.stderr.write("{}\n".format(e))
finally:
    vid.release()
    # Message to be displayed after releasing the device
    sys.stdout.write("Release Video Resource\n")

```
