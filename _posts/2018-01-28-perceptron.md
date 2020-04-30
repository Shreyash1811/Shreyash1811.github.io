---
title: "Introduction to Fun with Face-Recognition"
date: 2020-03-30
tags: [data wrangling, data science, messy data]
header:
  image: "/images/titanic_analysis/titanic.png"
excerpt: "Face Recognition, Data Science"
mathjax: "true"
---
## Table of Content:
1. ["Topic of the"](#try)
2. [""]



## What is facial recognition?
*Facial recognition is a biometric software application capable of uniquely identifying or verifying a person by comparing and analyzing patterns based on the person's facial contours. Facial recognition is mostly used for security purposes, though there is increasing interest in other areas of use. In fact, facial recognition technology has received significant attention as it has potential for a wide range of application related to law enforcement as well as other enterprises.*


### In this note we will talk about:
1. Face Matching: *Find the best match for a given face.*
2. Face Similarity: *Find faces that are most similar to a given face.*
3. Face Transformation: *Generate new faces that are similar to a given face.*


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
The picture I am using here is one of the most famous selfies from Oscar awards.

<img src="{{ site.url }}{{ site.baseurl }}/images/titanic_analysis/download.png" alt="linearly separable data">

### Step 3 - Recognize faces (piece of cake??)
*Great thing about this package is that it has methods that makes things much easier for an introductory level face recognition. It is fun and does not frustrate someone who is new to face recognition.*
```python
# Locating the faces in the image
face_location = face_recognition.face_locations(image)

```
#### Face_location gives us Top, Right, Bottom and Left points of the face to further use in processing. These numbers are pixels locations in the pictures as shown below.
>[(184, 494, 339, 339),
 (46, 391, 108, 328),
 (186, 325, 275, 235),
 (5, 494, 80, 419),
 (68, 175, 175, 67),
 (47, 320, 121, 245),
 (128, 629, 235, 521),
 (155, 237, 229, 162),
 (46, 239, 108, 176)]

 *Lets count faces in the image that face_recognition could recognition*
 ```Python
 number_of_faces = len(face_location)
 print('Number of face found are {}'.format(number_of_faces))
 ```
> Number of face found are 9




Here's some basic text.

And here's some *italics*

Here's some **bold** text.

What about a [link](https://github.com/dataoptimal)?

Here's a bulleted list:
* First item
+ Second item
- Third item

Here's a numbered list:
1. First
2. Second
3. Third

Python code block:
```python
import pandas

messages = pandas.read_csv('SMSSpamCollection',sep='\t',names=['labels','message'])
```

R code block:
```r
library(tidyverse)
df <- read_csv("some_file.csv")
head(df)
```

Here's some inline code `x+y`.

Here's an image:
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg" alt="linearly separable data">

Here's another image using Kramdown:
![alt]({{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg)

Here's some math:

<a id= "try"></a>
$$z=x+y$$

You can also put it inline $$z=x+y$$
