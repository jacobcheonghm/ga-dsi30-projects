# Porcelain Mark Classifier
by Cheong Hao Ming

link to dataset:
https://drive.google.com/drive/folders/1cwqyUktpcGBxZiTC5uXqnFrFbHqUCfFv?usp=sharing

link to model weights:
https://drive.google.com/drive/folders/1hTp-YQGXc6RwUjWtdjpKn64QgvqQX6Se?usp=sharing

## Background

Porcelain marks on antique Chinese porcelain were used to represent the period a piece was made in. Rather than indicating a particular year, the marks are usually reign marks which suggest the item may have been made anytime during the reign of a particular emperor. Therefore these porcelain marks have always been a topic of interest for experienced and budding new collectors alike.

## Problem Statement

As a business manager of a local antique boutique store specialising in oriental porcelain, I have chosen to build a porcelain mark classifier to test and improve my understanding of computer vision while applying some domain knowledge in the field of oriental porcelain.

Given that there exist more than a few dozen types of reign marks in just the two most recent dynasties alone (Ming and Qing Dynasty), this model will be scaled down to classifying 3 different reign marks of the Qing Dynasty.

## The Data

All image data have been manually collected from the websites of reputable auctions sites such as Sotheby's and Christies to ensure authenticity and accuracy of the images used to train and test the model.

### Summary of Dataset

|   | **Period** | **Source** | **Type**   | **Train** | **Val** | **Test** |
|:-:|:----------:|:----------:|------------|:---------:|:-------:|:--------:|
| 1 |  Qianlong  |  Internet  | _Zhuanshu_ |     62    |    20   |    30    |
| 2 |  Daoguang  |  Internet  | _Zhuanshu_ |     60    |    20   |    30    |
| 3 |   Guangxu  |  Internet  | _Kaishu_   |     60    |    20   |    30    |

Of the 30 test image in each class, 10 of the images are collected beyond the two auction sites. They are also not cropped to show only the porcelain mark and have more variations in terms of alignment, rotation and size of the porcelain relative to the whole image. Therefore image augmentation has been conducted using keras ImageGenerator on the training and validation data to add more variations to our small dataset to better deal with the unseen test data.

## Modelling

A total of 5 models have been constructed. A custom CNN model, VGG19 Base model, VGG19 with custom layers, MobileNet Base model and lastly a MobileNet with custom layers. For the four model contructed with pre-trained models, the base layers have been kept frozen to retain their original weight. 

## Evaluation
After constructing and evaluating the five models, their performance are compiled and compared in the table below:
<br/>
<br/>

|   |     **Model**    | **Train Acc** | **Train Loss** | **Test Acc** | **Test Loss** |
|:-:|:----------------:|:-------------:|----------------|:------------:|:-------------:|
| 1 |    Custom CNN    |     0.8571    |     0.4086     |    0.5889    |     1.1550    |
| 2 |    VGG19 Base    |     0.9780    |     0.0891     |  **0.8444**  |   **0.4432**  |
| 3 |   VGG19 Custom   |     0.9066    |     0.3201     |    0.7333    |     0.5852    |
| 4 |  MobileNet Base  |     0.9945    |     0.0251     |    0.7889    |    12.2197    |
| 5 | MobileNet Custom |     0.9890    |     0.1059     |    0.8000    |     0.5620    |


<br/>
<br/>
With reference to the table above, we can conclude the the VGG19 Base model is the best among the five as it scores the highest in terms of accuracy on unseen test data.

When we examine the misclassified images from our choice VGG19 Base model, we can observed that out of the 14 missclassified images, 13 belong the group of "dirty" test images that have not been cropped and processed to just show the mark.The single "clean" test image that was misclassified belongs to the "Qianlong" class which looks very similar to the "Daoguang" mark as they are both in "Zhuanshu" format.

The model is then tested against a cleaner test data by cropping the dirty images to ensure the porcelain is centrally located and can be easilty identified.

**Accuracy Improved from 84% to 94%**

As expected, with a cleaner dataset, we see a huge improvement in the classification accuracy from 84% to 94%. The misclassification also occurs where it is more likely, which is between the "Daoguang" and "Qianlong" class. All "Guangxu" class images have been classified accurately and only 5 "Qianlong" marks were wrongly classified as "Daoguang" marks. Then model behave similarly to when it was predicting on the unclean data where it seems to have a bias towards classifying "Daoguang" marks.
<br/>

When examining the misclassified images, again 4 of the 5 images originated from the "dirty" images, albiet cleaning has been done. The same clean image that has been misclassified is again being misclassified here. For the four misclassified images, we can see that the marks are more rotated, skewed or had sticker covering part of the mark. All these factor may have contributed to the misclassification.

## Conclusion & Future Works

**Conclusion**
<br/>

In conclusion, an experimental Chinese porcelain mark classifier capable of classifying 3 different porcelain marks from the Qing dynasty have been successfully modelled. While the model has an accuracy of 84%, it is acknowledged that it does struggles more with dirty images where the image of the porcelain mark itself do not occupy the majority of the image space. Nonethless, this project will therefore serve as a great base for further enhancement and improvement which will be discussed in the future works section.

**Future Works**
<br/>

As exhibited by the 10% increase in accuracy when the model is required to classify only clean images, the weakness of the model is in making the classification when there is too much noise in the image. One possibile way to counter this problem is to include an **object detection** function in the model. If the object detection is implemented properly, the classifier will only consider portion of image that it recognises as a porcelain mark. Which means the model will be less affected by noisy image data.

<br/>

Another area to expand the dimension of the project will be to **add more classes** of porcelain marks. We can start by including all the 10 important reign marks of the Qing Dynasty. Each reign mark can be found in either Zhuanshu or Kaishu which expands it into a 20-class classificaiton model. An expended model that can handle most of the important reign marks of Qing Dynasty will definitely be more beneficial for budding collectors and therefore attract them to use it.

<br/>

The final goal is to **deploy the classifier** on the website of East Inspirations as a way to engage customers who are interested chinese antique porcelain. Visitors of the website can submit an image of the porcelain mark they have and our model will be able tell them which reign mark it most likely is. Images submitted by the users can also be collected to add into our train data set to improve it's performance.This will hopefully help drive traffic to the website and increase awareness of our local business. 

