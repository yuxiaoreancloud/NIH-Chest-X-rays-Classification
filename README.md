# NIH-Chest-X-rays-Classification
An AWS Sandbox Project - Image Classification on Chest X-rays images 

This is an image classification task on NIH Chest X-rays dataset. There are multiple experiment results on multi-label classification and binary classification. For each task, first run the preprocess file, then run the model training files. 


Require files:

In order to run this code, first upload NIH Chest X-rays dataset to S3 (or in EFS). Images can be download from https://nihcc.app.box.com/v/ChestXray-NIHCC. In Sagemaker instance, make sure there are Data_Entry_2017.csv and blacklist.csv files in order to preprocess. 


Process:

First using the preprocess file to generate train tensors, validation tensors, test tensors, train labels, validation labels and test labels. Using at least ml.m4.10xlarge (Sagemaker) instance to avoid memory error. Store these 6 files to EFS. Notice these files can be over 40GB. Then in the model training files, load these 6 files, compile the model and load weight stored in google drive. Using at least ml.p2.xlarge instance to avoid memory error. 


Folder Content:
