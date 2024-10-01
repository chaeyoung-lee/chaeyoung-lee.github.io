---
layout: post
title: "Connecting STM32U585 (B-U585I-IOT02A Board) with Peripherals"
date: 2024-09-30
---

The STM32U5 series microcontrollers, including the STM32U585AI, are relatively new compared to ST’s more established families like the STM32F4. As a result, there are fewer resources available online for development. Over the past year, I’ve been working extensively with the STM32U585AI due to its ultra-low-power consumption and sufficient processing power to handle machine learning algorithms (see my paper on HyperCam). To help bridge the gap in available resources, I’m launching a series of tutorials focused on the STM32U585AI microcontroller to encourage more projects using this platform.

In this post, I'll walk you through how to connect peripherals to the B-U585I-IOT02A Discovery Kit, which features the STM32U585AI. I’ll frequently reference the following documents throughout the post:
- [UM2839](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.st.com/resource/en/user_manual/um2839-discovery-kit-for-iot-node-with-stm32u5-series-stmicroelectronics.pdf): User manual of the discovery board
- [STM32U585xx](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.st.com/resource/en/datasheet/stm32u585ai.pdf): Datasheet of the microcontroller

This tutorial will provide step-by-step instructions on how to connect several peripherals, including:
- Adafruit VL53L1X Time-of-Flight Sensor
- MB1379 RGB Camera
- HM01B0 Grayscale Camera

Over time, I will expand this list. However, by the end of this guide, you’ll be familiar with connecting peripherals using common communication protocols like I2C and SPI, letting you connect additional sensors not covered here.

## Adafruit VL53L1X Time-of-Flight Sensor

- Peripherhal: Adafruit VL53L1X Time of Flight Distance Sensor ([Adafruit](https://www.adafruit.com/product/3967))
- Interface: I2C
- Power: 3-5V


### What are Time-of-Flight Sensors?
First, let’s take a look at what the Time-of-Flight (ToF) sensor does. A ToF sensor works by emitting a laser from a laser source, which reflects off an object and returns to the sensor. The sensor then measures the "time of flight," or how long it took the light to bounce back, which allows it to calculate the distance to the object. This sensor is commonly used in applications like gesture recognition, object detection, and robotic navigation. Unlike LiDAR, which typically relies on a rotating motor to scan across multiple directions, ToF sensors measure distance in a single direction, making them simpler and more energy-efficient.

### Pinout
On page 33 of the board's user manual (UM2839, link is above), Table 24 describes the pinout of the Arduino connector located at the back of the discovery board. The board's I2C pins are CN13-9 (I2C1_SDA) and CN13-10 (I2C1_SCL). Find the board's 3V3 output at CN17-4 and the ground at CN17-6. Here is the photo of the pinout.

![pinout](/assets/blog/1/pinout.jpeg)

### Code
Let's enable I2C1 on the microcontroller. The pin number of CN13-9 and CN13-10 is PB9 and PB8, respectively. On the STM32CubeIDE, enable I2C1 by setting it in I2C mode and change the GPIO pins accordingly.

![alt text](/assets/blog/1/i2c.png)
