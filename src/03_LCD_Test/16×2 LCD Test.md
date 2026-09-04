# 16×2 LCD Test

This stage focused on testing the **16×2 LCD with an I2C backpack** before integrating it with the object detection system.

The LCD was tested independently to verify the I2C communication, wiring, and display functionality.

The I2C address of the LCD was identified as:

`0x27`

### Objectives

* Verify communication between the ESP32 and LCD.
* Confirm the correct I2C address.
* Test text display.
* Resolve hardware connection issues before final integration.

### Outcome

The LCD was successfully tested and confirmed to be working. The tested configuration was then used when integrating the display into the final object detection application.

### Lesson Learned

Testing individual hardware components before combining them into a larger system made troubleshooting significantly easier.
