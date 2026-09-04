# ESP32-CAM AI Object Detection System

An embedded AI object detection system built using an **ESP32-CAM** and a machine learning model trained and deployed using **Edge Impulse**.

The system was designed to identify four electronic/electrical tools:

* Multimeter
* Tester
* Breadboard
* Screwdriver

When an object is detected, the system displays the predicted object on a **16×2 LCD** and provides an audible indication using a **buzzer**.

---

## 🎥 Project Overview

[Watch the Project Video](https://youtube.com/shorts/WESwBV3ae2Q?si=yFEyD7pZwp0nkdHy)

> **Note:** The video above documents the development process, challenges, and learning experience behind the project.

Unfortunately, I did not record a live video of the final working prototype.

The reason was the intense time pressure during the final stage of the project. On the night before submission and presentation, I left campus at approximately 8:30 PM, returned to continue working on the project, and eventually slept around 3:00 AM. I woke up at approximately 5:00 AM to prepare for school.

The following morning, while some of my colleagues completed the final assembly, I was simultaneously preparing the presentation slides. We eventually had to rush to the lecture hall for the presentation.

Fortunately, the prototype was working properly during the presentation. However, in the rush, I completely forgot to record a final demonstration.

Rather than leave this part undocumented, I decided to document the actual development process, including the setup, dataset collection, model training, deployment, hardware integration, challenges, and lessons learned.

---

# Project Objective

The objective of this project was to explore how a machine learning model can be integrated into an embedded system to perform **real-time object detection**.

The project combines:

**Computer Vision + Machine Learning + Embedded Systems + Hardware Interfacing**

The ESP32-CAM captures images, the trained Edge Impulse model processes the image, and the detected object is communicated to the user through an LCD and buzzer.

---

# How the System Works

The overall process can be summarized as:

**Camera → Image → Machine Learning Model → Object Detection → LCD + Buzzer**

1. The ESP32-CAM captures an image.
2. The trained machine learning model analyzes the image.
3. The model identifies the object and produces a confidence score.
4. The detected object is displayed on the 16×2 LCD.
5. The buzzer provides an audible indication of detection.

---

# Machine Learning Workflow

The machine learning part of the project was developed using **Edge Impulse**.

### 1. Dataset Collection

Images were collected for four object classes:

* Multimeter
* Tester
* Breadboard
* Screwdriver

Different images were captured to provide the model with examples of the objects from different positions and orientations.

### 2. Data Labelling

The collected images were uploaded to Edge Impulse and the objects were manually labelled using bounding boxes.

This step is important because the model needs to learn **which part of an image contains the object**.

### 3. Model Training

The labelled dataset was then used to train an object detection model.

The final model achieved approximately:

* **Precision:** 1.00
* **Recall:** 0.95
* **F1 Score:** 97.4%

These results showed that the trained model was able to detect the selected objects with reasonably good performance.

### 4. Model Deployment

After training, the model was deployed as an Arduino-compatible library and integrated into the ESP32-CAM application.

This allowed the machine learning model to run on the embedded device rather than requiring the image to be sent to a remote server.

---

# Hardware Used

* ESP32-CAM
* ESP32-CAM programmer
* 16×2 LCD
* I2C LCD backpack
* Buzzer
* Connecting wires
* Prototype stand
* Multimeter
* Tester
* Breadboard
* Screwdriver

---

# Software and Tools

* Arduino IDE
* Edge Impulse
* Arduino C/C++
* Serial Monitor

---

# Development Stages

The project was developed progressively rather than building everything at once.

### Stage 1 — ESP32-CAM Setup

The first step was getting the ESP32-CAM programmed and communicating properly with the computer.

A simple camera streaming program was used to verify that the camera could capture and stream images.

**Code:**
`src/01_camera_streaming/`

### Stage 2 — Dataset Collection

Once the camera was working, it was used to capture images of the objects that the model would eventually recognize.

**Code:**
`src/02_object_capture/`

### Stage 3 — LCD Testing

Before integrating the LCD into the machine learning application, the LCD was tested independently.

This helped verify:

* I2C communication
* LCD address
* SDA/SCL connections
* Text display

**Code:**
`src/03_lcd_test/`

### Stage 4 — Edge Impulse Model Deployment

The trained object detection model was deployed to the ESP32-CAM and tested independently.

**Code:**
`src/04_edge_impulse_deployment/`

### Stage 5 — Final Integration

The final stage involved combining:

**ESP32-CAM + Edge Impulse Model + LCD + Buzzer**

The detected object's name was sent to the LCD, while the buzzer provided an audible indication.

**Code:**
`src/05_final_prototype/`

---

# Major Challenges

## 1. ESP32 Brownout Detector Error

One of the major problems encountered during development was the:

`Brownout detector was triggered`

error.

This occurs when the ESP32 detects that its supply voltage has dropped below a safe operating level.

The problem was particularly noticeable when using the ESP32-CAM because the camera and Wi-Fi can produce significant current demand.

This taught me an important lesson about embedded systems:

> A program can be correct and the hardware can still fail because of power-related problems.

Debugging this required checking the power supply, connections, programmer, and ESP32-CAM hardware.

---

## 2. Setting Up the 16×2 LCD

Integrating the LCD was another challenge.

Initially, I had difficulty getting the LCD to communicate correctly with the ESP32-CAM.

The LCD used an I2C backpack, which reduced the number of GPIO pins required. However, I still had to determine the correct I2C address and ensure that the connections were correct.

I eventually confirmed the LCD address as:

`0x27`

I also learned that the physical connections between the I2C backpack and LCD matter. The backpack needs to be properly connected to the LCD pins for the display to function correctly.

A separate LCD testing program was therefore created before integrating it into the final object detection code.

**LCD test code:**
`src/03_lcd_test/`

---

# What I Learned

This project taught me much more than simply how to deploy a machine learning model.

### Technical Lessons

* How to configure and program an ESP32-CAM
* How to collect an object detection dataset
* How to label images using Edge Impulse
* How object detection models are trained
* How to evaluate model performance using precision, recall and F1 score
* How to deploy a trained machine learning model to an embedded device
* How to interface an I2C LCD with a microcontroller
* How to control a buzzer from a microcontroller
* How to troubleshoot power-related ESP32 problems

### Engineering Lessons

The biggest lesson was that **engineering projects rarely go exactly as planned**.

Debugging, hardware failures, software errors, limited time and unexpected problems are all part of the process.

I also learned the importance of documenting the project **while building it**, rather than trying to remember everything after the project is finished.

Ironically, while trying to finish the project under a very tight deadline, I forgot to record the final demonstration.

That mistake is now part of the documentation of the project itself.

---

# Future Improvements

If I were to continue developing the project, I would consider:

* Improving the size and diversity of the training dataset
* Increasing detection accuracy
* Testing the model under different lighting conditions
* Improving the prototype enclosure
* Adding more recognizable objects
* Displaying confidence scores on the LCD
* Adding different buzzer patterns for different objects
* Improving power management
* Recording a proper demonstration of the completed system

---

# Project Status

**Completed and presented successfully.**

Although the final live demonstration was not recorded, the prototype was assembled and functioning during the project presentation.

This repository contains the development process, source code, machine learning workflow, hardware integration, challenges, and lessons learned from the project.
