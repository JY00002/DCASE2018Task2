# Freesound-audio-tagging


[DCASE2018 Task2](http://dcase.community/challenge2018/task-general-purpose-audio-tagging) - General-purpose audio tagging of Freesound 
content with AudioSet labels

[Kaggle](https://www.kaggle.com/c/freesound-audio-tagging) - Freesound General-Purpose Audio Tagging Challenge


## What you can get from this repository?

1. Framework for audio-tagging or audio classification which based on PyTorch.

2. Audio data processing method and feature extraction method.

3. Encapsulation of multiple models for the audio data.


## Data

From Kaggle competition https://www.kaggle.com/c/freesound-audio-tagging/data


## Requirments:

python 3.6

pytorch 0.4.0

cuda 9.1

librosa 0.5.1

torchvision 0.2.1


## How to run?


#### Feature extraction.

```
python data_transform.py
```

This code can extract three types of features by selecting 
different functions:

* Wave
* Log-Mel
* MFCC

**Note:** To extract different features, you need to set 
different parameters in config.

In order to speed up the extraction process, we use parallel 
computing, you could modify the number of threads according 
to your computer situation.

We extract log-mel and MFCC features, the delta and accelerate 
of log-mel and MFCC are calculated. Then we concatenate log-mel 
or MFCC with delta and accelerate to form a 3 x 64 x N dimension
matrix where N depends on the length of audio files.


#### Train on Wave.

~~~
python train_on_wave.py
~~~

To train the network directly from waveform.

Before run it, you should instantiate Class config to set 
parameters (such as directory, learning rate, batch size, 
epoch...). Make sure the data you are using is the wave 
feature you extracted earlier.


#### Train on Log-Mel

~~~
python train_on_logmel.py
~~~

To train the network from log-mel feature.

Make sure the data you are using is the log-mel feature you 
extracted earlier.

#### Train on MFCC

~~~
python train_on_logmel.py
~~~

To train the network from MFCC feature using the same code, but 
you should use the MFCC feature you extracted earlier.


## Single Models

Several deep learning networks are encapsulated for sound data in the network_*.py, including:

* Resnet
* ResNeXt
* SE-ResNeXt
* DPN
* Xception

Also, you can find useful pretrained models in this [repository](https://github.com/Cadene/pretrained-models.pytorch).



## To be improved

* More efficient and high-performance models to be designed.

* Currently, the models are trained on single GPU. Multiple GPUs can be used for parallel training to accelerate learning.
