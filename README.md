# Smart Trash Can Project

## Overview
The **Smart Trash Can** project is an innovative waste management system that utilizes cutting-edge technology to improve the efficiency and convenience of waste disposal. The system is designed to automatically open its lid when someone approaches, measure the fill level of the trash can, and indicate when it is full. This project aims to provide a smart and hygienic solution for waste management, making it an ideal solution for households, offices, and public spaces.

## Components
- **Arduino Uno microcontroller**
- **Ultrasonic sensor** (for sensing the movement)
- **Servo motor** (for lid movement)
- **Battery** (9v for power supply)
- **Jumping wires**
- **Trash can**

## Working Concept
- It is important to dispose of the trash properly. It is a responsibility with which everyone should comply. In the era of Covid-19, people are trying to innovate everyday life things and make things as contactless as possible.
- The smart trash can uses an Ultrasonic sensor HC-SR04 to detect objects in front.
- It then sends the signals to Arduino Uno. The Arduino understands the signal and sends a signal to the Servo Motor which opens the flap on top of the dustbin.
- Here we have programmed it to open the flap for only 3 seconds; after 3 seconds the flap automatically closes.
- **Sensor Integration:** The Ultrasonic sensor is placed in front of the trash can and connected to the Arduino Uno. When a person approaches the trash can, the Ultrasonic sensor detects the presence and sends a signal to the Arduino Uno.

## Circuit Diagram
- The circuit diagram for the smart trash can contains three main components: Arduino Uno, Power supply, and an ultrasonic sensor.
- The Ultrasonic sensor HC-SR04 pins (echo and trig) are connected to Arduino Uno pins 5 and 6 respectively. The VCC pin is connected to 5V on Arduino Uno and both the grounds are connected together.
- The Servo motor signal pin is connected to 7, gnd to gnd, and positive to 3.3 V.
- A 9V battery has been connected to the Vin pin on the Arduino Uno and the grounds are connected together.

## Program Code
```cpp
#include <Servo.h>   //servo library

Servo servo;
int trigPin = 5;
int echoPin = 6;
int servoPin = 7;
int led= 10;
long duration, dist, average;
long aver[3];   //array for average

void setup() {
    Serial.begin(9600);
    servo.attach(servoPin);
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    servo.write(0);   //close cap on power on
    delay(100);
    servo.detach();
}

void measure() {
    digitalWrite(10,HIGH);
    digitalWrite(trigPin, LOW);
    delayMicroseconds(5);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(15);
    digitalWrite(trigPin, LOW);
    pinMode(echoPin, INPUT);
    duration = pulseIn(echoPin, HIGH);
    dist = (duration/2) / 29.1;    //obtain distance
}

void loop() {
    for (int i=0;i<=2;i++) {   //average distance
        measure();
        aver[i]=dist;
        delay(10);   //delay between measurements
    }
    dist=(aver[0]+aver[1]+aver[2])/3;
    if (dist < 50) {   //Change distance as per your need
        servo.attach(servoPin);
        delay(1);
        servo.write(0);
        delay(3000);
        servo.write(150);
        delay(1000);
        servo.detach();
    }
    Serial.print(dist);
}
```

## Challenges and Limitations
- Ensuring accurate distance measurements using the ultrasonic sensor.
- Managing power consumption to prolong battery life.

## Output
The Smart Trash Can project demonstrates an innovative approach to waste management by leveraging automation and sensor technology. The system's ability to automatically open its lid can improve user experience and encourage responsible waste disposal. With further refinements and improvements, this project has the potential to make a significant impact in the field of waste management.
