# Remotely-Operated-Vehicle-ROV-

## Introduction
A Remotely Operated Vehicle (ROV) is an unmanned, highly maneuverable underwater robot typically operated by a person aboard a vessel or onshore
providing a safe and efficient means to explore, inspect, and work in underwater environments. ROVs are equipped with cameras, lights, and various tools
allowing operators to perform a wide range of tasks such as underwater research, inspection of underwater structures
marine salvage operations, and maintenance of oil rigs and pipelines. 
These versatile machines play a crucial role in industries such as marine biology, oceanography, underwater archaeology, and offshore energy production
offering an effective solution to the challenges of underwater operations without risking human divers.


## Overview
A Remotely Operated Vehicle (ROV) is an unmanned, underwater robot controlled by operators from a remote location. 
ROVs are designed to explore, inspect, and perform tasks in underwater environments, providing a safe and efficient alternative to human divers.
Real-time Sensor Data: Accurate readings from DS18B20 temperature sensor and RCWL1655 ultrasonic sensor for immediate environmental monitoring underwater.
Joystick-Controlled Thrusters: Precise manoeuvrability facilitated by L293D H-bridge, enabling responsive control of thrusters via joystick inputs.
Wireless Communication: Seamless interaction through HC05 Bluetooth module, allowing real-time data transmission and intuitive control via mobile devices.
User Interface: Mobile device interface for intuitive monitoring of sensor data and control of the ROV, enhancing usability and operational efficiency.
Underwater Exploration: Designed for safe and efficient data collection and navigation in underwater environments, supporting various exploration and research applications.


## Problem Statement
Underwater information sensing and transmission is very essential but use of human beings to collect this information is highly dangerous and inaccurate.

## Components Required with Bill of Materials
Hardware: Arduino Uno R3, Ultrasonic Waterproof sensor, H-bridge [L293D] IC, Joysticks, Thrusters, Li-ion battery, Tether Cables

Software: Arduino IDE

Communication: Bluetooth module for data transmission.

Interface: Mobile screen.


Particulars	Estimated Cost in INR

 1	Underwater thruster motor (1pair)	3400
 
 2	Joysticks (1 pair)	40 
 
 3	Arduino board	425 
 
 4	Waterproof Ultrasonic sensor	250 
 
 5	Waterproof temperature sensor	70 
 
 6	Bluetooth module	300 
 
 7	Li-ion battery	250 
 
 8	Breadboard & Jumper wires	50 
 
 9	Tether cables	40 
 
 10	H-bridge IC 	6
 
 11	Container	150
 
Total Cost

INR 4,981


## Table for Pin Connections

COMPONENT	CONNECTION DETAILS

Pin 1	Arduino pin 11

Pin 2	Arduino pin 12

Pin 3	Right motor negative wire

Pin 6	Right motor positive wire

Pin 7	Arduino pin 9

Pin 8	7.4 V from the battery

Pin 9	Arduino pin 10

Pin 10	Arduino pin 8

Pin 11	Left motor positive wire

Pin 14	Left motor negative wire

Pin 15	Arduino pin 7

Pin 16	5 V from Arduino Joystick	

L/R+ of both Joysticks	5 V from Arduino

L/R [Left Joystick]	Arduino analog pin A0

L/R [Right Joystick]	Arduino analog pin A1

Battery	

Positive Wire	Arduino Vin pin

Negative Wire	Arduino GND pin


## Pinout Diagram
![image](https://github.com/Vigneshr2106/Remotely-Operated-Vehicle-ROV-/assets/165021886/56ead2ec-9ce6-46ae-9217-9760139daf04)

## Project Demo Image

![WhatsApp Image 2024-07-04 at 3 53 21 PM](https://github.com/Vigneshr2106/Remotely-Operated-Vehicle-ROV-/assets/165415082/d3006044-8208-4fc0-969d-a4a343b87be2)

