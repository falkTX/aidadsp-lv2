# Aida DSP lv2 plugin bundle #

### What is this repository for? ###

* A bundle of audio plugins from [Aida DSP](http://aidadsp.cc)
* Bundle version: 1.0
* This bundle is intended to be used with moddevices's products and derivatives

### Plugin list ###

* rt-neural-lv2

#### rt-neural-lv2 ####

It's a simple headless lv2 plugin inspired by

- [NeuralPi](https://github.com/GuitarML/NeuralPi)
- [RTNeural](https://github.com/jatinchowdhury18/RTNeural.git)

This lv2 plugin is a simple wrapper to inference classes used in NeuralPi project. All
the credits go to the original authors.

I've decided to implement this plugin to be able to compile original NeuralPi plugin without JUCE
and also to eliminate every additional effect that has been added during time.

__*WIP: currently this plugin is under work since CPU consumption is not acceptable, come back later!*__

##### Generate json models #####

This implies neural network training. Please follow __*Automated_GuitarAmpModelling.ipynb*__ script available on

- [my Automated-GuitarAmpModelling fork](https://github.com/MaxPayne86/Automated-GuitarAmpModelling/tree/aidadsp_devel)

##### Dataset #####

Since I was not satisfied with dataset proposed by orignal authors I've put together one:

- [Thomann Stompenberg Dataset](https://github.com/MaxPayne86/ThomannStompenbergDataset)

### Build ###

Below a guide on how to cross compile this bundle with [aidadsp sdk](https://drive.google.com/drive/folders/1-AAfAP-FAddCw0LJuvzsW8m_1lWHKXaV?usp=sharing).
You can extract cmake commands to fit your build system.

- RTNEURAL_XSIMD=ON or RTNEURAL_EIGEN=ON to select an available backend for RTNeural library
- RTNEURAL_LSTM_MODEL_HIDDEN_SIZE specifies the lstm models you want to load since model size need to be specified at compile time

for other options see [RTNeural](https://github.com/jatinchowdhury18/RTNeural.git) project.

```
1. install sdk with ./poky-glibc-x86_64-aidadsp-sdk-image-aarch64-nanopi-neo2-toolchain-2.1.15.sh
3. source environment-setup-aarch64-poky-linux
4. git clone https://github.com/AidaDSP/aidadsp-lv2.git && cd aidadsp-lv2
5. mkdir build && cd build
6. cmake -DCMAKE_BUILD_TYPE=Release -DRTNEURAL_XSIMD=ON -DRTNEURAL_LSTM_MODEL_HIDDEN_SIZE:STRING="16" -DCMAKE_VERBOSE_MAKEFILE:BOOL=ON ../
7. cmake --build .
8. make install DESTDIR="/tmp/"

bundle will be placed in /tmp/ ready to be copied on your device
```
