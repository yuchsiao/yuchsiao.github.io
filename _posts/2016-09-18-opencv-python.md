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

