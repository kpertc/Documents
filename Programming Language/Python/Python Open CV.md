#python 

<iframe width="560" height="315" src="https://www.youtube.com/embed/oXlwWbU8l2o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

[[NumPy]]

Complete Package → `opencv-contrib-python`
Main module → `opencv-python`


> [!NOTE] 
> Install 4.5.5 - version if auto-complete is not working.

``` python
import cv2 as cv  
```

### Reading Image

```python
img = cv.imread('/Users/bytedance/Downloads/20230302-225351.jpeg')  

cv.imshow('title_name', img)  

cv.waitKey(0) # wait key to be pressed, 0 → infinite time
```

![[open-cv-1.png | 300]]

### Reading Video
``` python
# index of video capture device, e.g. webcam conncected to the computer
cv.VideoCaptur(0)

# path of the video file
capture = cv.VideoCapture("/Users/bytedance/Downloads/飞书20220509-193136.mp4")  

# continously reading frames
while True:  
    isTrue, frame = capture.read() # read single frame
    cv.imshow('video', frame)  
  
    if cv.waitKey(20) & 0xFF==ord('d'): # if D is pressed
        break
        
# Release the video capture object and close any open windows
capture.release()
cv.destroyAllWindows()
```

> [!failure] error: (-215:Assertion failed)
> 1. can not find file
> 2. run out of frame

### Resize & Rescale Images & Video

`cv.resize()`

```python
def rescaleFrame(frame, scale=0.75): # default scale 0.75
	width = int(frame.shape[1] * scale)
	height = int(frame.shape[0] * scale)
	dimensions = (width, height)
	
	return cv.resize(frame, dimensions, interpolation=cv.INTER_AREA)

resizedFrame = rescaleFrame(frame)
```

Video only


### Draw Shape

##### Draw blank image
```python
import numpy as np
```

```python
blank = np.zeros((500, 500), dtype='uint8')
blank = np.zeros((500, 500, 3), dtype='uint8') # 3 → set 3 color channel

blank[:] = 0, 0, 255 # set all pixel to red
blank[200:300, 300:400] = 0, 0, 255 # set ranges of pixel to red

cv.imshow('blank', blank)
cv.waitKey(0)
```

Get shape width & height
```python
blank.shape[0] # width
blank.shape[1] # height
```

set all pixel to red|set ranges of pixel to red
---|---
![[all-red.png]]|![[range.png]]

### Draw Rectangle

```python
# border
cv.rectangle(blank, (0,0), (250, 250), (0, 255, 0), thickness=2)

# filled
cv.rectangle(blank, (0,0), (250, 250), (0, 255, 0), thickness=-1)
cv.rectangle(blank, (0,0), (250, 250), (0, 255, 0), thickness=cv.FILLED)
```

border|filled
---|---
![[rectangle-border.png]]|![[rectangle-filled.png]]

###

