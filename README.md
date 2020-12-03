# SeeFish iPhone app 

iOs app to recognize more than 400 tropical fishes species while scuba diving, using GCP AutoMLmVision/TFLite/Xcode framework.

## Overview

Running this app on an encased mobile phone allow the user to point the camera to a fish and get a prediction of the specie to which it belongs. 

The prediction are obtained using a classification model created with the Google Cloud Platform AutoML Vision module

This repository contains the python code necessary to prepare the dataset, the model to be used and instruction how to build th app for your own use.

The daset preparation is only necessary if you want to aplly this project to your own classification problem.

The app is TFLite sample app. 

# Dataset

The datset used is a subset of about 500 species extracted from the wildifsh dataset (1000 species total). The species choosen do not represent the totality of the tropical fish species, but the most common ones. 3 species of jellyfish were added to the dataset and were retrieved form the xxx dataset.

The WildFish daset did contain enough images for each class. To reach a number of images sufficient for the classification a number of images (uo to 150 for each class) were obtained scraping internet. 

# Image augumentation

Image augumentation (rotation, orizontal flip, noise) was used to enhance the training dataset (see Jupiter notebook).

# Create the classification model

The model SeeFish_1_0 is creted using the AutoML Vision module. The dataset need to uploaded to a Google Storage bucket and a corresponding csv file with location of the image need to be creted (see Jupiter notebook). After the upload is completed the training can be launched, specifing that the model will be deployed to an edge device.

After training download the obtained 'model.tflite' and files with class labels 'dict.txt'. For this project the moddel was renamed 'SeeFish_1_0' and the labels to 'labels.txt' for later integration in the app.

# Install the app

The model was tested on TFLite iOs sample Xcode app ImageClassification. The app is very simple: it classify whatever object the camera is pointing to and gives the probability of the best two classes. This simple functionality is ideal during scuba diving since there is no need to click anything, just pointing gives the results.

The TFLite model is build to run on Android, but can be used on an IOs device building an interpreter for the XCode application.

The detailed instruction on how to install the sample app and create the interpreter for XCode are in the following tutorial

https://codelabs.developers.google.com/codelabs/recognize-flowers-with-tensorflow-on-ios/#0

the output of this process is 'ImageClassification.xcworkspace' file that can be opened with Xcode

# Modify the ImageClassification app with XCode

the above tutorial is abit imprecise on how to integrate the model in the app. Here following is how I did it.

To run the SeeFish_1_0 on this app, the model need to be added to the the 'Model' folder (please remove the existing ones).
than in the 'ModelDataHandler.swift' replace the nammes of the files as shown below

Img/Screen Shot 2020-12-03 at 2.10.29 PM.png

# Build the app and enjoy it!

# Some screen shot of the app in action


