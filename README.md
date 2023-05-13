
# Aries_2y_3dof_proj 

# UNET_EDGE_DETECTOR
## Model
The objective of the model is to create an edge map of an input image. For which I have used a U-Net model because this work is very similar to semantic segmentation as we are classifing each pixel to a category edge(1) or non-edge(0).So it is intutive to get a concised feature reprsentation of the image and then reconstructing an edge map by upsampling these feature and for a better information flow we have residual conection between features during down sampling and up sampling. 

But since the dataset on which the training is to be done contained only 200 images so, training the unit from scratch was leading to overfitting so to overcome that, I have used the VGG19 pre-trained model on ImageNet as the encoder part of unet for feature extraction. The intuition behind it was simply that the pre-trained model must have learned to get low-level and high-level features for recognizing image structure and context, which is quite a similar operation that our model should also do to extract a good feature representation of the image and later that feature is used in upsampling and reconstructing the edge map image.

## Loss Function
The most crucial part of this model is the loss function as using BinaryCross Entropy loss fails here because the class is highly imbalanced, so the model learns to cheat and just perform well in classifying non-edge pixels correctly. And hence assign all the pixels as non-edge because it alone reduces the loss function drastically as these pixels have a high contribution to the loss. 

**Loss Function:**  **-**(Beta)*(y_true)*(log(y_pred))-(1-Beta)*(1-y_true)*(log(1-y_pred))

**Beta** = (Total Number of Edge Pixel)/(Total Number of Pixel in Image)

By dynamically weighting the loss for every image we bring the contribution of edge and non edge classification to the same order so model will learn to perform well on both classifications and will not give a biased output.

# Image to array conversion
The image which is to be drawn ,is first passed through edge detection machanism.After that an important task is to convert the image data to array format,which could br further used for determining the coordinates .
for this purpose first the image is convertrd to grayscale using opencv library.
after converting to grayscale the image is resized to 100 * 100 .then the pixel data is manipulated using tenserflow library
if the pixel value is greater than some threshold value then it becomes 1 or it becomes 0.
by this way the image is converted to a 2d array of size 100 * 100.
this array is stored as a (.txt) file . 
 
# Robotic Arm Implementation

This repository provides a solution for controlling a robotic arm using an Arduino board to draw sketches or figures. The simulation is implemented using Matlab/Simulink.
## Hardware Implementation

Arduino Communication:-
 The Arduino board establishes real-time communication with a computer to receive coordinates for the pen position and placement. As a result, there is no need for external memory such as an SD card. The robotic arm can operate continuously without requiring disconnection for different uses.

Python Script:-
 'CoordinateTransfer.py' is included in this repository, which reads a set of coordinates from a text file and normalizes them based on the page size and position. The script establishes a serial communication channel between the computer and the Arduino board using a baud rate of 9600. Additionally, the script performs a verification check to ensure successful transmission of coordinates. If necessary, it can resend the coordinates.
## Simulation on MATLAB/Simulink
The verification of the sketch can be performed using the Robotics and Simscape Toolbox in Matlab. However, for this project, the inverse kinematics were hard-coded because the block provided by the robotics toolbox did not meet our requirements and was computationally expensive.

To work with this repository, please follow these steps:

1. Import the 'rbTree' file into the Matlab workspace to import the rigidbody tree. Import the text file containing the coordinates as sets of column vectors.
2. Run the 'trajectorybuilder.m' script to normalize the data to coordinates. Open the Simulink file 'inv_kin.slx'. 
3. Input the time vector and coordinate vectors into the signal builder within Simulink to define the desired path along the coordinates. Ensure that you choose an integer 'k' to normalize the time vector (T/k) in order to complete the simulation within a finite time. 
4. You can also view the robotic simulation within the Matlab editor. 

Please note that for this particular example, the coordinate space is set to 100x100 in the text file, representing the resized image.
