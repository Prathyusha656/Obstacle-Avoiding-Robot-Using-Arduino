# Obstacle-Avoiding Robot Using Arduino

## Project Overview
An autonomous robot that uses an ultrasonic sensor to detect and avoid obstacles. This is a beginner-friendly robotics project designed to help students learn about sensors, motor control, and programming with Arduino.

## Uses & Applications
- Autonomous navigation in robotics
- Smart vacuum cleaners
- Automated delivery robots
- Educational robotics projects

## Components Required
- Arduino Uno
- Ultrasonic Sensor (HC-SR04)
- L298N Motor Driver Module
- DC Motors with Wheels
- Chassis
- Battery (9V or 12V Li-ion)
- Jumper Wires

## Circuit Diagram
![Circuit Diagram](/images/circuit%20digaram.jpg)  

## Code

```cpp
#define trigPin 9
#define echoPin 10
#define motor1A 4
#define motor1B 5
#define motor2A 6
#define motor2B 7

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(motor1A, OUTPUT);
  pinMode(motor1B, OUTPUT);
  pinMode(motor2A, OUTPUT);
  pinMode(motor2B, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration;
  int distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  Serial.println(distance);
  
  if (distance < 15) {  // Obstacle detected within 15 cm
    stopRobot();
    delay(500);
    turnRight();
    delay(600);
  } else {
    moveForward();
  }
}

void moveForward() {
  digitalWrite(motor1A, HIGH);
  digitalWrite(motor1B, LOW);
  digitalWrite(motor2A, HIGH);
  digitalWrite(motor2B, LOW);
}

void stopRobot() {
  digitalWrite(motor1A, LOW);
  digitalWrite(motor1B, LOW);
  digitalWrite(motor2A, LOW);
  digitalWrite(motor2B, LOW);
}

void turnRight() {
  digitalWrite(motor1A, HIGH);
 
