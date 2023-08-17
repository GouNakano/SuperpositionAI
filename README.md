# SuperpositionAI

![spai](https://github.com/GouNakano/SuperpositionAI/assets/56259253/a2d51ad0-6763-4ba9-b993-4fdc6468e090)

## Introduction

This repository contains  explanation of SuperpositionAI and sample data and result data.
I am sorry that source code of SuperpositionAI is not to release.

## About SuperpositionAI

SuperpositionAI (hereinafter referred to as SPAI) is image analizing software.  
Please note that SPAI is experimental.
SPAI can works on Windows 10/11 of 64bit,

SPAI execute class separation  based thinking on quantum superposition.  
According to Born rule,The existence probability of a quantum is proportional to the absolute value of the square of the wave function (or ket state vector).  
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

1. download from Vector site.  
URL is blow.  
<https://www.vector.co.jp/soft/winnt/art/se525686.html>  

2. Downloaded SuperpositionAI_010.zip is to unzip.

3. Execute SuperpositionAI_010_setup.exe that is installer.  
After that, follow the instructions of the installer to install.

## Use for now

Here, I will introduce the procedure for those who think that they will move it for the time being.

1. Click the "Sample Movies" button.  
  ![img030](https://github.com/GouNakano/SuperpositionAI/assets/56259253/d927ba43-0b1f-4be6-998c-a2aadec68cfa)  
  
2. A list of sample videos will be displayed in Explorer.  
  Select "2_FA-18_take_off.wmv" and double-click it.
I think that "Movies & TV" and "Windows Media Player" will be launched.
If the video playback application cannot be started, please check the environment settings of your PC.
If the video playback application starts, I think that the video has started playing.
Pause and wait.  
![img031](https://github.com/GouNakano/SuperpositionAI/assets/56259253/e97dcdc5-a8da-41a0-bc8f-bf3f7786cdb0)

3. Selection of trained data  
  Click the Learn Setting button on the main screen of SuperpositionAI.
On the Learn Setting screen that appears, from the Using learned dataset combo box,
Select fighters and click the Save button.
Then click the Close button to close the Learn Setting screen.
4. Arranging windows  
  Place the SuperpositionAI window on the left side of the desktop and the video player window on the right side of the desktop.
At this time, be careful not to overlap both windows,
Adjust the window size of SuperpositionAI so that the aspect ratio is roughly the same.  
![img034](https://github.com/GouNakano/SuperpositionAI/assets/56259253/9970058e-55de-49cf-8d6f-9e14867c81fd)

5. Start execution of image analysis  
  Click the Execute button on the main screen of SuperpositionAI.
Since the entire desktop is covered with a light blue semi-transparency,
Select the image range for your video.
Once the selection is complete, image analysis will begin.  
![img033](https://github.com/GouNakano/SuperpositionAI/assets/56259253/e47c7a07-a240-4a4b-bda6-628901b407f0)  
![img032](https://github.com/GouNakano/SuperpositionAI/assets/56259253/a2a89c7a-d40e-4f07-b8fa-809edc070ad1)  

6. Completion of image analysis  
  Click the Stop button on the main screen of SuperpositionAI.
After a while, when the Stop process is completed,
Click the Quit button to exit SuperpositionAI.

## Quantum superposition and Evaluation of expected value

### Superposition of states

In quantum mechanics, quanta can have multiple possible states.
For the bracket notation mentioned above, the upward spin of the quantum and
The formula when the downward spin of the quantum has a possibility of 50% is as follows.  

$\ |ψ⟩ = 1/\sqrt2(|↑⟩ + |↓⟩) $  

In general, the quantum has multiple states  
$\ (|ψ_1⟩,|ψ_2⟩,...,|ψ_N⟩) $
, the coefficients  
$\ (c_1,c_2,...,c_N) $  
are It will be a linear combination that takes into account. i.e.

$\ |ψ⟩= c_1(|ψ_1⟩) + c_2(|ψ_2⟩)+...+c_N(|ψ_N⟩) $

becomes.
SuperpositionAI binarizes the image of the target part,
Let  
$\ |ψ_↑⟩$
be the white part,  
$\ |ψ_↓⟩ $
be the black part, and cw and cb be the respective coefficients.

$\ |ψ⟩ = c_w(|ψ_↑⟩) + c_b(|ψ_↓⟩) $

I'm doing it.
  
### Born rules and probabilities

The Born rule was presented in Born's paper in 1926.
In this rule, we obtain from the Schrödinger equation for some quantum
An interpretation was given that the square of the absolute value of the wave function indicates the existence probability density of the quantum.
In addition, the absolute value of the square of the state vector was also shown as the existence probability density of the quantum.
Wave functions or state vectors are generally complex numbers. i.e.

$\ 〈ψ|= (a,bi) \quad $
(
$\ i $
is the imaginary unit)

becomes. To get the square of the absolute value for this,
Multiply by the complex conjugate of (a,bi).
If the complex conjugate of 〈ψ| is |*ψ⟩, then the square of the absolute value is

$\ |ψ|^2 = 〈ψ|^*ψ⟩ $

becomes.
In SuperpositionAI, the complex conjugate of
$\ |ψ⟩ $
mentioned above is multiplied to obtain the square of the absolute value.

### Class determination by evaluation of target images

SuperpositionAI uses multiple binary learning images for each class,
Create a state vector for each class.
This is called building trained data.
Also, the state vector to be evaluated is created from the binary image to be evaluated.
$\ ψ_n $
is the state vector for each class
Let  
$\ φ $  
be the state vector to be evaluated.
Since  
$\ φ $
is the state vector of a binary image, it has only two states. i.e.

$\ φ=(1,0i) \quad $  
real part only  
$\ φ=(0,1i) \quad $  
imaginary part only  

By taking the inner product of  
$\ φ $
and  
$\ ψ $
, we can find out what  
$\ φ $
has in  
$\ ψ $
.
Only the real part and only the imaginary part can be represented.
That makes the evaluation of  
$\ φ $
against
$\ ψ $
. In other words, if the inner product is
$\ I_n $
,  

$\ In = 〈φ|ψ_n⟩ $

When  
$\ Pn$
is the score that indicates the degree of similarity for each target class,
If the formula for calculating  
$\ P_n$
is the square of the absolute value of I, then

$\ P_n = |I_n| ^2 $

$\ P_n$  
is normalized so that it falls within the range of 0 to 1.
$\ P_n $
is proportional to the probability that  
$\ φ$
is  
$\ ψ_n$
.
Apply this operation to all classes in the trained data.
At this time, the class with the largest  
$\ P $
is the class to be evaluated.
However, if the maximum  
$\ P $
is less than the user-configured threshold,
Treat as Unknown class.
