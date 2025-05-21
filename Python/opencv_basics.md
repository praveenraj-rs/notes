# opencv_basics
#python

OpenCV Course - Full Tutorial with Python: [youtube](https://youtu.be/oXlwWbU8l2o)
[QR](https://www.google.com/url?sa=t&source=web&rct=j&url=https://practicaldatascience.co.uk/data-science/how-to-read-qr-codes-in-python-using-opencv&ved=2ahUKEwj_jM_7uoX9AhXTRXwKHXZmA1sQFnoECAoQBQ&usg=AOvVaw0X0zxlJ5SQgeXQtOMNPRDk)
Humanoid Club: [GitHub](https://github.com/KushKumarK/HumanoidX-Computer_Vision#check-the-drive-link-given-in-the-txt-file-in-the-files-section) 

# Syllabus
Basics
1. Reading Images and Video
2. Image Transformations
3. Drawing Shapes
4. Putting Text

Advanced
1. Color Spaces
2. BITWISE operations
3. Masking
4. Histogram Computation
5. Edge Detection

Faces
1. Face Detection
2. Face Recognition
3. Deep Computer Vision

# Basic

## Opencv Installation

**Option1**
Main modules package
>`pip install opencv-python`

**Option2**
Full package (contains both main modules and contrib/extra modules)
>`pip install opencv-contrib-python` 

check contrib/extra modules listing from [OpenCV documentation](https://docs.opencv.org/master/)

**Option3** 
Headless main modules package: 
>`pip install opencv-python-headless`

**Option4**
Headless full package (contains both main modules and contrib/extra modules)
>`pip install opencv-contrib-python-headless`


## Images and Videos

### Destroy Windows
Python Opencv destroyAllWindows() function allows users to destroy or close all windows at any time after exiting the script. If you have multiple windows open at the same time and you want to close then you would use this function. It doesn’t take any parameters and doesn’t return anything. It is similar to destroyWindow() function but this function only destroys a specific window unlike destroyAllWindows().
```python
destroyAllWindows()
```
### Reading Images
```python
#!/usr/bin/python3
import cv2 as cv
img = cv.imread("cat1.jpeg")
cv.imshow('dog',img)
cv.waitKey(0)
```
![[Pasted image 20230207204936.png]]

### Reading Videos
```python
#!/usr/bin/python3
import cv2 as cv
capture=cv.VideoCapture('cat.mp4')
while True:
    isTrue,frame=capture.read()
    cv.imshow('Video',frame)

    if cv.waitKey(20) & 0xFF==ord('d'):
        break

capture.release()
cv.destroyAllwindows()
```
[[cat.mp4]]

### Live Capture
```python
#!/usr/bin/python3
import cv2
vid = cv2.VideoCapture(0)
while(True):
    ret, frame = vid.read()
    cv2.imshow('frame', frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
vid.release()
cv2.destroyAllWindows()
```

### Resizing Frames
```python
#!/usr/bin/python3
import cv2 as cv

#selecting the image
img = cv.imread('cat1.jpeg')

#function to resize
#works on img,video and live video
def rescaleFrame(frame,scale=0.75):
        width=int(frame.shape[1]*scale)
        height=int(frame.shape[0]*scale)
        dimension=(width,height)
        return cv.resize(frame,dimension,interpolation=cv.INTER_AREA)

#rescaling a image
rescale_img=rescaleFrame(img,0.5)
cv.imshow('cat_rescaled',rescale_img)
cv.waitKey(0)
```

### Blank Image
```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500),dtype='uint8')
cv.imshow('Blank',blank)
cv.waitKey(0)
```
![[Pasted image 20230207204850.png]]

### Paint the Image
```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500,3),dtype='uint8')
cv.imshow('Blank',blank)

#creating green image
blank[:]=0,255,0
cv.imshow('Green',blank)

#creating red image
blank[:]=0,0,255
cv.imshow('Red',blank)

cv.waitKey(0)
```
![[Pasted image 20230205105943.png]]

### Rectangle Box
```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500,3),dtype='uint8')
cv.imshow('Blank',blank)

#drawing rectangle
cv.rectangle(blank,(0,0),(250,250),(0,255,0),thickness=2)
cv.imshow('Rectangle',blank)
cv.waitKey(0)
```
![[Pasted image 20230206221739.png]]

### Filling Box
```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500,3),dtype='uint8')
cv.imshow('Blank',blank)

#drawing rectangle
cv.rectangle(blank,(0,0),(250,250),(0,255,0),thickness=cv.FILLED)
cv.imshow('Rectangle',blank)
cv.waitKey(0)
```
![[Pasted image 20230206221103.png]]

### Drawing Circle
```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500),dtype='uint8')
cv.imshow('Blank',blank)

#using the circle function
image= cv.circle(blank,(120,50),50,(255,0,0),thickness=1)
cv.imshow('Circle',image)
cv.waitKey(0)
```
![[Pasted image 20230207204752.png]]

### Drawing Line
```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500),dtype='uint8')
cv.imshow('Blank',blank)

#using the Line function
image= cv.line(blank,(120,50),(50,120),(255,0,0),thickness=1)
cv.imshow('Text',image)
cv.waitKey(0)
```
![[Pasted image 20230207204657.png]]

### Writing Text

```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np

#creating blank image
blank = np.zeros((500,500),dtype='uint8')
cv.imshow('Blank',blank)

#using the Line function
		image= cv.putText(blank,'Hello World',(250,250),cv.FONT_HERSHEY_SIMPLEX,1,(255,0,0),1)
cv.imshow('Text',image)
cv.waitKey(0)
```
![[Pasted image 20230207204626.png]]

## Essential Function

### Grey Scale
```python
#!/usr/bin/python3
import cv2 as cv
img=cv.imread('cat1.jpeg')
gray=cv.cvtColor(img,cv.COLOR_BGR2GRAY)
cv.imshow('Gray',gray)
cv.waitKey(0)
```
![[Pasted image 20230207204440.png]]

### Blur
```python
#!/usr/bin/python3
import cv2 as cv
img=cv.imread('cat1.jpeg')
blur=cv.GaussianBlur(img,(7,7),cv.BORDER_DEFAULT)
cv.imshow('Blur',blur)
cv.waitKey(0)
```
![[Pasted image 20230207204352.png]]

### Edge Cascade
```python
#!/usr/bin/python3
import cv2 as cv
img=cv.imread('cat1.jpeg')
canny=cv.Canny(img,125,175)
cv.imshow('Edge Cascade',canny)
cv.waitKey(0)
```
![[Pasted image 20230207204257.png]]

### Dilating The Image
Dilation adds pixels to the boundaries of objects in an image, while erosion removes pixels on object boundaries.
```python
#!/usr/bin/python3
import cv2 as cv
img=cv.imread('cat1.jpeg')
canny=cv.Canny(img,125,175)
cv.imshow('Edge Cascade',canny)
dilated=cv.dilate(canny,(5,5),iterations=3)
cv.imshow("Dilated",dilated)
cv.waitKey(0)
```
![[Pasted image 20230207233039.png]]

### Eroded Image
```python
#!/usr/bin/python3
import cv2 as cv

img=cv.imread('cat1.jpeg')
canny=cv.Canny(img,125,175)
cv.imshow('Edge Cascade',canny)
  
dilated=cv.dilate(canny,(5,5),iterations=3)
cv.imshow("Dilated",dilated)
  
eroded=cv.erode(dilated,(5,5),iterations=3)
cv.imshow("Eroded Image",eroded)
cv.waitKey(0)
```
![[Pasted image 20230207233632.png]]

### Resize
```python
#!/usr/bin/python3
import cv2 as cv
img = cv.imread("cat1.jpeg")
cv.imshow('dog',img)
cv.waitKey(0)

resized=cv.resize(img,(500,250))
cv.imshow('Resized Cat Image',resized)
```
![[Pasted image 20230207234148.png]]

### Cropping
```python
#!/usr/bin/python3
import cv2 as cv
img = cv.imread("cat1.jpeg")
cv.imshow('dog',img)
cv.waitKey(0)

cropped=img[50:100,50:100]
cv.imshow('Cropped Image',resized)
```
![[Pasted image 20230207234956.png]]

### Translate Image
```python
import cv2 as cv
import numpy as np

img = cv.imread('cat1.jpeg')
cv.imshow('Cat',img)

def translate(img,x,y):
    transMat=np.float32([[1,0,x],[0,1,y]])
    dimensions = (img.shape[1],img.shape[0])
    return cv.warpAffine(img,transMat,dimensions)
  
translated = translate(img,100,100)
cv.imshow("Translated",translated)
cv.waitKey(0)
```
![[Pasted image 20230209193900.png]]

### Rotating Image

```python
import cv2 as cv
import numpy as np

img = cv.imread('cat1.jpeg')
cv.imshow('Cat',img)
  
def rotate(img, angle, rotPoint=None):
    (height,width)=img.shape[:2]
    
    if rotPoint is None:
        rotPoint=(width//2 ,height//2)
    rotMat = cv.getRotationMatrix2D(rotPoint,angle,1.0)
    dimensions = (width,height)
    
    return cv.warpAffine(img, rotMat, dimensions)
    
rotated = rotate(img,90)
cv.imshow('Rotated',rotated)
cv.waitKey(0)
```
![[Pasted image 20230209195402.png]]

### Flipping Image
```python
#!/usr/bin/python3
import cv2 as cv
img = cv.imread("cat1.jpeg")
cv.imshow('Cat',img)

flipped = cv.flip(img,0)
cv.imshow('Flipped',flipped)
cv.waitKey(0)

```
![[Pasted image 20230209200001.png]]


## Color Spaces

### Grey Scale
![[#Gray Scale]]

### BGR Image

```python
#!/usr/bin/python3
import cv2 as cv
img = cv.imread("cat1.jpeg")
cv.imshow('dog',img)
cv.waitKey(0)
```

![[Pasted image 20230301225616.png]]

### HSV Image

```python
import cv2 as cv
img = cv.imread('cat1.jpeg')
hsv = cv.cvtColor(img,cv.COLOR_BGR2HSV)
cv.imshow('HSV',hsv)
cv.waitKey(0)
```

![[Pasted image 20230301224854.png]]


### LAB Image

```python
import cv2 as cv
img = cv.imread('cat1.jpeg')
lab = cv.cvtColor(img,cv.COLOR_BGR2LAB)
cv.imshow('LAB',lab)
cv.waitKey(0)
```

![[Pasted image 20230301224800.png]]


### RGB Image

```python
import cv2 as cv
img = cv.imread('cat1.jpeg')
rgb = cv.cvtColor(img,cv.COLOR_BGR2RGB)
cv.imshow('RGB',rgb)
cv.waitKey(0)
```

![[Screenshot from 2023-03-01 22-45-34.png]]

## Color Channel

### Red, Blue and Green
```python
import cv2 as cv
img = cv.imread('bgr_flag.png')
b,g,r = cv.split(img)
  
cv.imshow('Blue',b)
cv.imshow('Green',g)
cv.imshow('Red',r)
  
merged = cv.merge([b,g,r])
cv.imshow('Merged Img',merged)
cv.waitKey(0)
```

![[Pasted image 20230301232300.png|200]]  ![[Pasted image 20230301232327.png|200]]   ![[Pasted image 20230301232355.png|200]]

![[Pasted image 20230301232427.png|300]]



## Blurring

### Average Blur

```python
import cv2 as cv
img = cv.imread('cat1.jpeg')
average = cv.blur(img,(7,7))
cv.imshow('Average Blur',average)
cv.waitKey(0)
```

![[Pasted image 20230302103927.png|500]]


### Gaussian Blur

![[#Blur]]

### Median Blur

```python
import cv2 as cv
img = cv.imread('cat1.jpeg')
med_blur = cv.medianBlur(img,7)
cv.imshow('Median Blur',med_blur)
cv.waitKey(0)
```

![[Pasted image 20230302104720.png|300]]


### Bilateral Blur

```python
import cv2 as cv
img = cv.imread('cat1.jpeg')
bilater = cv.bilateralFilter(img,100,35,15)
cv.imshow('Bilater Blur',bilater)
cv.waitKey(0)
```

![[Pasted image 20230302110332.png|300]]


## Bitwise Operation in Images

### Rectangle and Cirlce

```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np
  
#creating blank image
blank = np.zeros((400,400),dtype='uint8')
cv.imshow('Blank',blank)
  
# creating rectangle and circle
rectangle = cv.rectangle(blank.copy(),(30,30),(370,370),255,-1)
cirle = cv.circle(blank.copy(),(200,200),200,255,-1)
  
cv.imshow('Rectangle',rectangle)
cv.imshow('Circle',cirle)
cv.waitKey(0)
```

![[Pasted image 20230302112153.png|200]]  ![[Pasted image 20230302112221.png|200]]  ![[Pasted image 20230302112625.png|200]]

### AND, OR, XOR

```python
#!/usr/bin/python3
import cv2 as cv
import numpy as np
  
#creating blank image
blank = np.zeros((400,400),dtype='uint8')
  
# creating rectangle and circle
rectangle = cv.rectangle(blank.copy(),(30,30),(370,370),255,-1)
cirle = cv.circle(blank.copy(),(200,200),200,255,-1)
  
bw_and = cv.bitwise_and(rectangle,cirle) # AND Operation
bw_or = cv.bitwise_or(rectangle,cirle) # OR Operation
bw_xor = cv.bitwise_xor(rectangle,cirle) # XOR Operation
bw_not = cv.bitwise_not(cirle) # NOT Operation
  
cv.imshow('AND',bw_and)
cv.imshow('OR',bw_or)
cv.imshow('XOR',bw_xor)
cv.imshow('NOT',bw_not)
  
cv.waitKey(0)
```

![[Pasted image 20230302115756.png|200]]  ![[Pasted image 20230302115822.png|200]]  ![[Pasted image 20230302115838.png|200]]
![[Pasted image 20230302115853.png|200]]

## Masking Image

### Circle Mask

```python
import cv2 as cv
import numpy as np

img = cv.imread('cat1.jpeg')
blank = np.zeros(img.shape[:2],dtype='uint8')
mask = cv.circle(blank,(img.shape[1]//2,img.shape[0]//2),100,255,-1)

masked = cv.bitwise_and(img,img,mask=mask)
cv.imshow('Real Image',img)
cv.imshow('Masked Image',masked)
cv.waitKey(0)
```

![[Pasted image 20230302170721.png|300]]   ![[Pasted image 20230302170739.png|300]]

## Histogram

### GrayScale Histogram

```python
#!/usr/bin/python3
import cv2 as cv
import matplotlib.pyplot as plt
  
img=cv.imread('cat1.jpeg')
gray=cv.cvtColor(img,cv.COLOR_BGR2GRAY)
gray_hit = cv.calcHist([gray],[0],None,[256],[0,256])
  
plt.figure()
plt.title('GrayScle histogram')
plt.xlabel('Bins')
plt.ylabel('# of pixels')
plt.plot(gray_hit)
plt.xlim([0,256 ])
plt.show()
  
cv.waitKey(0)
```

![[Pasted image 20230302182105.png|300]]


## Face Detection

### Haarcascade

[code_copy](https://github.com/opencv/opencv/blob/4.x/data/haarcascades/haarcascade_frontalface_default.xml)

```python
import cv2 as cv
img = cv.imread('face2.jpeg')
gray = cv.cvtColor(img,cv.COLOR_BGR2GRAY)
  
haar_cascade = cv.CascadeClassifier('haar_face.xml')
faces_rect = haar_cascade.detectMultiScale(gray,scaleFactor=1.1,minNeighbors=3)
  
print(f'Number of Faces: {len(faces_rect)}')
for (x,y,w,h) in faces_rect:
cv.rectangle(img,(x,y),(x+w,y+h),(0,255,0),2)
  
cv.imshow('Face',img)
cv.waitKey(0)
```

> Number Faces :  5
![[Pasted image 20230302201428.png|500]]


### Real Time Face Detection
```python
import cv2 as cv
  
haar_cascade = cv.CascadeClassifier('haar_face.xml')
  
capture = cv.VideoCapture(0)
while True:
	boolean,frame = capture.read()
	if boolean==True:
		gray = cv.cvtColor(frame,cv.COLOR_BGR2GRAY)
		coordinates = haar_cascade.detectMultiScale(gray,scaleFactor=1.1,minNeighbors=3)
  
		for (x,y,w,h) in coordinates:
			cv.rectangle(frame,(x,y),(x+w,y+h),(0,255,0),2)
			cv.imshow('Live',frame)
  
		if cv.waitKey(20) == ord('x'):
			break
capture.release()
cv.destroyAllWindows()
```

![[Pasted image 20230302222222.png|500]]

