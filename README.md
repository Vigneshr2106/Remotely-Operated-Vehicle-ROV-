# Remotely-Operated-Vehicle-ROV-

## Introduction
A Remotely Operated Vehicle (ROV) is an unmanned, highly maneuverable robot typically operated by a person aboard a vessel or onshore
providing a safe and efficient means to explore, inspect water bodies. ROVs are equipped with cameras, lights, and various tools
allowing operators to perform a wide range of tasks such as underwater research, inspection of underwater structures
marine salvage operations, and maintenance of oil rigs and pipelines. 
These versatile machines play a crucial role in industries such as marine biology, oceanography, underwater archaeology, and offshore energy production
offering an effective solution to the challenges of exploring water bodies without risking human divers.


## Overview
A Remotely Operated Vehicle (ROV) is an unmanned robot controlled by operators from a remote location. 
ROVs are designed to explore, inspect, and perform tasks in water environments, providing a safe and efficient alternative to human divers.
Real-time Sensor Data: Accurate readings from DS18B20 temperature sensor and RCWL1655 ultrasonic sensor for immediate environmental monitoring water bodies.
Joystick-Controlled Thrusters: Precise manoeuvrability facilitated by L293D H-bridge, enabling responsive control of thrusters via joystick inputs.
Wireless Communication: Seamless interaction through HC05 Bluetooth module, allowing real-time data transmission and intuitive control via mobile devices.
User Interface: Mobile device interface for intuitive monitoring of sensor data and control of the ROV, enhancing usability and operational efficiency.


## Problem Statement
Water bodies such as oceans, seas, rivers, and lakes hold immense ecological, scientific, and economic importance. However, their vastness and depth present significant challenges for exploration and monitoring. Remotely Operated Vehicles (ROVs) offer a promising solution for water bodies exploration, allowing researchers and professionals to gather data and monitor marine environments without direct human intervention.


## Components Required with Bill of Materials
Hardware: Arduino Uno R3, Ultrasonic Waterproof sensor, H-bridge [L293D] IC, Joysticks, Thrusters, Li-ion battery, Tether Cables

Software: Arduino IDE

Communication: Bluetooth module for data transmission.

Interface: Mobile screen.


Particulars	Estimated Cost in INR

 1	thruster motor (1pair)	3400
 
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

## Working Code

#include <SoftwareSerial.h>

// Pins for the joysticks

const int joyLpin = A0; // left joystick

const int joyRpin = A1; // right joystick

// Pins for the motors

const int motorLfwd = 7;  // left motor forward pin

const int motorLbck = 8;  // left motor backward pin

const int motorLen = 10;  // left motor enable pin

const int motorRfwd = 9;  // right motor forward pin

const int motorRbck = 12; // right motor backward pin

const int motorRen = 11;  // right motor enable pin

// Pins for the HC-05 module

const int bluetoothTx = 10; // TX on Arduino

const int bluetoothRx = 11; // RX on Arduino

// Pins for the HC-SR04 sensor

const int trigPin = 9;

const int echoPin = 8;

// Create a software serial port

SoftwareSerial bluetooth(bluetoothTx, bluetoothRx);

// Variables for joystick readings

int joyL; // left joystick reading (0-1023 from ADC)

int joyR; // right joystick reading (0-1023 from ADC)

int joyLneutral; // left joystick neutral position

int joyRneutral; // right joystick neutral position

const int deadzone = 20; // joystick "dead zone" to prevent drift

int motorLspeed; // left motor speed (0-255 for PWM)

int motorRspeed; // right motor speed (0-255 for PWM)

// Ultrasonic sensor variables

long duration;

float distanceCm;

void setup() {

  // Set motor control pins as outputs
  
  pinMode(motorLfwd, OUTPUT);
  
  pinMode(motorRfwd, OUTPUT);
  
  pinMode(motorLbck, OUTPUT);
  
  pinMode(motorRbck, OUTPUT);
  
  pinMode(motorLen, OUTPUT);
  
  pinMode(motorRen, OUTPUT);
  
  // Initialize the HC-SR04 sensor pins
  
  pinMode(trigPin, OUTPUT);
  
  pinMode(echoPin, INPUT);
  
  // Start serial communication with the PC
  
  Serial.begin(9600);
  
  Serial.println("Joystick and Ultrasonic Sensor with Bluetooth HC-05");
  
  // Start serial communication with the HC-05
  
  bluetooth.begin(9600);
  
  // Calibrate joysticks
  
  joyLneutral = analogRead(joyLpin);
  
  joyRneutral = analogRead(joyRpin);
  
}

void loop() {

  // Read joysticks
  
  joyL = analogRead(joyLpin);
  
  joyR = analogRead(joyRpin);
  
  // Read ultrasonic sensor
  
  digitalWrite(trigPin, LOW);
  
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  
  delayMicroseconds(10);
  
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  
  distanceCm = duration * 0.034 / 2;
  
  // Send distance to the serial monitor and Bluetooth
  
  bluetooth.print("Distance: ");
  
  bluetooth.print(distanceCm);
  
  bluetooth.println(" cm");
  
  // Check if an object is detected within 19 cm
  
  if (distanceCm <= 19) {
  
   // Stop both motors
     
   digitalWrite(motorLfwd, LOW);
    
   digitalWrite(motorLbck, LOW);
    
   digitalWrite(motorRfwd, LOW);
    
   digitalWrite(motorRbck, LOW);
    
   analogWrite(motorLen, 0);
    
   analogWrite(motorRen, 0);
    
   Serial.println("Object detected! Stopping motors.");
    
  }
  
  else 
  
  {
  
  // Control left motor based on left joystick
    
   if ((joyL - joyLneutral) < -deadzone) 
   
   {
   
   // Joystick pushed forward
     
   digitalWrite(motorLfwd, HIGH);
     
   digitalWrite(motorLbck, LOW);
     
     
   motorLspeed = map(joyL, joyLneutral, 0, 0, 255);
     
  } 
    
   else if ((joyL - joyLneutral) > deadzone)
   
   {
     
   // Joystick pulled backward
     
   digitalWrite(motorLfwd, LOW);
      
   digitalWrite(motorLbck, HIGH);
      
   motorLspeed = map(joyL, joyLneutral, 1023, 0, 255);
   
   } 
   
   else 
   
   {
     
   // Joystick in neutral position
   
   digitalWrite(motorLfwd, LOW);
   
   digitalWrite(motorLbck, LOW);
   
   motorLspeed = 0;
   
  }
  
 // Control right motor based on right joystick
 
 if ((joyR - joyRneutral) < -deadzone) 

 {
 
 // Joystick pushed forward
 
 digitalWrite(motorRfwd, HIGH);
 
 digitalWrite(motorRbck, LOW);
 
 motorRspeed = map(joyR, joyRneutral, 0, 0, 255);
 
}

else if ((joyR - joyRneutral) > deadzone) 

{

// Joystick pulled backward

digitalWrite(motorRfwd, LOW);

digitalWrite(motorRbck, HIGH);

motorRspeed = map(joyR, joyRneutral, 1023, 0, 255);

} 

else 

{

// Joystick in neutral position

digitalWrite(motorRfwd, LOW);

digitalWrite(motorRbck, LOW);

motorRspeed = 0;

 }
 
 // Set motor speeds
 
analogWrite(motorLen, motorLspeed);

analogWrite(motorRen, motorRspeed);

}

delay(100);

}

## Working Code Explanation Video

https://github.com/user-attachments/assets/841f11a5-8bcd-495b-88a9-b7e2914db04b


## Demo Video

https://github.com/Vigneshr2106/Remotely-Operated-Vehicle-ROV-/assets/165415082/28e736f9-6113-4dae-a2c7-bd2a89081963

## Final Video 
