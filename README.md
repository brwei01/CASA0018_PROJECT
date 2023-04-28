# CASA0018_PROJECT

# Telling different Electronic Instruments -- using toms and kicks as example
Borui Wei

## 1. Introduction

This project employed deep learning techniques to discriminate between synthesizer engineered sound effects/clips of 2 types of instruments in a drum rack -- kicks and toms. The inspiration of this project comes from the examples of projects "letting your sensors to hear" introduced by Edge Impulse. The MFE, MFCC and Spectrogram models are well suitated the need of sound detection or classification.
The objective is to explore the ability of deep learning models to tell different tone colours with the help of sensors. Sometimes in music production especially electronic sound engineering, there are sounds that easily to get mixed with others, like toms and kicks. Deep learning models 'hears' different sounds in a quite different way -- by analyzing the spectrograms ('seeing' the sound rather than hearing).


The project has developed an application that can be deployed on an Arduino BLE33 sensor through the help of Edge Impulse. The application can be runned either on desktop terminal, or By deploying it on a suitable sensor, the model embedded will analyse the singal that the sensor has to intake, and returns an answer determining whether the sound clip is likely to be a kick or tom. Given an accuracy of 80%, the application is relatively trustful in classifying these 2 instruments from a drum rack.



## 2. Research Question

1. How effcient are the deep learning models combined with sensors in distinguishing different electronic instrumental sounds.

2. What features in sound design are extracted by deep learning models.


## 3. Application Overview
### 3.1. Application build
This application components were Edge Impulse, Arduino BLE33 microphone and the Arduino IDE. Edge Impulse, as an end-to-end development platform for building and deploying machine learning models on edge devices played an important role in linking the components together by accomplishing the following tasks:  
1. Generating files to update the firmware on Arduino BLE33 and make it ready for connection;
2. Operating the sensor to sample data, and train-test set splitting of sampled data;
3. Model building, training, and testing (with test set or live testing with new clips recorded);
4. Generating model deployment solutions for Arduino sensor that can be runned by desktop shell command or the Arduino IDE.


In terms of the hardwares, The Arduino BLE33 sensor that has recording functionality is required to be connected to a supportive desktop so that it can be operated through Edge Impulse in data sampling and live testing tasks, or the deployment through desktop shell command and Arduino IDE. A flow chart that illustrate the application build is shown in the flow chart below:
<img width="894" alt="build_flowchart" src="https://user-images.githubusercontent.com/116358733/235208217-a90b39aa-abdb-4fda-8538-c060ec7217ca.png">


### 3.2. System requirements
The system requirements where this project is developed and tested is provided as follows:
- macOS Catalina version 10.15.4
- Arduino IDE (2.0.3)
 

### 3.3.  application deployment and testing
This application can be deployed and tested on Arduino BLE33 sensor in two ways: 
1. A ready-to-use shell application that can be runned directly on a desktop with Arduino BLE33 sensor connected. By cloning down the folder named "drum-rack-nano-ble33-sense" in this repository to local, run the 'flash-mac.command' file to install the mapplication firmware on the sensor. After the installation is finished, start up a new command window and run command:
``` edge-impulse-run-impulse ``` 
The application will run and log the following in the terminal on your desktop. The sound clip should be played after the 'Recording' prompt and the results are printed at the end of each classification loop:
``` 
Starting inferencing in 2 seconds...
Recording...
Recording done
Predictions (DSP: 33 ms., Classification: 31 ms., Anomaly: 0 ms.): 
    kick: 0.73047
    tom: 0.26953
```


2. A library for Arduino IDE -- By downloading the zip file named 'ei-drum-rack-arduino-1.0.2.zip' to the local. This zip file can then be included as a library in Arduino IDE. 

<img width="1440" alt="include_library" src="https://user-images.githubusercontent.com/116358733/235198515-e73e1a18-95a4-4f1c-a4f0-5d884c921cfb.png">

Then download and open up the sketch file '/nano_ble33_sense_microphone/nano_ble33_sense_microphone.ino', click upload button to run the application. The output can be monitored via Tools > Serial monitor where the signal processing pipeline can be started. The 'baud rate' is recommended to be set at 115200, which indicates the data sent by the Arduino board will be transmitted at a speed of 115,200 bits per second.






## 4. Data 
The data sampled can be sourced from KSHMR website: https://splice.com/sounds/packs/splice/kshmr-sok4-sample-pack/overview. The kicks and toms are played on the websites and recorded from the microphone. In the live testing, samples are used from both KSHMR Splice websites and self-contained audio sources from Ableton Live 10 Suite. 

The data samples are collected as sound clips of 15000 miliseconds at 16000 hertz by Arduino BLE33 built-in microphone on the interface provided by Edge Impulse.
These latter preprocessing steps are implemented within the models. The sampling rate is decided to satisfy the Nyquist's theorem for all samples. Around 80% of the data was splitted as training set and 20% as test set by data sampler provoided by Edge Impulse interface.



## 5. Model
- model choice
The model architecture chosen is Spectr-conv1d-3de. 

The MFE model was chosen as the pre-fitting technique, which extracted 640 features from the data, reshaped the layer into 32 columns, and applied three 1-dimensional convolutional layers, followed by a Flatten layer and a dropout layer, to output the features into two categories. The training process consisted of 100 cycles at a learning rate of 0.005.

The EON Tuning tool on Edge impulse was utilized to select the most suitable models, which identified the MFE and spectrogram models as the optimal choices. The spectrogram model outperformed the MFE model by approximately 4% on the test set and had lower performance latency. Given that the time windows were set as 1000ms, covering most of the time spans of the samples, the MFE appeared to have the same sampling range as the spectrogram model, which windowed over the entire time span of individual samples. This suggests that there was no need to be concerned about the spectrogram model not providing as much detail as the MFE. The performance of both models on the validation and test datasets is depicted on the subsequent slide.

Lastly, the deployment of the model on an Arduino device was discussed. The peak RAM and flash usages were found to be moderate, indicating that the model was relatively lightweight.


- differences and improvements from the demo task

Compared to the demo task where data was sampled through an audio loopback driver 'blackhole' that records computer audio play with minimal latency, MFE model performed better in later development of this task. The model has two main differences in data preprocessing from the spectrogram used in demo task.

In model structure, the MFE model 

## 6. Experiments




## 7. Results and Observations


The model was broadly tested by a wide range of sound clips labeled toms and kicks. And these test samples are also characterized in their names as 'cinematic', 'acoustic' etc, which may indicate these clips are quite different in design even within each label. Utilizing the variety of clips can be  It can be noticed that the different characteristics in resnotation and change in frequencies in the two types of sounds are captured by the model. In this example below, a kick that appears to have longer resonation is was misclassified as tom. 
<img width="946" alt="mc_kick_reson" src="https://user-images.githubusercontent.com/116358733/234876502-af5544a2-1b04-45b6-a801-41c3e5366c61.png">

Another example shows how a kick with obvious change in frequency(pitch) can be misclassified as 








## 8. Authorship

