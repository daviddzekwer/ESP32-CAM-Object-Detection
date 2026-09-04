# Final Object Detection Prototype

This stage combines the machine learning model with the hardware output components to form the final prototype.

The system integrates:

**ESP32-CAM + Edge Impulse Model + 16×2 LCD + Buzzer**

When an object is detected, the system processes the camera image using the trained machine learning model. The detected object is then displayed on the LCD, while the buzzer provides an audible indication.

### Target Objects

* Multimeter
* Tester
* Breadboard
* Screwdriver

### System Flow

**Camera Capture → Object Detection → Classification → LCD Display + Buzzer**

### Objectives

* Integrate the Edge Impulse model with the LCD.
* Add an audible buzzer indication.
* Display the detected object's name.
* Combine the individual components into a functional prototype.

### Outcome

The complete prototype was assembled and successfully demonstrated during the project presentation.

Although a video of the final live demonstration was unfortunately not recorded due to the tight project deadline, the development process and final prototype design have been documented in the main repository README.
