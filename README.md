# Python Emotion Recognition using EEG Signals
This repository contains the code for emotion recognition using wavelet transform and svm classifiers' rbf kernel.

## Abstract: ##
This paper aims to propose emotion recognition using electroencephalography (EEG) techniques.​ ​An electroencephalogram (EEG) is a machine  that detects electrical activity in a human brain using small metal discs (electrodes) attached to the scalp. The brain cells communicate via electrical impulses and are active all the time, even when we are asleep. This activity shows up as wavy lines on an EEG recording.

## Dataset Summary ##

The data set contains downsampled signal, preprocessed and segmented versions of the EEG data in Matlab (.mat file). The data was downsampled to 200Hz. A bandpass frequency filter from 0-75Hz was applied. EEG segments were extracted according to the duration of clips. There are a total of 45 .mat (Matlab) files, one for each experiment. Each subject performed the experiment three times with an interval of about one week. Each subject file contains 16 arrays. 15 arrays contain segmented preprocessed EEG data of 15 trials in one experiment (eeg_1~eeg_15, channel×data). An array named ‘labels’ contains the label of the corresponding emotional labels (-1 for negative, 0 for neutral and +1 for positive). The detailed order of the channels is included in the dataset.

## Steps involved ##
**Preprocessing:**
The ‘preprocess’ function consists of filtering data to between 0 to 75 Hz. It returns a new matrix with sampling frequency as 200Hz and between 0 to 75Hz. We used Finite Impulse Response ‘Low pass filter’. Bandpass was not used as it would make the eeg data unstable after processing. Filter order = 5 (or 10 if desired results are not obtained).

**Feature Extraction:**
In the feature extraction phase, we divide the eeg pre-processed input into 5 frequency sub bands using wavelet filter banks technique.
In order to separate the five types of signal in the eeg recording i.e., alpha, beta, gamma, delta and theta as explained above, we use wavelet transform’s filter banks to separate the different frequencies. In the lower level, there is a filter that separates the frequency band in half and gives us high pass (detail coefficient) and low pass (approximation coefficient). We further take the approximation coefficient and pass it through the filter. We do this until the desired frequency ranges are not achieved. Since the filters are successively applied, they are known as filter banks.
We repeat the process for each channel. In each iteration for 62 channels, we extract entropy and energy for each sub-band i.e., 10 features for each channel. The feature extraction is complete with each eeg pre processed signal having output of 620 features.

**1. Entropy:** Entropy measures quantify the uncertainty in the EEG, which roughly equates to the possible configurations or their predictability.

**2. Energy:** Wavelet energy reflects the distribution of the principal lines, wrinkles and ridges in different resolutions(scales).

**Feature Reduction:** 
In the feature reduction phase, we use Principal Component Analysis or PCA. PCA is an eigenvector-based statistical mechanism, which employs singular value decomposition, that transforms a set of correlated features into mutually uncorrelated training features, principal components or PCs. 
Steps to perform Principal Components Analysis:
1. Mean normalisation of features.
2. Calculating Covariance Matrix.
3. Calculate EigenVectors.
4. Get the reduced features or principal components.

After this process, we receive principal components PCs.

**Classification:** 

The PCs from the previous step will be fed into the SVM classifier for output into emotions.


**This project would not have been possible without:** 
1. [Wavelet transform](http://users.rowan.edu/~polikar/WTtutorial.html).
2. [Principal Components Analysis](https://www.coursera.org/learn/machine-learning).
3. [Support Vector Machines](https://www.coursera.org/learn/machine-learning).
4. [Seed Dataset](http://bcmi.sjtu.edu.cn/~seed/).

**Note:** Please send an email to shivamc021999@gmail.com for further queries or collaborations.

**Note2:** Please refer to [this](https://bcmi.sjtu.edu.cn/~seed/downloads.html#seed-access-anchor) link to get access to the dataset.
