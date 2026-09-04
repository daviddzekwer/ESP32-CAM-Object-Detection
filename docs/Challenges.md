# Challenges and Lessons Learned

Building this ESP32-CAM object detection system was not a straightforward process. Several hardware, software, and time-related challenges were encountered during development.

These challenges became an important part of the project because they provided practical experience in debugging, hardware integration, machine learning deployment, and working under project constraints.

---

## 1. ESP32-CAM Brownout Detector Error

One of the major challenges encountered during the project was the repeated:

```text
Brownout detector was triggered
```

error from the ESP32-CAM.

A brownout occurs when the ESP32 detects that its supply voltage has dropped below a safe operating level. The ESP32-CAM can experience relatively high current demand, particularly when the camera and Wi-Fi are active.

### What I experienced

The board would sometimes restart unexpectedly instead of running the application normally. This made it difficult to determine whether the problem was coming from the software, the camera, or the power supply.

### Troubleshooting

I investigated several possible causes, including:

* Power supply stability
* USB programmer and connections
* ESP32-CAM power requirements
* Camera operation
* Wiring and physical connections
* Possible hardware-related issues

This process taught me that debugging an embedded system requires looking beyond the code. A program can be correctly written and still fail because of an electrical or power-related problem.

### Lesson Learned

**Power is part of the system.**

When working with microcontrollers and other embedded hardware, software debugging should not be separated from electrical troubleshooting.

---

## 2. Setting Up the 16×2 LCD

Another challenge was integrating the 16×2 LCD into the project.

The LCD was connected through an I2C backpack, which made it possible to communicate with the display using fewer GPIO pins.

However, getting the LCD working initially required troubleshooting both the hardware and software configuration.

### Problems Encountered

The initial setup involved checking:

* SDA and SCL connections
* LCD power connections
* I2C communication
* The LCD I2C address
* Library compatibility
* Physical connection between the I2C backpack and LCD

The LCD's I2C address was eventually identified as:

```text
0x27
```

### Approach Used

Rather than immediately adding the LCD to the relatively complex Edge Impulse application, I created a separate LCD testing program.

This allowed the LCD to be tested independently before it became part of the final system.

### Lesson Learned

**Test components individually before integrating them into a larger system.**

Breaking a complex problem into smaller, testable sections made troubleshooting much easier.

---

## 3. Integrating Machine Learning With Embedded Hardware

Deploying the Edge Impulse model to the ESP32-CAM introduced another layer of complexity.

The project was no longer simply a microcontroller application. It required the integration of:

* Camera capture
* Image processing
* Machine learning inference
* Object detection
* LCD communication
* Buzzer control

Each component had to work correctly while also operating within the limitations of the ESP32-CAM.

The Edge Impulse model therefore had to be deployed in a way that allowed inference to take place on the embedded device.

### Lesson Learned

Machine learning on embedded systems is different from simply training a model on a computer. The model must also be suitable for the available computational and memory resources of the target hardware.

---

## 4. Dataset Collection and Labelling

The quality of an object detection model depends heavily on the data used to train it.

Images had to be collected for four classes:

* Multimeter
* Tester
* Breadboard
* Screwdriver

The images then had to be labelled using bounding boxes so that the model could learn both **what the objects looked like and where they were located in the image**.

This process required time and attention because poorly labelled or insufficiently varied images could negatively affect the model's ability to generalize.

### Lesson Learned

**Good machine learning starts with good data.**

Collecting and labelling data is not just preparation for model training; it is an important part of building a reliable object detection system.

---

## 5. Working Under Extreme Time Pressure

Perhaps the biggest non-technical challenge was the project deadline.

The final stages of the project had to be completed under significant time pressure.

On the night before submission and presentation, I left campus at approximately **8:30 PM**, had something to eat, and returned to continue working on the project.

I eventually went to sleep at approximately **3:00 AM** and woke up around **5:00 AM** to prepare for school.

The class was scheduled to begin at **8:00 AM**, but the project was still being assembled that morning.

To manage the remaining work, I assigned the final assembly to some of my colleagues while I focused on preparing and editing the presentation slides.

We were still finishing parts of the project when we had to rush to the lecture hall for the presentation.

Fortunately, the prototype was functioning properly during the presentation.

### The Documentation Problem

There was, however, one unfortunate consequence.

Because of the pressure and constant switching between assembly, debugging, and presentation preparation, I completely forgot to record a video of the final working prototype.

Therefore, the repository does not contain a live demonstration showing the ESP32-CAM detecting one of the four objects and displaying the result on the LCD.

Instead, I documented the development process using the footage and images I had captured during the earlier stages, together with the 3D design of the final prototype.

### Lesson Learned

**Document the project while building it, not after finishing it.**

Even when the project itself is successful, important evidence of the development process can easily be lost when working under pressure.

---

# Overall Lessons From the Project

This project taught me several lessons that go beyond the technical implementation.

### 1. Debug systematically

When something fails, changing everything at once can make the problem harder to identify. Testing individual components helped isolate problems more effectively.

### 2. Hardware and software must be considered together

The brownout problem demonstrated that software behaviour can be affected by electrical conditions such as unstable power.

### 3. Build incrementally

Testing the camera, dataset collection, LCD, machine learning model, and final integration as separate stages made the overall project more manageable.

### 4. Start early

Leaving major integration and documentation tasks until the final day created unnecessary pressure and reduced the amount of time available for testing and documentation.

### 5. Document continuously

Photos, videos, screenshots, code versions, test results, and failures are all valuable parts of an engineering project.

---

# Final Reflection

Although the project presented several challenges, each problem became an opportunity to learn.

The most valuable part of the project was not simply getting an object detection model to run on an ESP32-CAM. It was learning how to move from an idea to a working embedded AI system while dealing with real-world problems involving **power, hardware interfaces, software, machine learning, debugging, teamwork, and time constraints**.

The missing final demonstration is unfortunate, but it also reflects an important lesson from the project:

> **A successful engineering project should be built, tested, and documented.**

This experience has made me more conscious of documenting future projects from the very beginning.
