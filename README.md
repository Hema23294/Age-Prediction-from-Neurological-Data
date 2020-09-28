# Age Prediction from Neurological Data

The purpose of this project was to predict the age given multimodal brain features such as 3D functional spatial maps from resting-state functional MRI,
static functional network connectivity (FNC) matrices, and source-based morphometry (SBM) loading values from structural MRI. 

## About the features used:

The first set of features are source-based morphometry (SBM) loadings. These are subject-level weights from a group-level
ICA decomposition of gray matter concentration maps from structural MRI (sMRI) scans.

The second set are static functional network connectivity (FNC) matrices. These are the subject-level cross-correlation values among 53 component 
timecourses estimated from GIG-ICA of resting state functional MRI (fMRI).

The third set of features are the component spatial maps (SM). These are the subject-level 3D images of 53 spatial networks estimated from GIG-ICA of
resting state functional MRI (fMRI).

## About the dataset:

The following files were provided by TreNDS Neuroimaging research :-

fMRI_train - a folder containing 53 3D spatial maps for train samples in .mat format

fMRI_test - a folder containing 53 3D spatial maps for test samples in .mat format

fnc.csv - static FNC correlation features for both train and test samples

loading.csv - sMRI SBM loadings for both train and test samples

train_scores.csv - age and assessment values for train samples

sample_submission.csv - a sample submission file in the correct format

reveal_ID_site2.csv - a list of subject IDs whose data was collected with a different scanner than the train samples

fMRI_mask.nii - a 3D binary spatial map

ICN_numbers.txt - intrinsic connectivity network numbers for each fMRI spatial map; matches FNC names

## Project Flow:

The EDA was done to understand the distribution of the dataset and the correlation between the features.

the following were observed:-

![image info](Capture.JPG)

Top 5 most frequent ages are 57, 60, 54, 55, 50

Most of the patients lie between the age group 22 to 77

![image info](Heat.JPG)

IC_13 and IC_14 has a correlation value as high as 0.55

IC_10 and IC_22 are also very highly negative correlated with correlation value -0.54


Following this a Deep Neural Network for Predicting Age Using Keras was developed with MSE loss and Adam optimizer. Dropout layers were added to achieve a more robust model
by avoiding overfitting.

Finally a feature weighted, normalized absolute error of 0.1610 was achieved with the model. 

Following this I experimented the model using RAPIDS by replacing pd with cuDF. This made the model run 87 times faster by drastically reducing the loading time of the files.

