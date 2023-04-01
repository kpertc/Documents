#python 

<iframe width="560" height="315" src="https://www.youtube.com/embed/oXlwWbU8l2o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


Complete Package → `opencv-contrib-python`
Main module → `opencv-python`


> [!NOTE] 
> Install 4.5.5 - version if auto-complete is not working.

``` python
import cv2 as cv  
```


> [!failure] error: (-215:Assertion failed)
> 1. can not find file
> 2. run out of frame


### Reading Image

```python
img = cv.imread('/Users/bytedance/Downloads/20230302-225351.jpeg')  

cv.imshow('title_name', img)  

cv.waitKey(0)
```

![[open-cv-1.png | 300]]

### Reading Video
``` python
capture = cv.VideoCapture("/Users/bytedance/Downloads/飞书20220509-193136.mp4")  
  
while True:  
    isTrue, frame = capture.read()  
    cv.imshow('video', frame)  
  
    if cv.waitKey(20) & 0xFF==ord('d'):  
        break
```
