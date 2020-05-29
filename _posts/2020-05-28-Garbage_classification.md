---
title: "Garbage Classification using Neural Network with keras"
date: 2020-05-17
categories: [Python]
tags: [Image Classification]
header:
  image: "/images/garbage_classification/header.png"
excerpt: "Building a basic convolution Neural Network to classify the type of waste using Keras"
mathjax: "true"
---

## Garbage Classification and Segregating using Image Recognition with Keras:

#### Why is it import to know what goes in the garbage and reaches the dumps?
Last summer I was fortunate to get to work with DSNY as a Business Intelligence Analyst, it was a great experience not only in the terms of the work environment and seeing the New York City from within an organisation that keeps it the way it is but also learned how the waste that you throw goes through a dozen steps.

DSNY makes sure it recycles every bit of what can be recovered from the waste. My last words on my report were **“I have been a part of NYC but DSNY made NYC a part of me”.**

**One of the biggest hurdle or rather the most time consuming part** of the process to recycling that tons of waste is sorting the waste for recyclable waste from non recyclable waste. This project is an attempt to make machine do all the heavy lifting for us in doing the sorting.  

#### What is Keras?
Keras is an open-source neural-network library written in Python. It is capable of running on top of TensorFlow, Microsoft Cognitive Toolkit, R, Theano, or PlaidML. Designed to enable fast experimentation with deep neural networks, it focuses on being user-friendly, modular, and extensible.

### Step 1: **Importing the required libraries**


```python
import numpy as np
import matplotlib.pyplot as plt
from keras.preprocessing.image import ImageDataGenerator, load_img, img_to_array, array_to_img
from keras.layers import Conv2D, Flatten, MaxPooling2D, Dense
from keras.models import Sequential

import glob, os, random
```

### Step 2 : Getting the images to train and test our model.
*I have used some 2527 labeled images of 6 different classes*
  - Carboard
  - Glass
  - Metal
  - Paper
  - Plastic
  - Trash


```python
base_path = r'C:\Users\shrey\OneDrive\Desktop\dataset_posts\81794_189983_bundle_archive\Garbage classification\Garbage classification'

img_list = glob.glob(os.path.join(base_path, '*/*.jpg'))

print(len(img_list))
```

    2527


### Preview of the images:
- I made sure the images are what the garbage normally would contain.


```python
from PIL import Image
for i, img_path in enumerate(random.sample(img_list, 6)):
    img = load_img(img_path)
    img = img_to_array(img, dtype=np.uint8)

    plt.subplot(2, 3, i+1)
    plt.imshow(img.squeeze())
```


![png](/images/garbage_classification/output_8_0.png)


### Step 3: Preparing Image data from the directory:
- Splitting the data into Train, Test and Validation images set.
- I have taken a batch size of 16 for both testing and validating.


```python
train_datagen = ImageDataGenerator(
    rescale=1./255,
    shear_range=0.1,
    zoom_range=0.1,
    width_shift_range=0.1,
    height_shift_range=0.1,
    horizontal_flip=True,
    vertical_flip=True,
    validation_split=0.1
)

test_datagen = ImageDataGenerator(
    rescale=1./255,
    validation_split=0.1
)

train_generator = train_datagen.flow_from_directory(
    base_path,
    target_size=(300, 300),
    batch_size=16,
    class_mode='categorical',
    subset='training',
    seed=0
)

validation_generator = test_datagen.flow_from_directory(
    base_path,
    target_size=(300, 300),
    batch_size=16,
    class_mode='categorical',
    subset='validation',
    seed=0
)

labels = (train_generator.class_indices)
labels = dict((v,k) for k,v in labels.items())

print(labels)
```

    Found 2276 images belonging to 6 classes.
    Found 251 images belonging to 6 classes.
    {0: 'cardboard', 1: 'glass', 2: 'metal', 3: 'paper', 4: 'plastic', 5: 'trash'}


### Step 4: Building the Neural Network:
- I have taken 4 convolution neural network.
- 4 Max pooling to reduce the complexity,
- and 2 Dense layers.
- I tried to keep it simple using relu as an activation function.


```python
model = Sequential([
    Conv2D(filters=32, kernel_size=3, padding='same', activation='relu', input_shape=(300, 300, 3)),
    MaxPooling2D(pool_size=2),

    Conv2D(filters=64, kernel_size=3, padding='same', activation='relu'),
    MaxPooling2D(pool_size=2),

    Conv2D(filters=32, kernel_size=3, padding='same', activation='relu'),
    MaxPooling2D(pool_size=2),

    Conv2D(filters=32, kernel_size=3, padding='same', activation='relu'),
    MaxPooling2D(pool_size=2),

    Flatten(),

    Dense(64, activation='relu'),

    Dense(6, activation='softmax')
])

model.compile(loss='categorical_crossentropy', optimizer='adam', metrics=['acc'])

model.summary()

```

    WARNING:tensorflow:From C:\Users\shrey\AppData\Local\Continuum\anaconda3\envs\PythonGPU\lib\site-packages\keras\backend\tensorflow_backend.py:4070: The name tf.nn.max_pool is deprecated. Please use tf.nn.max_pool2d instead.

    Model: "sequential_1"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    conv2d_1 (Conv2D)            (None, 300, 300, 32)      896       
    _________________________________________________________________
    max_pooling2d_1 (MaxPooling2 (None, 150, 150, 32)      0         
    _________________________________________________________________
    conv2d_2 (Conv2D)            (None, 150, 150, 64)      18496     
    _________________________________________________________________
    max_pooling2d_2 (MaxPooling2 (None, 75, 75, 64)        0         
    _________________________________________________________________
    conv2d_3 (Conv2D)            (None, 75, 75, 32)        18464     
    _________________________________________________________________
    max_pooling2d_3 (MaxPooling2 (None, 37, 37, 32)        0         
    _________________________________________________________________
    conv2d_4 (Conv2D)            (None, 37, 37, 32)        9248      
    _________________________________________________________________
    max_pooling2d_4 (MaxPooling2 (None, 18, 18, 32)        0         
    _________________________________________________________________
    flatten_1 (Flatten)          (None, 10368)             0         
    _________________________________________________________________
    dense_1 (Dense)              (None, 64)                663616    
    _________________________________________________________________
    dense_2 (Dense)              (None, 6)                 390       
    =================================================================
    Total params: 711,110
    Trainable params: 711,110
    Non-trainable params: 0
    _________________________________________________________________


### Step 5: Fit the date in the model to train and validate.
*I ended up doing 5 cycles of 20 epochs each to better the results*


```python
model.fit_generator(train_generator, epochs=20, validation_data=validation_generator)
```

    WARNING:tensorflow:From C:\Users\shrey\AppData\Local\Continuum\anaconda3\envs\PythonGPU\lib\site-packages\keras\backend\tensorflow_backend.py:422: The name tf.global_variables is deprecated. Please use tf.compat.v1.global_variables instead.

    Epoch 1/20
    143/143 [==============================] - 77s 535ms/step - loss: 1.6152 - acc: 0.3150 - val_loss: 1.4464 - val_acc: 0.3785
    Epoch 2/20
    143/143 [==============================] - 67s 466ms/step - loss: 1.3991 - acc: 0.4148 - val_loss: 1.5782 - val_acc: 0.4303
    Epoch 3/20
    143/143 [==============================] - 69s 486ms/step - loss: 1.3026 - acc: 0.4793 - val_loss: 1.5782 - val_acc: 0.4382
    Epoch 4/20
    143/143 [==============================] - 69s 485ms/step - loss: 1.1899 - acc: 0.5303 - val_loss: 0.8941 - val_acc: 0.4980
    Epoch 5/20
    143/143 [==============================] - 75s 524ms/step - loss: 1.1848 - acc: 0.5387 - val_loss: 1.2322 - val_acc: 0.5020
    Epoch 6/20
    143/143 [==============================] - 69s 484ms/step - loss: 1.1357 - acc: 0.5598 - val_loss: 1.3540 - val_acc: 0.5418
    Epoch 7/20
    143/143 [==============================] - 70s 487ms/step - loss: 1.0970 - acc: 0.5866 - val_loss: 0.9259 - val_acc: 0.5139
    Epoch 8/20
    143/143 [==============================] - 70s 488ms/step - loss: 1.0801 - acc: 0.5927 - val_loss: 1.2407 - val_acc: 0.5618
    Epoch 9/20
    143/143 [==============================] - 94s 658ms/step - loss: 1.0235 - acc: 0.6085 - val_loss: 0.8642 - val_acc: 0.6215
    Epoch 10/20
    143/143 [==============================] - 103s 719ms/step - loss: 0.9809 - acc: 0.6261 - val_loss: 1.4799 - val_acc: 0.6295
    Epoch 11/20
    143/143 [==============================] - 83s 579ms/step - loss: 0.9864 - acc: 0.6252 - val_loss: 0.8969 - val_acc: 0.5896
    Epoch 12/20
    143/143 [==============================] - 76s 533ms/step - loss: 0.9286 - acc: 0.6599 - val_loss: 0.6854 - val_acc: 0.6215
    Epoch 13/20
    143/143 [==============================] - 77s 542ms/step - loss: 0.9186 - acc: 0.6643 - val_loss: 0.9536 - val_acc: 0.6375
    Epoch 14/20
    143/143 [==============================] - 80s 557ms/step - loss: 0.9272 - acc: 0.6538 - val_loss: 1.0167 - val_acc: 0.6016
    Epoch 15/20
    143/143 [==============================] - 76s 529ms/step - loss: 0.8763 - acc: 0.6740 - val_loss: 0.7694 - val_acc: 0.6653
    Epoch 16/20
    143/143 [==============================] - 75s 524ms/step - loss: 0.8394 - acc: 0.6894 - val_loss: 0.8056 - val_acc: 0.6414
    Epoch 17/20
    143/143 [==============================] - 76s 529ms/step - loss: 0.8546 - acc: 0.6841 - val_loss: 1.7697 - val_acc: 0.6574
    Epoch 18/20
    143/143 [==============================] - 79s 552ms/step - loss: 0.8035 - acc: 0.7056 - val_loss: 0.9549 - val_acc: 0.6574
    Epoch 19/20
    143/143 [==============================] - 76s 532ms/step - loss: 0.7713 - acc: 0.7245 - val_loss: 0.8060 - val_acc: 0.6653
    Epoch 20/20
    143/143 [==============================] - 76s 530ms/step - loss: 0.7836 - acc: 0.7017 - val_loss: 1.1788 - val_acc: 0.6733





    <keras.callbacks.callbacks.History at 0x1bcb264cb00>




```python
model.fit_generator(train_generator, epochs=20, validation_data=validation_generator)
```

    Epoch 1/20
    143/143 [==============================] - 78s 546ms/step - loss: 0.7756 - acc: 0.7192 - val_loss: 1.3460 - val_acc: 0.6773
    Epoch 2/20
    143/143 [==============================] - 74s 520ms/step - loss: 0.7089 - acc: 0.7368 - val_loss: 0.6735 - val_acc: 0.6693
    Epoch 3/20
    143/143 [==============================] - 76s 532ms/step - loss: 0.7833 - acc: 0.7021 - val_loss: 1.0749 - val_acc: 0.6295
    Epoch 4/20
    143/143 [==============================] - 75s 527ms/step - loss: 0.6850 - acc: 0.7491 - val_loss: 0.8889 - val_acc: 0.6972
    Epoch 5/20
    143/143 [==============================] - 76s 529ms/step - loss: 0.6564 - acc: 0.7619 - val_loss: 1.2926 - val_acc: 0.6375
    Epoch 6/20
    143/143 [==============================] - 75s 522ms/step - loss: 0.6904 - acc: 0.7417 - val_loss: 0.5795 - val_acc: 0.7012
    Epoch 7/20
    143/143 [==============================] - 75s 526ms/step - loss: 0.6499 - acc: 0.7610 - val_loss: 0.8577 - val_acc: 0.6574
    Epoch 8/20
    143/143 [==============================] - 78s 546ms/step - loss: 0.6010 - acc: 0.7733 - val_loss: 0.6104 - val_acc: 0.6454
    Epoch 9/20
    143/143 [==============================] - 77s 535ms/step - loss: 0.6360 - acc: 0.7627 - val_loss: 0.5955 - val_acc: 0.6653
    Epoch 10/20
    143/143 [==============================] - 76s 534ms/step - loss: 0.6093 - acc: 0.7830 - val_loss: 1.0563 - val_acc: 0.6733
    Epoch 11/20
    143/143 [==============================] - 76s 533ms/step - loss: 0.5914 - acc: 0.7830 - val_loss: 0.5808 - val_acc: 0.6056
    Epoch 12/20
    143/143 [==============================] - 78s 543ms/step - loss: 0.5438 - acc: 0.7961 - val_loss: 0.8169 - val_acc: 0.7012
    Epoch 13/20
    143/143 [==============================] - 79s 549ms/step - loss: 0.5604 - acc: 0.7939 - val_loss: 0.5128 - val_acc: 0.6534
    Epoch 14/20
    143/143 [==============================] - 77s 541ms/step - loss: 0.5340 - acc: 0.8098 - val_loss: 0.7509 - val_acc: 0.7291
    Epoch 15/20
    143/143 [==============================] - 75s 523ms/step - loss: 0.5346 - acc: 0.8076 - val_loss: 1.7310 - val_acc: 0.7371
    Epoch 16/20
    143/143 [==============================] - 76s 534ms/step - loss: 0.5125 - acc: 0.8137 - val_loss: 0.7376 - val_acc: 0.7211
    Epoch 17/20
    143/143 [==============================] - 80s 556ms/step - loss: 0.5185 - acc: 0.8199 - val_loss: 0.7743 - val_acc: 0.7331
    Epoch 18/20
    143/143 [==============================] - 76s 533ms/step - loss: 0.5301 - acc: 0.8102 - val_loss: 0.5023 - val_acc: 0.6494
    Epoch 19/20
    143/143 [==============================] - 76s 533ms/step - loss: 0.5401 - acc: 0.7948 - val_loss: 0.9443 - val_acc: 0.6693
    Epoch 20/20
    143/143 [==============================] - 77s 538ms/step - loss: 0.4736 - acc: 0.8286 - val_loss: 0.5621 - val_acc: 0.7012





    <keras.callbacks.callbacks.History at 0x1bcbddaf400>




```python
model.fit_generator(train_generator, epochs=20, validation_data=validation_generator)
```

    Epoch 1/20
    143/143 [==============================] - 71s 499ms/step - loss: 0.4631 - acc: 0.8313 - val_loss: 1.4531 - val_acc: 0.7012
    Epoch 2/20
    143/143 [==============================] - 77s 538ms/step - loss: 0.4395 - acc: 0.8436 - val_loss: 0.9198 - val_acc: 0.7371
    Epoch 3/20
    143/143 [==============================] - 74s 517ms/step - loss: 0.4414 - acc: 0.8374 - val_loss: 1.1267 - val_acc: 0.7092
    Epoch 4/20
    143/143 [==============================] - 68s 476ms/step - loss: 0.4538 - acc: 0.8273 - val_loss: 1.3691 - val_acc: 0.7291
    Epoch 5/20
    143/143 [==============================] - 73s 510ms/step - loss: 0.4419 - acc: 0.8418 - val_loss: 0.2491 - val_acc: 0.7410
    Epoch 6/20
    143/143 [==============================] - 72s 503ms/step - loss: 0.4424 - acc: 0.8409 - val_loss: 1.1183 - val_acc: 0.6972
    Epoch 7/20
    143/143 [==============================] - 69s 481ms/step - loss: 0.4320 - acc: 0.8445 - val_loss: 0.4544 - val_acc: 0.6972
    Epoch 8/20
    143/143 [==============================] - 68s 477ms/step - loss: 0.4309 - acc: 0.8533 - val_loss: 0.6958 - val_acc: 0.7211
    Epoch 9/20
    143/143 [==============================] - 68s 477ms/step - loss: 0.4121 - acc: 0.8497 - val_loss: 1.1414 - val_acc: 0.7092
    Epoch 10/20
    143/143 [==============================] - 68s 473ms/step - loss: 0.3815 - acc: 0.8590 - val_loss: 0.4075 - val_acc: 0.7171
    Epoch 11/20
    143/143 [==============================] - 67s 471ms/step - loss: 0.3741 - acc: 0.8708 - val_loss: 0.5975 - val_acc: 0.7251
    Epoch 12/20
    143/143 [==============================] - 68s 479ms/step - loss: 0.4142 - acc: 0.8563 - val_loss: 0.2998 - val_acc: 0.7371
    Epoch 13/20
    143/143 [==============================] - 69s 483ms/step - loss: 0.3891 - acc: 0.8660 - val_loss: 0.4255 - val_acc: 0.7371
    Epoch 14/20
    143/143 [==============================] - 68s 472ms/step - loss: 0.4212 - acc: 0.8519 - val_loss: 1.4170 - val_acc: 0.7331
    Epoch 15/20
    143/143 [==============================] - 68s 476ms/step - loss: 0.4071 - acc: 0.8568 - val_loss: 1.2283 - val_acc: 0.7171
    Epoch 16/20
    143/143 [==============================] - 68s 473ms/step - loss: 0.4024 - acc: 0.8467 - val_loss: 0.4771 - val_acc: 0.7092
    Epoch 17/20
    143/143 [==============================] - 68s 473ms/step - loss: 0.3330 - acc: 0.8809 - val_loss: 0.4325 - val_acc: 0.7331
    Epoch 18/20
    143/143 [==============================] - 67s 471ms/step - loss: 0.3712 - acc: 0.8682 - val_loss: 0.3482 - val_acc: 0.7450
    Epoch 19/20
    143/143 [==============================] - 68s 473ms/step - loss: 0.3457 - acc: 0.8796 - val_loss: 0.7545 - val_acc: 0.6932
    Epoch 20/20
    143/143 [==============================] - 68s 473ms/step - loss: 0.3521 - acc: 0.8792 - val_loss: 0.2761 - val_acc: 0.7410





    <keras.callbacks.callbacks.History at 0x1bd0f9aa2b0>




```python
model.fit_generator(train_generator, epochs=20, validation_data=validation_generator)
```

    Epoch 1/20
    143/143 [==============================] - 69s 485ms/step - loss: 0.3161 - acc: 0.8801 - val_loss: 0.8363 - val_acc: 0.7251
    Epoch 2/20
    143/143 [==============================] - 69s 480ms/step - loss: 0.3496 - acc: 0.8770 - val_loss: 0.5825 - val_acc: 0.7171
    Epoch 3/20
    143/143 [==============================] - 70s 492ms/step - loss: 0.3456 - acc: 0.8787 - val_loss: 1.6263 - val_acc: 0.7371
    Epoch 4/20
    143/143 [==============================] - 91s 633ms/step - loss: 0.3826 - acc: 0.8594 - val_loss: 0.6068 - val_acc: 0.7450
    Epoch 5/20
    143/143 [==============================] - 72s 501ms/step - loss: 0.3268 - acc: 0.8801 - val_loss: 0.5656 - val_acc: 0.7490
    Epoch 6/20
    143/143 [==============================] - 68s 478ms/step - loss: 0.3356 - acc: 0.8805 - val_loss: 0.9498 - val_acc: 0.7410
    Epoch 7/20
    143/143 [==============================] - 68s 478ms/step - loss: 0.2916 - acc: 0.8954 - val_loss: 1.6909 - val_acc: 0.7331
    Epoch 8/20
    143/143 [==============================] - 68s 478ms/step - loss: 0.3800 - acc: 0.8708 - val_loss: 0.4898 - val_acc: 0.7171
    Epoch 9/20
    143/143 [==============================] - 68s 477ms/step - loss: 0.3231 - acc: 0.8862 - val_loss: 1.5298 - val_acc: 0.7410
    Epoch 10/20
    143/143 [==============================] - 68s 476ms/step - loss: 0.2911 - acc: 0.8937 - val_loss: 0.6644 - val_acc: 0.7490
    Epoch 11/20
    143/143 [==============================] - 69s 481ms/step - loss: 0.2871 - acc: 0.8994 - val_loss: 0.6162 - val_acc: 0.7530
    Epoch 12/20
    143/143 [==============================] - 69s 480ms/step - loss: 0.2891 - acc: 0.9011 - val_loss: 0.9558 - val_acc: 0.7769
    Epoch 13/20
    143/143 [==============================] - 68s 478ms/step - loss: 0.2691 - acc: 0.9003 - val_loss: 0.2585 - val_acc: 0.7729
    Epoch 14/20
    143/143 [==============================] - 68s 474ms/step - loss: 0.3307 - acc: 0.8761 - val_loss: 0.4693 - val_acc: 0.7490
    Epoch 15/20
    143/143 [==============================] - 68s 474ms/step - loss: 0.2724 - acc: 0.9042 - val_loss: 0.5113 - val_acc: 0.7530
    Epoch 16/20
    143/143 [==============================] - 69s 485ms/step - loss: 0.2721 - acc: 0.9073 - val_loss: 1.0859 - val_acc: 0.7809
    Epoch 17/20
    143/143 [==============================] - 68s 475ms/step - loss: 0.2966 - acc: 0.8950 - val_loss: 0.9362 - val_acc: 0.7570
    Epoch 18/20
    143/143 [==============================] - 67s 470ms/step - loss: 0.2754 - acc: 0.8959 - val_loss: 0.7791 - val_acc: 0.7291
    Epoch 19/20
    143/143 [==============================] - 69s 480ms/step - loss: 0.2661 - acc: 0.9091 - val_loss: 1.2383 - val_acc: 0.7450
    Epoch 20/20
    143/143 [==============================] - 68s 474ms/step - loss: 0.2856 - acc: 0.8963 - val_loss: 1.1178 - val_acc: 0.7490





    <keras.callbacks.callbacks.History at 0x1bd0f9b4f98>




```python
model.fit_generator(train_generator, epochs=20, validation_data=validation_generator)
```

    Epoch 1/20
    143/143 [==============================] - 63s 441ms/step - loss: 0.3072 - acc: 0.8976 - val_loss: 0.9062 - val_acc: 0.7410
    Epoch 2/20
    143/143 [==============================] - 71s 499ms/step - loss: 0.2438 - acc: 0.9117 - val_loss: 0.0425 - val_acc: 0.7450
    Epoch 3/20
    143/143 [==============================] - 75s 522ms/step - loss: 0.2289 - acc: 0.9244 - val_loss: 1.6609 - val_acc: 0.7570
    Epoch 4/20
    143/143 [==============================] - 73s 509ms/step - loss: 0.2536 - acc: 0.9112 - val_loss: 0.9987 - val_acc: 0.7769
    Epoch 5/20
    143/143 [==============================] - 67s 471ms/step - loss: 0.3728 - acc: 0.8642 - val_loss: 0.2657 - val_acc: 0.7610
    Epoch 6/20
    143/143 [==============================] - 67s 469ms/step - loss: 0.2970 - acc: 0.8981 - val_loss: 1.0738 - val_acc: 0.7450
    Epoch 7/20
    143/143 [==============================] - 68s 476ms/step - loss: 0.2550 - acc: 0.9077 - val_loss: 0.6475 - val_acc: 0.7610
    Epoch 8/20
    143/143 [==============================] - 68s 474ms/step - loss: 0.2246 - acc: 0.9231 - val_loss: 1.0998 - val_acc: 0.7530
    Epoch 9/20
    143/143 [==============================] - 68s 476ms/step - loss: 0.2235 - acc: 0.9161 - val_loss: 1.1230 - val_acc: 0.7649
    Epoch 10/20
    143/143 [==============================] - 67s 470ms/step - loss: 0.2168 - acc: 0.9266 - val_loss: 0.3634 - val_acc: 0.7809
    Epoch 11/20
    143/143 [==============================] - 67s 469ms/step - loss: 0.2515 - acc: 0.9130 - val_loss: 0.3327 - val_acc: 0.7131
    Epoch 12/20
    143/143 [==============================] - 68s 477ms/step - loss: 0.2322 - acc: 0.9187 - val_loss: 0.5366 - val_acc: 0.7131
    Epoch 13/20
    143/143 [==============================] - 67s 469ms/step - loss: 0.2108 - acc: 0.9253 - val_loss: 0.5895 - val_acc: 0.7809
    Epoch 14/20
    143/143 [==============================] - 67s 468ms/step - loss: 0.2370 - acc: 0.9178 - val_loss: 1.0208 - val_acc: 0.7171
    Epoch 15/20
    143/143 [==============================] - 68s 477ms/step - loss: 0.3069 - acc: 0.8963 - val_loss: 0.1289 - val_acc: 0.7371
    Epoch 16/20
    143/143 [==============================] - 71s 499ms/step - loss: 0.2730 - acc: 0.9033 - val_loss: 0.0812 - val_acc: 0.7371
    Epoch 17/20
    143/143 [==============================] - 91s 634ms/step - loss: 0.2411 - acc: 0.9126 - val_loss: 0.4288 - val_acc: 0.7410
    Epoch 18/20
    143/143 [==============================] - 62s 436ms/step - loss: 0.2495 - acc: 0.9139 - val_loss: 0.6342 - val_acc: 0.7689
    Epoch 19/20
    143/143 [==============================] - 68s 474ms/step - loss: 0.2212 - acc: 0.9240 - val_loss: 1.0186 - val_acc: 0.7450
    Epoch 20/20
    143/143 [==============================] - 68s 475ms/step - loss: 0.2908 - acc: 0.8994 - val_loss: 2.1742 - val_acc: 0.7331





    <keras.callbacks.callbacks.History at 0x1bce2cf8780>



#### Five cycles later our model seems to be in a good place to be able to predict our test samples

### Step 6: Making predictions with the model


```python
test_x, test_y = validation_generator.__getitem__(1)

preds = model.predict(test_x)

plt.figure(figsize=(16, 16))
for i in range(16):
    plt.subplot(4, 4, i+1)
    plt.title('pred:%s / truth:%s' % (labels[np.argmax(preds[i])], labels[np.argmax(test_y[i])]))
    plt.imshow(test_x[i])
```


![png](/images/garbage_classification/output_21_0.png)



```python
predicted= []
actual = []
for i in range(16):
    predicted.append(labels[np.argmax(preds[i])])
    actual.append(labels[np.argmax(test_y[i])])

import pandas as pd
df = pd.DataFrame(predicted, columns=["predicted"])
df["actual"] = actual
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>predicted</th>
      <th>actual</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>paper</td>
      <td>paper</td>
    </tr>
    <tr>
      <th>1</th>
      <td>plastic</td>
      <td>plastic</td>
    </tr>
    <tr>
      <th>2</th>
      <td>paper</td>
      <td>paper</td>
    </tr>
    <tr>
      <th>3</th>
      <td>glass</td>
      <td>glass</td>
    </tr>
    <tr>
      <th>4</th>
      <td>metal</td>
      <td>cardboard</td>
    </tr>
    <tr>
      <th>5</th>
      <td>plastic</td>
      <td>glass</td>
    </tr>
    <tr>
      <th>6</th>
      <td>cardboard</td>
      <td>cardboard</td>
    </tr>
    <tr>
      <th>7</th>
      <td>glass</td>
      <td>glass</td>
    </tr>
    <tr>
      <th>8</th>
      <td>plastic</td>
      <td>plastic</td>
    </tr>
    <tr>
      <th>9</th>
      <td>plastic</td>
      <td>metal</td>
    </tr>
    <tr>
      <th>10</th>
      <td>paper</td>
      <td>paper</td>
    </tr>
    <tr>
      <th>11</th>
      <td>plastic</td>
      <td>plastic</td>
    </tr>
    <tr>
      <th>12</th>
      <td>glass</td>
      <td>metal</td>
    </tr>
    <tr>
      <th>13</th>
      <td>metal</td>
      <td>metal</td>
    </tr>
    <tr>
      <th>14</th>
      <td>paper</td>
      <td>paper</td>
    </tr>
    <tr>
      <th>15</th>
      <td>paper</td>
      <td>paper</td>
    </tr>
  </tbody>
</table>
</div>
## conclusions:
- Our model seems to be doing great in classifying most of the object classes.
- It is struggling between Glass and Metal since they have quite a similarity in appearance.  
