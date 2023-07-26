# SuperpositionAI


## Introduction

This repository contains  explanation of SuperpositionAI and sample data and result data.
I am sorry that source code of SuperpositionAI is not to release.
## About SuperpositionAI
SuperpositionAI (hereinafter referred to as SPAI) is image analizing software.  
Please note that SPAI is experimental.
SPAI can works on Windows 10/11 of 64bit,

SPAI execute class separation  based thinking on quantum superposition.  
According to Born rule,The existence probability of a quantum is proportional to the absolute value of the square of the wave function (ket vector).  
Considering the probability as the expected value, among the classes of trained data,
Shows the class with the highest expected value.  
Deep learning and convolutional neural networks (CNN), which have become mainstream recently,It works lightly compared to artificial intelligence.
High-performance CPU (Central Processing Unit) necessary for CNN, similarly high-performance GPU (computing unit specialized for image processing)
Works at realistic speeds without assistance.
However, since the current version is in an experimental stage,
Please understand that there are many cases where the expected results are not obtained.

## Dependencies of execute

It is OK that PC is able to work on Windows10 or 11 and 64bit.  
It is needless another hardware or software.

## Installation

First, download from Vector site.  
URL is blow.

(後で変更する)  
https://www.vector.co.jp/soft/winnt/business/se464889.html  

Downloaded SuperpositionAI_010.zip is to unzip.

Execute SuperpositionAI_010_setup.exe that is installer.

After that, follow the instructions of the installer to install.


## Use for now

Here, I will introduce the procedure for those who think that they will move it for the time being.
 
① Click the Sample Movies button.
  
② A list of sample videos will be displayed in Explorer.
  Select 2_FA-18_take_off.wmv and double-click it.
I think that "Movies & TV" and "Windows Media Player" will be launched.
If the video playback application cannot be started, please check the environment settings of your PC.
If the video playback application starts, I think that the video has started playing.
Pause and wait.
  
③ Selection of trained data
  Click the Learn Setting button on the main screen of SuperpositionAI.
On the Learn Setting screen that appears, from the Using learned dataset combo box,
Select fighters and click the Save button.
Then click the Close button to close the Learn Setting screen.
④ Arranging windows
  Place the SuperpositionAI window on the left side of the desktop and the video player window on the right side of the desktop.
At this time, be careful not to overlap both windows,
Adjust the window size of SuperpositionAI so that the aspect ratio is roughly the same.
  
⑤ Start execution of image analysis
  Click the Execute button on the main screen of SuperpositionAI.
Since the entire desktop is covered with a light blue semi-transparency,
Select the image range for your video.
Once the selection is complete, image analysis will begin.
  
  
⑥ Completion of image analysis
  Click the Stop button on the main screen of SuperpositionAI.
After a while, when the Stop process is completed,
Click the Quit button to exit SuperpositionAI.

## Quantum Superposition and Expectation Evaluation
Superposition of states
In quantum mechanics, quanta can have multiple possible states.
For the bracket notation mentioned above, the upward spin of the quantum and
The formula when the downward spin of the quantum has a possibility of 50% is as follows.

|ψ⟩ = 1/√2(|↑⟩) + 1/√2(|↓⟩)

In general, the quantum has multiple states (|ψ1⟩,|ψ2⟩,...,|ψN⟩)
, the coefficients (c1,c2,...,cN) are
It will be a linear combination that takes into account. i.e.

|ψ⟩= c1(|ψ1⟩) + c2(|ψ2⟩)+...+cN(|ψN⟩)

becomes.
SuperpositionAI binarizes the image of the target part,
Let |↑⟩ be the white part, |↓⟩ be the black part, and cw and cb be the respective coefficients.

|ψ⟩= cw(|ψ↑⟩) + cb(|ψ↓⟩)

I'm doing it.
 
Born rules and probabilities
The Born rule was presented in Born's paper in 1926.
In this rule, we obtain from the Schrödinger equation for some quantum
An interpretation was given that the square of the absolute value of the wave function indicates the existence probability (density) of the quantum.
In addition, the absolute value of the square of the state vector was also shown as the existence probability (density) of the quantum.
Wavefunctions or state vectors are generally complex numbers. i.e.

〈ψ|= (a,bi) (i is the imaginary unit)

becomes. To get the square of the absolute value for this,
Multiply by the complex conjugate of (a,bi).
If the complex conjugate of 〈ψ| is |*ψ⟩, then the square of the absolute value is

|ψ|2 = 〈ψ|*ψ⟩

becomes.
In SuperpositionAI, the complex conjugate of |ψ⟩ mentioned above is multiplied to obtain the square of the absolute value.

 
Class determination by evaluation of target images
SuperpositionAI uses multiple binary learning images for each class,
Create a state vector for each class.
This is called building trained data.
Also, the state vector to be evaluated is created from the binary image to be evaluated.
ψn is the state vector for each class
Let φ be the state vector to be evaluated.
Since φ is the state vector of a binary image, it has only two states. i.e.

φ=(1,0i) real part only
φ=(0,1i) imaginary part only
By taking the inner product of φ and ψ, we can find out what φ has in ψ.
Only the real part and only the imaginary part can be represented.
That makes the evaluation of φ against ψ. In other words, if the inner product is In,

In = 〈φ|ψn⟩

When Pn is the score that indicates the degree of similarity for each target class,
If the formula for calculating Pn is the square of the absolute value of I, then

Pn = |In|2

Pn is normalized so that it falls within the range of 0 to 1.
Pn is proportional to the probability that φ is ψn.
Apply this operation to all classes in the trained data.
At this time, the class with the largest P is the class to be evaluated.
However, if the maximum P is less than the user-configured threshold,
Treat as Unknown class.

## Weak points of current SuperpositionAI

In the top-level directory are executable scripts to execute, evaluate, and
visualize the tracker. The main entry point is in `deep_sort_app.py`.
This file runs the tracker on a MOTChallenge sequence.

In package `deep_sort` is the main tracking code:

* `detection.py`: Detection base class.
* `kalman_filter.py`: A Kalman filter implementation and concrete
   parametrization for image space filtering.
* `linear_assignment.py`: This module contains code for min cost matching and
   the matching cascade.
* `iou_matching.py`: This module contains the IOU matching metric.
* `nn_matching.py`: A module for a nearest neighbor matching metric.
* `track.py`: The track class contains single-target track data such as Kalman
  state, number of hits, misses, hit streak, associated feature vectors, etc.
* `tracker.py`: This is the multi-target tracker class.

The `deep_sort_app.py` expects detections in a custom format, stored in .npy
files. These can be computed from MOTChallenge detections using
`generate_detections.py`. We also provide
[pre-generated detections](https://drive.google.com/open?id=1VVqtL0klSUvLnmBKS89il1EKC3IxUBVK).

## Good points of current SuperpositionAI

If you find this repo useful in your research, please consider citing the following papers:

    @inproceedings{Wojke2017simple,
      title={Simple Online and Realtime Tracking with a Deep Association Metric},
      author={Wojke, Nicolai and Bewley, Alex and Paulus, Dietrich},
      booktitle={2017 IEEE International Conference on Image Processing (ICIP)},
      year={2017},
      pages={3645--3649},
      organization={IEEE},
      doi={10.1109/ICIP.2017.8296962}
    }

    @inproceedings{Wojke2018deep,
      title={Deep Cosine Metric Learning for Person Re-identification},
      author={Wojke, Nicolai and Bewley, Alex},
      booktitle={2018 IEEE Winter Conference on Applications of Computer Vision (WACV)},
      year={2018},
      pages={748--756},
      organization={IEEE},
      doi={10.1109/WACV.2018.00087}
    }