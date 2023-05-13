
# Aries_2y_3dof_proj 


## Objective

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
