---
title: "Introduction to Fun with Face-Recognition"
date: 2020-03-30
tags: [Face Recognition, Data Science]
header:
  image: "/images/face_rec/face_header.jpg"
excerpt: "Face Recognition"
mathjax: "true"
---

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
*lets try to draw lines on these landmark points for each faces.*

```python
for face_landmarks in face_landmarks_list:
    for name, list_of_points in face_landmarks.items():
        print("the {} in this face has the following points: {}".format(name,list_of_points))
        draw.line(list_of_points, fill= "red",width=2)

pil_image.show()
```
### They look like zombies from zombiland. Well! it did the job at least.

<img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/landmark_mark.png" alt="linearly separable data">

# Face Recognition and Matching:
*This was all about playing around with the faces. How about some recognizing similar faces using pixel matching techniques.*
## Step 1: Encoding the image.
*Since Images are pixel points and it can get really difficult to manipulate them in their raw form.*
- Encode the Image such that we have information on each pixel in a more workable mathematical representation.
- We will use face_encoding method to encode the images.
```python
#Encoding the image.
face_encoded = face_recognition.face_encodings(image)

if len(face_encoded) == 0:
    print("there is no face")
else:
    first_face_encoding = face_encoded[0]
    print(first_face_encoding)
```
*Expect an output with array of numbers reperesntation of Image we encoded as shown below*

```python
[-2.47579083e-01  7.29503706e-02  8.54542255e-02 -2.40019821e-02
 -8.91461521e-02  3.61719504e-02  7.91041255e-02  3.36378478e-02
  2.31346667e-01 -3.04129049e-02  1.52322352e-01 -5.63380346e-02
 -2.69292295e-01  5.37429005e-03 -4.55064327e-02  9.71197858e-02
 -1.36848509e-01 -1.02482304e-01 -1.80513084e-01 -6.74042106e-02
  2.53426284e-02  6.72162175e-02  2.11295076e-02  4.21013311e-02
 -1.19355015e-01 -3.58677238e-01 -5.32349721e-02 -1.95801377e-01
  1.10595495e-01 -1.47833824e-01  3.26224416e-02  3.66484113e-02
 -1.82484999e-01 -1.13388374e-01 -2.07062904e-02  7.75643960e-02
 -7.62411803e-02 -7.32168108e-02  2.84501433e-01 -3.07528302e-03
```
## Step 2: Lets use some face images to try to match them and recognize them.
*Here I used 3 tagged images with 3 different people in it and later I use 8 other untagged pictures with these same 3 people in it to match them with the tagged pictures. As Shown below*
img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/pic_collage.png" alt="linearly separable data">
```python
# Loading Pictues
face1 = face_recognition.load_image_file("../input/recognition/person_1.jpg")
face2 = face_recognition.load_image_file("../input/recognition/person_2.jpg")
face3 = face_recognition.load_image_file("../input/recognition/person_3.jpg")
# Encoding Pictues
person_face1 = face_recognition.face_encodings(face1)
person_face2 = face_recognition.face_encodings(face2)
person_face3 = face_recognition.face_encodings(face3)

# Putting tagged encodings in an array together
known_face_encoding =[person_face1,person_face2, person_face3]

#Loading Unknown/untagged images
unknown_image = face_recognition.load_image_file("../input/recognition/unknown_1.jpg")
```
## Step 3: Face landmark location.
*Since our untagged pictures can have multiple people in it unlike tagged pictures, we will first run face location method to locate all the faces in the pictures before we encode each face*

```python
# Face location of Untagged pictures
face_location = face_recognition.face_locations(unknown_image, number_of_times_to_upsample=2)
# Face encoding of those each faces
unknow_face_encoding = face_recognition.face_encodings(unknown_image,known_face_locations=face_location)
```
## Step 4: Comparing Face encoding of known images with Unknown images.
```python
for unknown_encoding in unknow_face_encoding:
    results = face_recognition.compare_faces(known_face_encoding,unknown_encoding)

    name ='unknown'
    if results[0].all():
        name = 'person 1'
    elif results[1].all():
        name = 'person 2'
    elif results[2].all():
        name = 'person 3'
    print(name)
```
## Output From the above code
> person 2

*Our code matches unknown image 1 to be person 2, lets see if it is correct*

**Unknown Image:**

<img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/face_rec_pic/unknown_1.jpg" alt="linearly separable data">

**Person Image:**

<img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/face_rec_pic/person_2.jpg" alt="linearly separable data">

## Amazing!! our code matched the person in the picture correctly.

## Final Fun excercise with what we learned so far:
*Lets try to put some makeup on the faces with the location arrays we can get using Face_recognition Library*
```python
#Importing main libraries
from PIL import Image , ImageDraw
# Loading images
unknown_image = face_recognition.load_image_file("../input/recognition/unknown_6.jpg")
# Landmark location on the face
face_landmarks = face_recognition.face_landmarks(unknown_image)
# Back to pil_image object from arrays
pil_image = Image.fromarray(unknown_image)
# Creating a draw obj using ImageDraw module
d = ImageDraw.Draw(pil_image,'RGBA')

# Here we will draw on these locations using fill color
for face_landmark in face_landmarks:

    d.line(face_landmark["left_eyebrow"],fill = (128,0,128,100), width=3)
    d.line(face_landmark["right_eyebrow"],fill = (128,0,128,100), width=3)

    d.polygon(face_landmark["top_lip"],fill=(128,0,128,100))  
    d.polygon(face_landmark["bottom_lip"],fill=(128,0,128,100))  

pil_image.show()
pil_image
```
<img src="{{ site.url }}{{ site.baseurl }}/images/face_rec/makup_face.png" alt="linearly separable data">
