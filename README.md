![NebraskaMedicineSign062320](https://user-images.githubusercontent.com/102309439/178884966-c471b510-1842-4a58-b66b-1bc69161954c.jpg)


# Convolutional Neural Network - Breast Histopathology Image Classification

## Overview 


---


This repository presents a deep learning approach (Convolutional Neural Network - CNN) for automatic detection, visual analysis, and classification of invasive ductal carcinoma (IDC) tissue regions in whole slide images (WSI) of breast cancer.

## Business Problem 

--- 

Invasive breast cancer detection is a tedious and difficult task. Like searching for a needle in a haystack, a pathologist must scan vast stretches of benign regions to (maybe) identify a small plot of malignancy within. Accurate and precise identification of IDC tissue regions is critical for the subsequent tumor aggression and patient outcome calculations and predictions. 


The Pathology Specialists at the University of Nebraska Medical Center (UNMC) approached us with the following problems: 

- Overworked pathologists and elevated physician burnout rates
- Commonly misidentified or unidentified IDC in breast cancer WSI


After discussing their problems, and the available data, we created the following goals: 

- To be used as either a preliminary scan or a fail-safe check, create a model that will save UNMC pathologists time, increase accuracy, and reduce misidentified and unidentified malignant regions within samples. 


- Create a model that can accurately identify and categorize tissue regions in WSI of breast cancer with over 90% accuracy, and over 90% recall. 

![pone 0177544 g001 PNG_L](https://user-images.githubusercontent.com/102309439/178885007-4d9e6e97-2e79-486f-9578-ec934f493fac.png)


## Data Understanding 

---
According to Kaggle, the original dataset consisted of 162 whole mount slide images of Breast Cancer (BCa) specimens scanned at 40x. From that, 277,524 patches of size 50 x 50 were extracted (198,738 IDC negative and 78,786 IDC positive). Each patch’s file name is of the format: uxXyYclassC.png — > example 10253idx5x1351y1101class0.png . Where u is the patient ID (10253idx5), X is the x-coordinate of where this patch was cropped from, Y is the y-coordinate of where this patch was cropped from, and C indicates the class where 0 is non-IDC and 1 is IDC.

In order to create a digestible size of data, I randomly selected images and randomly sorted them into my Test, Train, and Validation sets, each containing two subset folders: Cancer and Normal. 

![Screen Shot 2022-07-11 at 8 31 14 AM](https://user-images.githubusercontent.com/102309439/178885059-e3811ebe-96ab-4dd6-82c4-9ed42305467f.png)

Test
  - Normal: 773 images 
  - Cancer: 208 images

Train
  - Normal: 2,943 images
  - Cancer: 3,920 images

Validation
  - Normal: 65 images
  - Cancer: 44 images

In total, there were 3,781 Normal image scans and 4,172 Cancer image scans. I built data generation and image augmentation into our model, allowing us to train our final model with 555,903 images. 

## Methodology and Results 

---

### Model 1: Logistic Regression (Simple Baseline Model) 
After exploring the data and building in extra data generation/image augmentation, the first model I created was a simple logistic regression model. A Logistic regression model estimates the probability of an event occurring, "cancerous" or "normal". This scored surprisingly well, at 83% accuracy and 78% recall. 

![logistic_regression](https://user-images.githubusercontent.com/102309439/178885112-ad253ea0-f07d-45f8-8374-4e2006191058.png)

---

### Model 2: Baseline CNN Model  
![model_2_cnn_baseline](https://user-images.githubusercontent.com/102309439/178885180-e7fd2dce-e21d-453a-a79f-f22dca0e5443.png)

Moving into deep learning models, the baseline convolution neural network produced some interesting results. The training data scored with 83% accuracy and 95% recall, yet the test data scored with 90% accuracy and 88% recall. 

This could be due to the nature of my data split. In order to create a digestible data size I randomly selected samples from only a few (4-6) patients for my test set, which may have been easier to classify than the entire population(15-20 patients). Thus, perhaps, my model is not very generalizable. This should be explored in future testing. 

---

### Model 3: CNN - Addition of MaxPool2d and Conv2d layers  
![model_3_cnn](https://user-images.githubusercontent.com/102309439/178885206-fa92d39e-8557-48cf-b7c8-c731279fa779.png)

In my third model I added MaxPool2d and Conv2d layers. Here we see the training score increase slightly to 84% and the recall decrease to 88%. On the testing data we see the accuracy score decrease to 88% and our recall decrease to 85%.

### Model 4 (Final Model): CNN - Change optimizer, add batch normalization, add paddin
![model_4_cnn](https://user-images.githubusercontent.com/102309439/178885232-65ec3c38-4c66-464f-9519-d86ba3a5c7d8.png)

Here we changed our optimizer to rmsprop, added batch normalization and padding. 

Despite MaxPool2d and Conv2d lowering the previous model's performance, this model performed better with those layers still present. 

We see the test scores increase to 90.1% and recall increase to 89%. 
![confusion_matrix_heatmap](https://user-images.githubusercontent.com/102309439/178885258-e63fae72-64ee-4870-8dce-4d03cfe89f46.png)

---

## Conclusion 

A primary recommendation to my stakeholder would be to use this final model as a preliminary detection technique. Pathologists may spend literally hours on end scanning hundreds of whole slide images with a very real chance of coming across no malignant cells. Seeing the accuracy and recall of my model, I'm confident it has the ability to perform a preliminary scan, in a fraction of the time, to determine whether or not a patient's biopsy contains malignant cells. 

This helps address the business problem from multiple angles. It not only saves physicians time and reduces burnout, but it helps inform them specifically where they should expend their time and energy, reducing errors and misdiagnosis. Ultimately, this takes stress off the provider and helps the patient receive the highest-level quality of care. 

---

## Limitations and Next Steps 

Working with limited time and limited computing capacity, I was restricted in the number of samples/patients I was able to analyze and train my model with. While I had access to over 100 patients' WSIs, I was only able to use a fraction of these, which could've skewed my data and made it less generalizable. Further, I didn't have access to any demographic information like age, sex, symptoms, etc., which I believe are features that could've helped create a more informed model. 

Moving forward, in addition to utilizing greater computing power, I believe that topographical and proximal location information on cells would be highly valuable information, allowing for the creation of a more accurate and precise model. Further, I would like to look into applying this model for the diagnosis of other types of scans and cancers. 

---
##### *Disclaimer*
*I do not hold any rights to any images used or have any affiliations to any of the institutions named within this repository.  Any use is for educational and demonstrative purposes only to simulate a legitimate stakeholder.* 



