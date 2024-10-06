---
title: 'OpenCV 使用前置攝影機'
date: 2023-08-06 14:51:43
categories:
tags:
    - 'Python'
    - 'OpenCV'
---
```py
import cv2 as cv
cam = cv.VideoCapture(0)

while True:
    ret, frame = cam.read()
    cv.imshow('cam',frame)
    if cv.waitKey(1)==ord('q'):
        break

cam.release()
cv.destroyAllWindows()
```