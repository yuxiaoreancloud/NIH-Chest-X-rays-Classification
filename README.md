# NIH-Chest-X-rays-Classification
An AWS Sandbox Project - Image Classification on Chest X-rays images 

Description: 
In recent years there is a huge push for Computer-assisted Diagnosis (CAD) and organizations such as NIH published on of the largest public x-ray datasets with more than 112,000 chest x-ray of more than 30,000 unique patients suffering from 14 different Thorax diseases. 

In this project, We built CNN models to screen a particular medical condition and models to classify chest x-rays into 14 pathology classes. We conduct multiple experiments on multi-label classification and binary classification. For each task, run the preprocess file first, then run the model-training files. 

------------------------------------------------------------------------------------------------------------------------------------------

Require files:

In order to run this code, first upload NIH Chest X-rays dataset to S3 (or in EFS). Images can be download from https://nihcc.app.box.com/v/ChestXray-NIHCC. In Sagemaker instance, make sure to have Data_Entry_2017.csv, train_val_list.txt, test_list.txt and blacklist.csv files in order to preprocess. 

------------------------------------------------------------------------------------------------------------------------------------------

Process:

First using the preprocess file to generate train tensors, validation tensors, test tensors, train labels, validation labels and test labels. Using at least ml.m4.10xlarge (Sagemaker) instance to avoid memory error. Store these 6 files in EFS. Notice these files can be over 40GB. 

Second, in the model-training files, load these 6 files, compile the model and load weights stored in the google drive: https://drive.google.com/drive/folders/1BLpz3zg7l5MqlV1D26LVTuucGhGKqDkm?usp=sharing. Using at least ml.p2.xlarge instance to avoid memory error. 

------------------------------------------------------------------------------------------------------------------------------------------

Folder Content:

  Multi-label classification

    1. Preprocess X-rays images by cropping, removing blacklist, and loading images as size 300 * 300. Then using pre-trained model         DenseNet169 in keras with modified densely connect layer to train model. Use Adam as opitmizer.
  
    preprocess: nit-preprocess-multi-crop-noBlack.ipynb
    train-model: model-100%300CropRemoveBlack-169-AdamBest.ipynb
    weights: 300Crop169Adam.hdf5


    2. Same as 1, except using SGD as optimizer.
  
    preprocess: nit-preprocess-multi-crop-noBlack.ipynb
    train-model: model-100%300CropRemoveBlack-169-SGD.ipynb
    weights: 300Crop169SGD.hdf5
  
    3. Same as 1, except oversample under-represented samples. Oversampling details is in preprocess file. 
  
    preprocess: nit-preprocess-multi-crop-noBlack-balanced.ipynb
    train-model: model-100%300CropRemoveBlack-169-SGD-balanced.ipynb
    weights: 300Crop169SGDbalanced.hdf5
  
    4. Drop out 'No Finding' Class and train on the remaining samples. 
  
    preprocess: nit-preprocess-disease-712.ipynb
    train-model: model-mulitlabel-diseaseOnly-712.ipynb
    weights: multilabel_diseaseOnly712.hdf5
  
  
  
  Binary Classification 
  1. Binary classification to classify fibrosis or non-fibrosis.
  
    preprocess: nit-preprocess-224CropRemoveBlack-fibrosis.ipynb
    train-model:model-224CropRemoveBlack-fibrosis.ipynb
    weights: fibrosis.hdf5
    
  2. Binary classification to classify No Finding or disease.
  
    preprocess: nit-preprocess-binary.ipynb
    train-model:model-binary-NForDisease.ipynb
    weights: binary_balanced.hdf5
  
