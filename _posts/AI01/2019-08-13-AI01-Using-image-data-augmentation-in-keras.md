---
layout : post
title : AI01, Using image data augmentation in keras
categories: [AI01]
comments : true
tags : [AI01]
---
[Back to the previous page](https://userdyk-github.github.io/Study.html) ｜<a href="https://github.com/userdyk-github/userdyk-github.github.io/blob/master/_posts/AI01/2019-08-13-AI01-Using-image-data-augmentation-in-keras.md" target="_blank">page management</a><br>
List of posts to read before reading this article
- <a href='https://userdyk-github.github.io/pl03/PL03-Libraries.html' target="_blank">Python Libraries</a>
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

## Contents
{:.no_toc}

* ToC
{:toc}

<hr class="division1">

## **Sample Image : bird.jpg**
[bird.jpg][1]
![bird](https://user-images.githubusercontent.com/52376448/71425392-90601580-26df-11ea-923d-3ceb7efd0b70.jpg)


<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>

<br><br><br>

<hr class="division2">

## **Shift Augmentation**
### ***Horizontal shift***
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(width_shift_range=0.9)
#datagen = ImageDataGenerator(width_shift_range=[-200,200])
```
```python
# example of horizental shift image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(width_shift_range=0.9)
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,12,figsize=(20,3))
for i in range(3):
    for j in range(12):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425606-4dec0800-26e2-11ea-9cb0-52ec3f7b9457.png)
<hr class='division3'>
</details>

<br><br><br>

---


### ***Vertical shift***
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(height_shift_range=0.9)
#datagen = ImageDataGenerator(height_shift_range=[-200,200])
```
```python
# example of vertical shift image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(height_shift_range=0.9)
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,12,figsize=(20,3))
for i in range(3):
    for j in range(12):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425565-e635bd00-26e1-11ea-86a2-c884b9106c8d.png)
<hr class='division3'>
</details>

<br><br><br>

<hr class="division2">

## **Flip Augmentation**
### ***Horizontal flip***
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(horizontal_flip=True)
```
```python
# example of horizontal flip image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(horizontal_flip=True)
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,3,figsize=(10,10))
for i in range(3):
    for j in range(3):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425704-7d4f4480-26e3-11ea-8a95-7e36c1367c71.png)
<hr class='division3'>
</details>

<br><br><br>

---

### ***Vertical flip***
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(vertical_flip=True)
```
```python
# example of vertical flip image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(vertical_flip=True)
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,3,figsize=(10,10))
for i in range(3):
    for j in range(3):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425719-a8399880-26e3-11ea-8a14-42d5c4d239cf.png)
<hr class='division3'>
</details>

<br><br><br>
<hr class="division2">

## **Random Rotation Augmentation**
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(rotation_range=90)
```
```python
# example of random rotation image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(rotation_range=90)
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,3,figsize=(9,9))
for i in range(3):
    for j in range(3):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425812-b20fcb80-26e4-11ea-801d-831564b6aa50.png)
<hr class='division3'>
</details>

<br><br><br>

<hr class="division2">

## **Random Brightness Augmentation**
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(brightness_range=[0.2,1.0])
```
```python
# example of brighting image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(brightness_range=[0.2,1.0])
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,3,figsize=(9,9))
for i in range(3):
    for j in range(3):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425860-4417d400-26e5-11ea-9cfb-85e07f1ec92e.png)
<hr class='division3'>
</details>


<br><br><br>

<hr class="division2">

## **Random Zoom Augmentation**
```python
from keras.preprocessing.image import ImageDataGenerator
datagen = ImageDataGenerator(zoom_range=[0.5,1.0])
```
```python
# example of zoom image augmentation
from numpy import expand_dims
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import ImageDataGenerator
from matplotlib import pyplot

# load the image
img = load_img('bird.jpg')
data = img_to_array(img)
samples = expand_dims(data, 0)

# create image data augmentation generator
datagen = ImageDataGenerator(zoom_range=[0.5,1.0])
iterator = datagen.flow(samples, batch_size=1)

# generate samples and plot
fig , axes = pyplot.subplots(3,3,figsize=(9,9))
for i in range(3):
    for j in range(3):
        batch = iterator.next()
        image = batch[0].astype('uint8')
        axes[i,j].imshow(image)
pyplot.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/71425883-893c0600-26e5-11ea-82fa-db53c5789239.png)
<hr class='division3'>
</details>

<br><br><br>

<hr class="division1">

List of posts followed by this article
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

Reference
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>

[1]:{{ site.url }}/download/AI01/bird.jpg

