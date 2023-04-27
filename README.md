# CASA0018_PROJECT

# Telling different Electronic Instruments
Borui Wei

## Introduction

- overview of what the project does
This project explores the use of deep learning models in classifying different sound effects made by synthesizers, using kicks and toms as examples.  The project aims to address the challenges of analyzing sound components, which is essential in music production, sound effects creation, and other related fields. 

- inspiration for making this project

Traditionally, sound engineering techniques like Fourier analysis have been utilized, but they can be time-consuming and require technical expertise. To overcome these challenges, the project utilizes deep learning models that can understand and generate complex patterns in sound. The models are trained on large amounts of data to recognize different sound components and how they fit together. The report evaluates the effectiveness of these models in different tasks according to the way sounds are built, either additively or subtractively. This analysis helps identify the strengths and weaknesses of each model and provides insights on how to make better use of deep learning in sound analysis.


The report concludes by discussing the potential applications of deep learning in sound engineering and the future directions of this field. By utilizing deep learning models, sound engineers can create custom sounds and understand how they were made. This knowledge can be used to replicate sounds and add unique twists to them, improving the quality of music production, sound effects, and related fields. Overall, the report highlights the feasibility and potential of using deep learning models in sound engineering, opening up new possibilities in this field.

- examples the project is based on
The project is based on Tiny ML book, ELGE IMPULSE WEBSITE and CASA0018 module.

## Research Question
1. How effcient are the deep learning models in distinguishing different electronic instrumental sounds.

2. Explore what features in sound design are extracted by deep learning models.
## Application Overview
This application components were Edge Impulse and Arduino BLE33 microphone.

## Data 
The data can be sourced from KSHMR website: https://splice.com/sounds/packs/splice/kshmr-sok4-sample-pack/overview. The kicks and toms are played on the websites and recorded from the microphone. In the live testing, samples are used from both KSHMR Splice websites and self-contained audio sources from Ableton Live 10 Suite. 

The data samples are collected as sound clips of 15000 miliseconds at 16000 hertz by Arduino BLE33 built-in microphone on the interface provided by Edge Impulse.
These latter preprocessing steps are implemented within the models. The sampling rate is decided to satisfy the Nyquist's theorem for all samples. Around 80% of the data was splitted as training set and 20% as test set by data sampler provoided by Edge Impulse interface.



## Model

The model architecture chosen is MFE-conv1d-daf. 

Compared to the demo task where data was sampled through an audio loopback driver 'blackhole' that records computer audio play with minimal latency, MFE model performed better in later development of this task. 

This study employed deep learning techniques to discriminate between different types of sound. The MFE model was chosen as the pre-fitting technique, which extracted 640 features from the data, reshaped the layer into 32 columns, and applied three 1-dimensional convolutional layers, followed by a Flatten layer and a dropout layer, to output the features into two categories. The training process consisted of 100 cycles at a learning rate of 0.005.

The EON Tuning tool on Edge impulse was utilized to select the most suitable models, which identified the MFE and spectrogram models as the optimal choices. The spectrogram model outperformed the MFE model by approximately 4% on the test set and had lower performance latency. Given that the time windows were set as 1000ms, covering most of the time spans of the samples, the MFE appeared to have the same sampling range as the spectrogram model, which windowed over the entire time span of individual samples. This suggests that there was no need to be concerned about the spectrogram model not providing as much detail as the MFE. The performance of both models on the validation and test datasets is depicted on the subsequent slide.

Lastly, the deployment of the model on an Arduino device was discussed. The peak RAM and flash usages were found to be moderate, indicating that the model was relatively lightweight.


## Experiments




## Results and Observations




The model was broadly tested by a wide range of sound clips labeled toms and kicks. And these test samples are also characterized in their names as 'cinematic', 'acoustic' etc, which may indicate these clips are quite different in design even within each label. Utilizing the variety of clips can be  It can be noticed that the different characteristics in resnotation and change in frequencies in the two types of sounds are captured by the model. In this example below, a kick that appears to have longer resonation is wa smissclassified as tom. 
<img width="946" alt="mc_kick_reson" src="https://user-images.githubusercontent.com/116358733/234876502-af5544a2-1b04-45b6-a801-41c3e5366c61.png">

Another example shows how a kick with obvious change in frequency(pitch) can be misclassified as 








## Authorship

