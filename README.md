# CASA0018_PROJECT

# Telling different Electronic Instruments
Borui Wei

## Introduction

This project employed deep learning techniques to discriminate between synthesizer engineered sound effects/clips of 2 types of instruments in a drum rack -- kicks and toms. The inspiration of this project comes from the examples of projects "letting your sensors to hear" introduced by Edge Impulse. The MFE, MFCC and Spectrogram models are well suitated the need of sound detection or classification.
The objective is to explore the ability of deep learning models to tell different tone colours with the help of sensors. Sometimes in music production especially electronic sound engineering, there are sounds that easily to get mixed with others, like toms and kicks. Deep learning models 'hears' different sounds in a quite different way -- by analyzing the spectrograms ('seeing' the sound rather than hearing).


The project has developed an application that can be deployed on an Arduino BLE33 sensor through the help of Edge Impulse. By deploying it on a suitable sensor, the model embedded will analyse the singal that the sensor has to intake, and returns an answer determining whether the sound clip is likely to be a kick or tom. Given an accuracy of 80%, the application is relatively trustful in classifying these 2 instruments from a drum rack.



## Research Question

1. How effcient are the deep learning models combined with sensors in distinguishing different electronic instrumental sounds.

2. What features in sound design are extracted by deep learning models.


## Application Overview
- Application build
This application components were Edge Impulse and Arduino BLE33 microphone. Edge Impulse was used in three main ways: 
1. Data Sampling, Train-test Splitting;
2. Model building, training, and testing;
3. Model deployment to Aruidno

- deployment and testing
This application can be deployed on Arduino BLE33 by cloning down the files in this repository. By runing the file written in shell, it can


## Data 
The data sampled can be sourced from KSHMR website: https://splice.com/sounds/packs/splice/kshmr-sok4-sample-pack/overview. The kicks and toms are played on the websites and recorded from the microphone. In the live testing, samples are used from both KSHMR Splice websites and self-contained audio sources from Ableton Live 10 Suite. 

The data samples are collected as sound clips of 15000 miliseconds at 16000 hertz by Arduino BLE33 built-in microphone on the interface provided by Edge Impulse.
These latter preprocessing steps are implemented within the models. The sampling rate is decided to satisfy the Nyquist's theorem for all samples. Around 80% of the data was splitted as training set and 20% as test set by data sampler provoided by Edge Impulse interface.



## Model
- model choice
The model architecture chosen is MFE-conv1d-daf. 

 The MFE model was chosen as the pre-fitting technique, which extracted 640 features from the data, reshaped the layer into 32 columns, and applied three 1-dimensional convolutional layers, followed by a Flatten layer and a dropout layer, to output the features into two categories. The training process consisted of 100 cycles at a learning rate of 0.005.

The EON Tuning tool on Edge impulse was utilized to select the most suitable models, which identified the MFE and spectrogram models as the optimal choices. The spectrogram model outperformed the MFE model by approximately 4% on the test set and had lower performance latency. Given that the time windows were set as 1000ms, covering most of the time spans of the samples, the MFE appeared to have the same sampling range as the spectrogram model, which windowed over the entire time span of individual samples. This suggests that there was no need to be concerned about the spectrogram model not providing as much detail as the MFE. The performance of both models on the validation and test datasets is depicted on the subsequent slide.

Lastly, the deployment of the model on an Arduino device was discussed. The peak RAM and flash usages were found to be moderate, indicating that the model was relatively lightweight.


- differences and improvements from the demo task

Compared to the demo task where data was sampled through an audio loopback driver 'blackhole' that records computer audio play with minimal latency, MFE model performed better in later development of this task. The model has two main differences in data preprocessing from the spectrogram used in demo task.

In model structure, the MFE model 

## Experiments




## Results and Observations




The model was broadly tested by a wide range of sound clips labeled toms and kicks. And these test samples are also characterized in their names as 'cinematic', 'acoustic' etc, which may indicate these clips are quite different in design even within each label. Utilizing the variety of clips can be  It can be noticed that the different characteristics in resnotation and change in frequencies in the two types of sounds are captured by the model. In this example below, a kick that appears to have longer resonation is wa smissclassified as tom. 
<img width="946" alt="mc_kick_reson" src="https://user-images.githubusercontent.com/116358733/234876502-af5544a2-1b04-45b6-a801-41c3e5366c61.png">

Another example shows how a kick with obvious change in frequency(pitch) can be misclassified as 








## Authorship

