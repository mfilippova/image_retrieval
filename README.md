# Image retrieval for medical images’ applications

This repository reflects the work done in my master's thesis.

## Motivation for Content Based Image Retrieval

When we analyze medical images with artificial intelligence we need to make medical decisions very carefully because the cost of a mistake is human health. So, we need to interpret the diagnosis made by artificial intelligence to validate the diagnosis by medical workers. Unfortunately, neural networks are black box algorithms, that are hard for interpretation.

The solution is to make a Content based image retrieval system for neural networks, that will find medical images with similar appearance and with the same diagnosis based only on the content of the image.

## Content Based Image Retrieval pipeline

Preparation stage:

* Train a convolutional neural network on a label related to the task 
* Get feature descriptions for all train images, providing to the backbone

Evaluation/Usage stage:

* Evaluated image is passed into the same backbone, which extracts its feature vector
* Compute distance metric between the vector of evaluating image and all vectors from train images
* Choose k closest vectors and get their images

## Datasets

[RSNA Pneumonia Detection Challenge](https://www.kaggle.com/competitions/rsna-pneumonia-detection-challenge/overview):

* 26684 Chest X-ray exam images all for unique patients
* Binary label for the presence of pneumonia
* Bounding boxes detecting the presence of pneumonia

NIH Chest X-ray Dataset (Wang et al., [2017](http://openaccess.thecvf.com/content_cvpr_2017/papers/Wang_ChestX-ray8_Hospital-Scale_Chest_CVPR_2017_paper.pdf)):

* Binary labels for the for the presence of the 14 classes of lung diseases. One patient can have more than one lung disease.

## Models

| | First stage | Second stage |
|---|---|---|
|1. | Binary classification (Baseline) | kNN |
|2. | Binary classification + Hash layer | prefilter with Hamming + kNN |
|3. | Multilabel classification | kNN |
|4. | Detection | kNN |

## Results

| Approach | First stage ROC-AUC <br /> for Pneumonia class, % | Second stage accuracy, % |
|---|:---:|:---:|
| Binary classification (Baseline) | 83.57 | 78.67 |
| Binary classification with hash layer | 83.72 | 79.85 |
| Multilabel classification | **84.03** | **80.04** |
| Detection | 83.19 | 79.48|


