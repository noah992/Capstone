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

Iamge recognition is widely used and it improves our search performance a lot.
One major use case of image recogition is deployment on EC site. Some EC site such as Amazo, Taobao, has search option where you can upload pictures of what you want,
and the website looks for similar objects for you.
Especially when you want specific cloths because it is common to happen that you are not sure what brand the good looking jacket is and it is difficult to describe how it looks.
You could not find the jacket describing that the jacket is green, wide neck or silk because all of these is applied on many various kinds of cloths.
It is very helpful if you can use a picture of the jacket and websites find it for you.

I worked on to create similar function with sightseeing objects. I created classification model trained with images of sightseeing objects.
This model recognizes which picture is which object and probide you certain information of the object.

One initial technical problem is that I could not deal with very many kinds of sightseeing objects due to machine spec and time constraint.
Also I would like to choose the objects which is somewhat related so I concluded to pick up 10 kinds of cathedrals.

Many EC site which sells cloths deploy image search function and Amazon is one of those store.
You can upload a picuture of cloths and Amazon finds you the similar cloths.
I introduce use of image recognition which saves your time when you look for something online.
that you can find items with its image on EC site.
I made an image recognition model that improves your search experience.
More specifically, this will help you to get locaton of sight seeing spots

which helps you to find certain information regarding an object that you are curious of using its images.


___
## Data collecting

I gathered around 100 images for each object using [Image Downloader](https://chrome.google.com/webstore/detail/image-downloader/cnpniohnfphhjihaiiggeabnkjhpaldj) from Google search result.
Get images to detect and mix those images with any images, but the any images must not have the object you want to detect. I will create a model which detects the object.This is Notre Dame. I will detect this.
There are many images which were taken at various angle and colored with some filters. I pick up pictures which look similar in perspective of colors and angles. I used 300 images for this model
Image for post
Other image can be anything. but quantity of picture should be close to Notre Dame. I will collect 200–400 pictures.

|Cathedral|
|-|
|The Cathedral Church of St. John the Divine|
|Catedral Metropolitana Nossa Senhora Aparecida|
|Patrick’s Cathedral|
|Catedral de La Plato|
|Cathedral Basilica of the Sacred Heart|
|Cathédrale Notre-Dame de Chartres|
|Cattedrale di Santa Maria del Fiore|
|Kölner Dom|
|St. Paul's Cathedral|
|Patriarchal Cathedral ST. Alexander Nevsky|


![Catedral de La Plata_100.jpg](https://github.com/noah992/Capstone/blob/master/image/Catedral%20de%20La%20Plata/Catedral%20de%20La%20Plata_100.jpg?raw=true)
___
## EDA

Clean and format images. Some pictures are taken in gray scale. Some are in color, and some has alpha information. In order to train a model, I need to feed formatted images so I will collect only RGB images.
If I do not format the images, the shapes will be different and I cannot train a model with different shaped images.

>So I want to organize images from below:
>|Image|Color information|Height|Width|
>|-|-|-|-|
>|Plato_1|RGBα|566|728|
>|Plato_2|RGB|780|1100|
>|NotreDame_1|P|1200|728|
>|NotreDame_2|RGB|875|511|
>...
>
>to below.
>|Image|Color information|Height|Width|
>|-|-|-|-|
>|Plato_2|RGB|256|256|
>|NotreDame_2|RGB|255|255|
>...

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
