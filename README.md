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

```
## Use for now

Beside the main tracking application, this repository contains a script to
generate features for person re-identification, suitable to compare the visual
appearance of pedestrian bounding boxes using cosine similarity.
The following example generates these features from standard MOT challenge
detections. Again, we assume resources have been extracted to the repository
root directory and MOT16 data is in `./MOT16`:
```
python tools/generate_detections.py \
    --model=resources/networks/mars-small128.pb \
    --mot_dir=./MOT16/train \
    --output_dir=./resources/detections/MOT16_train
```
The model has been generated with TensorFlow 1.5. If you run into
incompatibility, re-export the frozen inference graph to obtain a new
`mars-small128.pb` that is compatible with your version:
```
python tools/freeze_model.py
```
The ``generate_detections.py`` stores for each sequence of the MOT16 dataset
a separate binary file in NumPy native format. Each file contains an array of
shape `Nx138`, where N is the number of detections in the corresponding MOT
sequence. The first 10 columns of this array contain the raw MOT detection
copied over from the input file. The remaining 128 columns store the appearance
descriptor. The files generated by this command can be used as input for the
`deep_sort_app.py`.

**NOTE**: If ``python tools/generate_detections.py`` raises a TensorFlow error,
try passing an absolute path to the ``--model`` argument. This might help in
some cases.

## Training the model

To train the deep association metric model we used a novel [cosine metric learning](https://github.com/nwojke/cosine_metric_learning) approach which is provided as a separate repository.

## Highlevel overview of source files

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

## Citing DeepSORT

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