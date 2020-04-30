---
title: "Introduction to Fun with Face-Recognition"
date: 2020-03-30
tags: [Face Recognition, Data Science]
header:
  image: "/images/face_rec/titanic.png"
excerpt: "Face Recognition, Data Science"
mathjax: "true"
---
## Table of Content:
1. ["Topic of the"](#try)
2. [""]



## What is facial recognition?
*Facial recognition is a biometric software application capable of uniquely identifying or verifying a person by comparing and analyzing patterns based on the person's facial contours. Facial recognition is mostly used for security purposes, though there is increasing interest in other areas of use. In fact, facial recognition technology has received significant attention as it has potential for a wide range of application related to law enforcement as well as other enterprises.*


### In this note we will talk about:
1. **Face Matching:** *Find the best match for a given face.*
2. **Face Similarity:** *Find faces that are most similar to a given face.*
3. **Face Transformation:** *Generate new faces that are similar to a given face.*


### Step 1: picking your libraries, installing and Importing them.
*Of all the amazing libraries out there I chose to explore **Face_recognition** for its simplicity and easy documentation*

```python
#packages for recognizing faces
!pip install face_recognition
import face_recognition
#packages to manipulate pixel data
import numpy as np
import pandas as pd
#PIL packages to draw on the images
import PIL.Image
import PIL.ImageDraw
import face_recognition
```

### Step 2:  Get an image with faces in it for the purpose.
```python
#load the jpg file
image = face_recognition.load_image_file("../input/facess/lead_720_405.jpg")
#To display the Image
pil_image =PIL.Image.fromarray(image)
pil_image.show()
pil_image
```
The picture I am using here is one of the most famous selfies from Oscar awards. What happy faces :smile:

<img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/download.png" alt="linearly separable data">

### Step 3 - Recognize faces (piece of cake??)
*Great thing about this package is that it has methods that makes things much easier for an introductory level face recognition. It is fun and does not frustrate someone who is new to face recognition.*
```python
# Locating the faces in the image
face_location = face_recognition.face_locations(image)

```
#### Face_location gives us Top, Right, Bottom and Left points of the face to further use in processing. These numbers are pixels locations in the pictures as shown below.
```python
[(184, 494, 339, 339),
 (46, 391, 108, 328),
 (186, 325, 275, 235),
 (5, 494, 80, 419),
 (68, 175, 175, 67),
 (47, 320, 121, 245),
 (128, 629, 235, 521),
 (155, 237, 229, 162),
 (46, 239, 108, 176)]
```

 *Lets count faces in the image that face_recognition could recognition*

 ```python
 number_of_faces = len(face_location)
 print('Number of face found are {}'.format(number_of_faces))
 ```
> Number of face found are 9

### Step 3 - Convert image file to an object so we can work on it:
*Creates an image memory from an object exporting the array interface (using the buffer protocol). If obj is not contiguous, then the to bytes method is called and from buffer() is used*

#### Parameters:
obj – Object with array interface
mode – Mode to use (will be determined from type if None) See: Modes.
#### Returns:
An image object.

*In the for loop we iterate through each recognized face locations and draw rectangales on them using PIL's extensive drawing methods*

```python
#Creating Image obj
pil_image =PIL.Image.fromarray(image)

# Looping through each face
for face_locationn in face_location:
    top, right, bottom, left = face_locationn
    print('A face is located at pixel location Top {}, right {}, bottom {}, left {}'.format(top,right,bottom,left))
    # Drawing Rectangle on each face recognized.
    draw = PIL.ImageDraw.Draw(pil_image)
    draw.rectangle([left,top,right,bottom],outline="red")
```

```python
A face is located at pixel location Top 184, right 494, bottom 339, left 339
A face is located at pixel location Top 46, right 391, bottom 108, left 328
A face is located at pixel location Top 186, right 325, bottom 275, left 235
A face is located at pixel location Top 5, right 494, bottom 80, left 419
A face is located at pixel location Top 68, right 175, bottom 175, left 67
A face is located at pixel location Top 47, right 320, bottom 121, left 245
A face is located at pixel location Top 128, right 629, bottom 235, left 521
A face is located at pixel location Top 155, right 237, bottom 229, left 162
A face is located at pixel location Top 46, right 239, bottom 108, left 17
```

#### This looks amazing. This Library could recognize almost all the faces except for the ones barely visible in the picture.
<img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/rect_face.png" alt="linearly separable data">

### Step 5 - Detecting Face Landmarks:
*In the code notebook so far we could only recognize the face locations but not the actually characteristics of a face.
 Our next attempt would be to recognize the location of landmarks (i.e Chin, Left Eyebrows, Right Eyebrows, Nose Bridge, Nose Tip, left eye, right eye, top lip, bottom lip )*
- We will use face_landmarks method with the image we stored.
- Output should be pixel location points for each landmark.

 ```python
face_landmarks_list = face_recognition.face_landmarks(image)
face_landmarks_list
 ```

```python
[{'chin': [(369, 247),(368, 263),(369, 279),(371, 296),(376, 314),(386, 329),(398, 344),(412, 357),(429, 360),(448, 357),
   (466, 346),
   (483, 334),
   (497, 320),
   (505, 303),
   (506, 283),
   (505, 263),
   (504, 243)],
  'left_eyebrow': [(370, 235), (372, 223), (381, 219), (393, 218), (404, 221)],
  'right_eyebrow': [(427, 220),
   (443, 215),
   (458, 214),
   (472, 218),
   (482, 228)],
  'nose_bridge': [(416, 234), (416, 245), (415, 256), (415, 268)],
  'nose_tip': [(404, 276), (411, 279), (418, 281), (427, 278), (435, 275)],
  'left_eye': [(381, 242),
   (387, 237),
   (394, 237),
   (402, 240),
   (395, 241),
   (387, 242)],
  'right_eye': [(441, 239),
   (449, 234),
   (456, 234),
   (464, 238),
   (457, 239),
   (449, 239)],
  'top_lip': [(394, 298),
   (405, 296),
   (414, 295),
   (423, 297),
   (433, 295),
   (449, 294),
   (465, 296),
   (461, 297),
   (433, 298),
   (423, 300),
   (415, 299),
   (399, 299)],
  'bottom_lip': [(465, 296),
   (451, 312),
   (436, 319),
   (425, 320),
   (415, 320),
   (405, 313),
   (394, 298),
   (399, 299),
   (415, 311),
   (424, 312),
   (434, 311),
   (461, 297)]},
```
lets try to draw lines on these landmark points for each faces.

```python
for face_landmarks in face_landmarks_list:
    for name, list_of_points in face_landmarks.items():
        print("the {} in this face has the following points: {}".format(name,list_of_points))
        draw.line(list_of_points, fill= "red",width=2)

pil_image.show()
```
