# Capstone: Image recognition model with neural network
---

## Introduction

This repo contains code of convolutional neural network model for image recognition and its images

> * [Code](https://github.com/noah992/Capstone/blob/master/code/code.ipynb)
> * [Images](https://github.com/noah992/Capstone/tree/master/image)
> * [Slide](https://github.com/noah992/Capstone/blob/master/assets/Presentation.pdf)

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

I worked on to create similar function using a multi-classification model trained with images of several sightseeing objects. This model recognizes which object is in a picture. For this model, convolutional neural network is appropriate as this predicts based on images

One initial technical problem is that I could not deal with very many kinds of sightseeing objects due to machine spec and time constraint so that I chosed only 10 objects which are somewhat related.

After all I decided to use 10 kinds of cathedrals as these are famous places for visitors and I bet their appearances are relatively similar to one another so that many visitors could be confused when they want to go certain cathedral.


___
## Data set

I gathered images of 10 cathedrals from Google search result using Chrome extension, [Image Downloader](https://chrome.google.com/webstore/detail/image-downloader/cnpniohnfphhjihaiiggeabnkjhpaldj)

These images need to satisfy  below
* Similar - Angle, distance
* RGB - Filter out Gray, RGBA
* Same shape - (1200, 800, 3) → (256, 256, 3)

### Similar

Some images has a front side of an object, some has back side of the object and some others ware taken at very far away. If I take all of these images into the model together, it would not learn effectively so that I need to gather images which are visually similar.

Below 2 images contain same object, but it looks different as they were taken at different angle and distance. Also second one is colored by a light.
Using data set of these combination would not be rational so that I gathered images only similar to first one.

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

Height and width of images are various. I converted the images to have same shape.

>So I want to organize images from below:
>|Image|Height|Width|
>|-|-|-|
>|Plato_2|780|1100|
>|NotreDame_2|875|511|
>...
>
>to below.
>|Image|Height|Width|
>|-|-|-|
>|Plato_2|256|256|
>|NotreDame_2|256|256|
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
___
## Reccomendation

I made an app to demonstrate how you could use the image recognition on your website.
![demonstration](https://github.com/noah992/Capstone/blob/master/assets/demonstration.gif?raw=true)
In this app, I fed a url of image. This is a cathedral located in Brazil.
You can see what image I fed on the second screen.
This app loaded the image and neural network model which I assembled worked on the background and generated a prediction of what the object is in the image.
Based on the result of the prediction, it navigates you to the locatoin on google map.

You may consider to deploy image recognition as search option as it definitely improve user experience. As I mentioned in `Problem Statement`, visitors could not be sure which cathedral is which as they look similar so it could be hard to identify a cathedral for them by searching with keywords however, they would be happy using image search because it would be much easier and faster for this case.

---

## Next step

I used images which are taken at similar angle, similar distance and similar color. So if I make a prediction with images which were taken in different angle or with different light color, this model is likely to fail to predict correct location.

I can surely improve the accuracy by feeding more training images, and also it will be more useful to train with various kinds of pictures in terms of angle and color because this model will be more flexible on picture variations
