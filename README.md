# Capstone: Image recognition model with neural network
---

## Introduction

This repo contains code of convolutional neural network model for image recognition and its images

> * [Code](https://github.com/noah992/Capstone/blob/master/code/code.ipynb)
> * [Images](https://github.com/noah992/Capstone/tree/master/image)

## Summary

* ### Problem Statement
  * Multi-classification model with convolutional neural network trained by images of 10 cathedrals.
  This is known as image recognition and great tool as a search option especially when it is hard to describe what you are looking for. 
* ### Data set
  * Get around 50 images for 10 objects from Google search result using [Image Downloader](https://chrome.google.com/webstore/detail/image-downloader/cnpniohnfphhjihaiiggeabnkjhpaldj) 
  * Only `RGB` images.
* ### Model, Evaluation
  * Model: `tensorflow.keras`: `sequential`
  * Metric: `Accuracy`
* ### Recommendation
  * See demonstraion below how you could use image recognition as a search option.
---
## Problem Statement

Iamge recognition is widely used and it improves our search performance a lot. One major use case of image recogition is deployment on EC site. Some EC sites such as Amazon, ZARA, has a search option where you can upload a picture of items that you want to buy and then the website will look for the items or similar items for you.

Especially it is deployed on many fashion related EC sites because it is common to happen that you are not sure what brand the good looking jacket is and it is difficult to describe how it looks. You could not find the jacket describing that the jacket is green, made with silk or else because all of these features can be applied on many various kinds of cloths. It is very helpful if you can use a picture of the jacket and the websites find it for you.

I worked on to create similar function with sightseeing objects using a multi-classification model trained with images of several sightseeing objects. This model recognizes which object is in the picture. Convolutional neural network model is appropriate for this problem as I use images as prediction values.

One initial technical problem is that I could not deal with very many kinds of sightseeing objects due to machine spec and time constraint so that I chosed only 10 objects which are somewhat related. After all I decided to use 10 kinds of cathedrals as these are famous places for visitors and I bet their appearances are relatively similar to one another so that many visitors could not be sure which cathedral they want to go.


___
## Data set

I will gather images of 10 cathedrals from Google search result using [Image Downloader](https://chrome.google.com/webstore/detail/image-downloader/cnpniohnfphhjihaiiggeabnkjhpaldj)

My model requires the images to be below
* Similar - Angle, distance
* RGB - Filter out Gray, RGBA
* Same shape - (1200, 800, 3) → (256, 256, 3)

#### Similar

Some images has a front side of an object, some has back side of the object and some others are taken at very far away. If I take all of these images into my model together, it would not learn effectively so that I need to gather images which are visually similar.

Below 2 images contain same object, but it looks different as they were taken at different angle and distance. Also second one is colored by light.
Data set of these combination would not be rational so that I gather images similar to first one.

<img src="https://github.com/noah992/Capstone/blob/master/assets/data-collecting-01.JPG?raw=true" width="200pt"> <img src="https://github.com/noah992/Capstone/blob/master/assets/data-collecting-02.JPG?raw=true" width="300pt">


### RGB

Some pictures are in gray scale, others are in color, and some others have alpha information. As I need to feed formatted images, I will take only `RGB` images.

>Third index of the data shape stores color information and this number must be same
>|Color|Shape|
>|-|-|
>|RGBα|(1200, 450,  `4`)|
>|RGB|(428, 678, `3`)|
>|Gray|(564, 680, `1`)|

### Same shape

Height and width of images vary. I converted the images to have same shape.

>So I want to organize images from below:
>|Image|Color information|Height|Width|
>|-|-|-|-|
>|Plato_2|780|1100|
>|NotreDame_2|875|511|
>...
>
>to below.
>|Image|Color information|Height|Width|
>|-|-|-|-|
>|Plato_2|256|256|
>|NotreDame_2|255|255|
>...

### Target objects

>|10 Cathedrals in this model|
>|-|
>|The Cathedral Church of St. John the Divine|
>|Catedral Metropolitana Nossa Senhora Aparecida|
>|Patrick’s Cathedral|
>|Catedral de La Plato|
>|Cathedral Basilica of the Sacred Heart|
>|Cathédrale Notre-Dame de Chartres|
>|Cattedrale di Santa Maria del Fiore|
>|Kölner Dom|
>|St. Paul's Cathedral|
>|Patriarchal Cathedral ST. Alexander Nevsky|

___
## Model, Evaluation

I used convolutional neural network model with `tensorflow Sequential`

**90% Accuracy with unseen data**
Surely this can be closer to 100% with more images
___
## Reccomendation

I made an app to demonstrate how you could use the image recognition on your website.
![demonstration](https://github.com/noah992/Capstone/blob/master/assets/demonstration.gif?raw=true)
In this app, I fed an url of image. This is a cathedral located in Brazil.
You can see what image I fed on the second page.
This app loaded the image and neural network model which I assembled worked on the backend and generated prediction of what the object is in the image.
Based on the result of the prediction, it navigate you to the locatoin with google map.

Deploying of image recognition as search option will resulted in improvement of user experience

---

## Next step

I used images which are taken at similar angle, similar distance and similar color. So if I feed images which were taken in different angle or with different light color, this model is likely to fail to predict correct location.

I could improve the accuracy by feeding various kinds of pictures in terms of angle and color, this app will be greater as it can be more flexible on picture variation
