---
title: "Introduction to Fun with Face-Recognition"
date: 2018-01-28
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
### - Face Matching: *Find the best match for a given face.*
### - Face Similarity: *Find faces that are most similar to a given face.*
### - Face Transformation: *Generate new faces that are similar to a given face.*


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
