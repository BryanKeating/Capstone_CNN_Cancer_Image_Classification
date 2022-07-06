# Convolutional Neural Network - Breast Histopathology Image Classification 

## Overview 
---
This repository presents a deep learning approach (Convolutional Neural Network - CNN) for automatic detection, visual analysis, and classification of invasive ductal carcinoma (IDC) tissue regions in whole slide images (WSI) of breast cancer.

## Business Problem 

---

Invasive breast cancer detection is a tedious and difficult task. Like searching for a needle in a haystack, a pathologist must scan vast stretches of benign regions to (maybe) identify a small plot of malignancy within. Accurate and precise identification of IDC tissue regions is critical for the subsequent tumor aggression and patient outcome calculations and predictions. 


The Pathology Specialists at the University of Nebraska Medical Center (UNMC) approached us with the following problems: 

- Overworked pathologists, and elevated physician burnout rates
- Commonly misidentified or unidentified IDC in breast cancer WSI


After discussing their problems, and the available data, we created the following goals: 

- To be used as either a preliminary scan or a fail-safe check, create a model that will save UNMC pathologists time, increase accuracy, and reduce misidentified and unidentified malignant regions within samples. 


- Create a model that can accurately identify and categorize tissue regions in WSI of breast cancer with over 90% accuracy, and over 90% recall. 

## Data Understanding 

---
According to Kaggle, the original dataset consisted of 162 whole mount slide images of Breast Cancer (BCa) specimens scanned at 40x. From that, 277,524 patches of size 50 x 50 were extracted (198,738 IDC negative and 78,786 IDC positive). Each patch’s file name is of the format: uxXyYclassC.png — > example 10253idx5x1351y1101class0.png . Where u is the patient ID (10253idx5), X is the x-coordinate of where this patch was cropped from, Y is the y-coordinate of where this patch was cropped from, and C indicates the class where 0 is non-IDC and 1 is IDC.

In order to create a digestable size of data, I randomly selected images and randomly sorted them into my Test, Train, and Validation sets, each containing two subset folders: Cancer and Normal. 

Test
  - Normal: 773 images 
  - Cancer: 208 images

Train
  - Normal: 2,943 images
  - Cancer: 3,920 images

Validation
  - Normal: 65 images
  - Cancer: 44 images

In total, there were 3,781 Normal image scans and 4,172 Cancer image scans. We built data generation and image augmentation into our model, allowing us to train our final model with 555,903 images. 

## Methodology and Results 

---
### Model 1: Logistic Regression 

