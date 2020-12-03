# SeeFish iPhone app 

iOS app to recognize more than 400 tropical fishes species while scuba diving, using GCP AutoMLmVision/TFLite/Xcode framework.

## Overview

Running this app on an encased mobile phone allows the user to point the camera to a fish and predict the species to which it belongs. 

The prediction is obtained using a classification model created with the Google Cloud Platform AutoML Vision module.

This repository contains the Jupietr Notebook python code necessary to prepare the dataset, the model to be used, and instructions on how to build the app for your use.

The dataset preparation is only necessary if you want to apply this project to your classification problem.

The app is TFLite sample app. 

# Dataset

The dataset used is a subset of about 500 species extracted from the WildiFish dataset (1000 species total) (1). The species chosen do not represent the totality of the tropical fish species, but the most common ones. Three species of jellyfish were added to the dataset and were retrieved form the 'Jellyfish' dataset(2).

The WildFish dataset did contain enough images for each class. To reach the number of images sufficient for the classification task, some images (up to 150 for each class) were obtained scraping the internet. 

# Image augmentation

Image augmentation (rotation, horizontal flip, noise) was used to enhance the training dataset (see Jupiter notebook).

# Create the classification model

The model SeeFish_1_0 is created using the AutoML Vision module. The dataset needs to upload to a Google Storage bucket, and a corresponding CSV file with the location of the image needs to be created (see Jupiter notebook). After the upload is completed, the training can be launched, specifying that the model will be deployed to an edge device.

After training, download the obtained 'model. tflite' and files with class labels 'dict.txt.' For this project, the model was renamed 'SeeFish_1_0' and the labels to 'labels.txt' for later integration in the app.
The files are in the 'Model' folder of this repository.

# Install the app

The model was tested on TFLite iOs sample Xcode app ImageClassification. The app is straightforward: it classifies whatever object the camera is pointing to and gives the probability of the best three classes. This simple functionality is ideal during scuba diving since there is no need to click anything; just pointing gives the results.

The TFLite model is built to run on Android but can be used on an IOs device, building an interpreter for the XCode application.

The detailed instructions on how to install the sample app and create the interpreter for XCode are in the following tutorial:

https://codelabs.developers.google.com/codelabs/recognize-flowers-with-tensorflow-on-ios/#0

the output of this process is 'ImageClassification.xcworkspace' file that can be opened with Xcode

# Modify the ImageClassification app with XCode

The above tutorial is a bit imprecise on how to integrate the model in the app. Here following is how I did it.

To run the SeeFish_1_0 on this app, the model needs to be added to the 'Model' folder (please remove the existing ones).

Then in the 'ModelDataHandler.swift' replace the names of the files as shown below:

https://github.com/vittorio-pepe/SeeFish-iPhone-app---462/blob/main/Img/Screen%20Shot%202020-12-03%20at%202.10.29%20PM.png?raw=true

# Build the app, and enjoy it!

# Some screenshot of the app in action

https://github.com/vittorio-pepe/SeeFish-iPhone-app---462/blob/main/Img/IMG_0008.PNG?raw=true
https://github.com/vittorio-pepe/SeeFish-iPhone-app---462/blob/main/Img/IMG_0010.PNG?raw=true
https://github.com/vittorio-pepe/SeeFish-iPhone-app---462/blob/main/Img/IMG_0013.PNG?raw=true

# Useful links

The link to original datasets are here:

https://github.com/PeiqinZhuang/WildFish

https://zenodo.org/record/3545785#.X8lj5KpKh24

# References for the datasets

(1) WildFish dataset:
Zhuang, Peiqin and Wang, Yali and Qiao, Yu,’ WildFish: A Large Benchmark for Fish Recognition in the Wild’, ACM Multimedia Conference on Multimedia Conference, 2018, p. 1301-1309.

(2) Jellyfish dataset:
Ruiz-Frau, Ana, Hintz, Hilmar and Jennings, Charlotte (2019, Nov 11) 'Jellyfish dataset', https://zenodo.org/record/3545785#.X8lj5KpKh24


