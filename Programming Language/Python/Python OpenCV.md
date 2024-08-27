#python 

<iframe width="560" height="315" src="https://www.youtube.com/embed/oXlwWbU8l2o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

[[NumPy]]

> [!NOTE] Why OpenCV use BGR instead of RGB
OpenCV reads in images in BGR format because **when OpenCV was first being developed, BGR color format was popular among camera manufacturers and image software providers**. The main difference between RGB versus BGR is the arrangement of the subpixels for Red, Green, and Blue.

### Installation
``` shell
# Complete Package
pip install opencv-contrib-python

# Main module
pip install opencv-python
```

> [!NOTE] 
> Install 4.5.5 - version if auto-complete is not working.

``` python
import cv2 as cv  
```

### Reading Image

```python
img = cv.imread('/Users/userName/Downloads/20230302-225351.jpeg')  

cv.imshow('title_name', img)  

cv.waitKey(0) # wait key to be pressed, 0 → infinite time
```

![[open-cv-1.png | 300]]

### Reading Video
``` python
# index of video capture device, e.g. webcam conncected to the computer
cv.VideoCaptur(0)

# path of the video file
capture = cv.VideoCapture("/Users/userName/Downloads/飞书20220509-193136.mp4")  

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

blank = np.zeros(img.shape, dtype='uint8') # create a blank with same width & height as img

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

### Draw Shape & Text

```python
# border
cv.rectangle(blank, (0,0), (250, 250), (0, 255, 0), thickness=2)

# filled
cv.rectangle(blank, (0,0), (250, 250), (0, 255, 0), thickness=-1)
cv.rectangle(blank, (0,0), (250, 250), (0, 255, 0), thickness=cv.FILLED)

# circle
cv.circle(blank, (200, 200), 100, (0,0,255), thickness=3)
# image, center, radius, color, border / fill

# line
cv.line(blank, (0,0), (100, 100), (0, 255, 0), thickness=10)
# image, start point, end point, color, border

# Text
cv.putText(blank, "Hello", (225, 225), cv.FONT_HERSHEY_COMPLEX, 1.0, (255, 255, 255), 2)
# image, text, start point, fontface, scale, color, thickness
```

border|filled
---|---
![[rectangle-border.png]]|![[rectangle-filled.png]]

Circle|Line|putText
---|---|---
![[python-cv-circle.png]]|![[python-cv-line.png]]|![[python-cv-putText.png]]


### 
```python
img = cv.imread('sd.png')

# Greyscale image
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)

# Blur image
blur = cv.GaussianBlur(img, (9, 9), cv.BORDER_DEFAULT)
# kernel size

canny = cv.Canny(img, 125, 125)

# dilating the image
dilated = cv.dilate(canny, (7,7), iterations=3)

cv.imshow('Show', gray)
cv.waitKey(0)
```

greyscale|blur|canny(Edge)|canny + dilate
---|---|---|---
![[gray.png]]|![[blur.png]]|![[canny.png]]|![[dilated.png]]

Resize
```python
resized = cv.resize(img, (100, 200))
# des size → (100, 200)

resized = cv.resize(img, (100, 200), interpolation=cv.INTER_CUBIC)
# default interpolation cv.INTER_AREA 
# linear, cubic (slow, best)
```

Crop
```python
cropped = img[50:200, 200:400]
```

### Image Transformation

translation
```python
def translate(_img, x, y):
	transMat = np.float32([[1,0,x], [0,1,y]])
	dimensions = (_img.shape[1], _img.shape[0])
	return cv.warpAffine(_img, transMat, dimensions)
  
translated = translate(img, 100, 100)
cv.imshow('translation', translated)
```

rotation
```python
def rotate(img, angle, rotPoint=None):
	(height, width) = img.shape[:2]
	if rotPoint is None:
		rotPoint = (width//2, height//2)

	rotMat = cv.getRotationMatrix2D(rotPoint, angle, 1.0) # rotation point, angle, scale
	dimensions = (width,height)

	return cv.warpAffine(img, rotMat, dimensions)

rotated = rotate(img, 30)
cv.imshow('rotated', rotated)
```

flip
```python
fliped = cv.flip(img, 0) # vertical
fliped = cv.flip(img, 1) # horizontal
fliped = cv.flip(img, -1) # vertical & horizontal

cv.imshow('fliped', fliped)
```

threshold & contour

contour ≠ edge

1. canny + blur
2. threshold + contour

```python
ret, thresh = cv.threshold(img, 128, 255, cv.THRESH_BINARY)

cv.imshow('threshold', thresh)

contours, hierarachies = cv.findContours(thresh, cv.RETR_LIST, cv.CHAIN_APPROX_SIMPLE)
print(len(contours)) 

cv.drawContours(blank, contours, -1, (0,0,255), 3)
cv.imshow("contour", blank)
```

threshold|contour
---|---
![[python-cv-threshhold.png]]|![[python-cv-contour.png]]


### Color Space Conversion

```python
# rgb
# bgr to rgb
rgb = cv.cvtColor(img, cv.COLOR_BGR2RGB)
cv.imshow('RGB', rgb)

# hsv
# bgr to hsv
hsv = cv.cvtColor(img, cv.COLOR_BGR2HSV)
cv.imshow('HSV', hsv)

# bgr to lab
lab = cv.cvtColor(img, cv.COLOR_BGR2LAB)
cv.imshow('LAB', lab)
```

### Channel

```python
# split channel
b,g,r = cv.split(img)

# img.shape → (height, width, 3) 3 channels
# b.shape → (height, width) 1 channel

# merge channel
merged = cv.merge([b,g,r])
```

### Blur

```python
# linear filter → blur all

average = cv.blur(img, (7,7))

gaussianBlur = cv.GaussianBlur(img, (9, 9), cv.BORDER_DEFAULT)

# non-linear filter → Blur noise not content (noise reduce)

medium = cv.medianBlur(img, 3)

bilateralFilter = cv.bilateralFilter(img, 15, )

```

![[median-filter.png]]

### bitewise
``` python
blank = np.zeros((400, 400), dtype="uint8")
rectangle = cv.rectangle(blank.copy(), (30, 30), (370, 370), 255, -1)
circle = cv.circle(blank.copy(), (200, 200), 200, 255, -1)
```

rectangle|circle
---|---
![[bitwise_rectangle.png]]|![[bitwise_circle.png]]

```python
# bitewise AND → intersection
bitwise_and = cv.bitwise_and(rectangle, circle)

# bitewise or → both
bitwise_or = cv.bitwise_or(rectangle, circle)

# bitewise xor → not intersection
bitwise_xor = cv.bitwise_xor(rectangle, circle)

# bitewise not
bitwise_not = cv.bitwise_not(rectangle, circle)
```

and|or|xor|not
---|---|---|---
![[bitwise_and.png]]|![[bitwise_or.png]]|![[bitwise_xor.png]]|![[bitwise_not.png]]

### Mask

image and mask image dimension must be same

```python
# create the same size blank image
img_size_blank = np.zeros(img.shape[:2], dtype="uint8")

# draw a center circle
circle = cv.circle(img_size_blank, (img_size_blank.shape[1]//2, img_size_blank.shape[0]//2), 200, 255, -1)

masked = cv.bitwise_and(img, img, mask=circle)
cv.imshow("masked", masked)
```

![[python-cv-circle-masked.png|300]]

Histogram 
```python
hist = cv.calcHist([img], [0], None, [256], [0, 256])
# img, channel, mask, histSize,

plt.plot(hist)
plt.show()
```