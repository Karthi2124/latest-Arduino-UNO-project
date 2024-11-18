# voice-controlled robot using an Arduino UNO 
### Creating a voice-controlled robot using an Arduino UNO involves using a voice recognition module or smartphone app that converts voice commands into serial data, which is then sent to the Arduino UNO to control the robot's movements.Here's a step-by-step explanation:

## Components Required

  Arduino UNO: The brain of the robot, processes voice commands.
  L298N Motor Driver Module: Controls the DC motors for movement.
  DC Motors (2 or 4): Enable the robot to move forward, backward, turn left, or right.
  Chassis: Robot body to mount motors and components.
  ## Voice Recognition Module:
   Option 1: Dedicated module like Elechouse Voice Recognition Module V3.
   Option 2: A smartphone app (like Arduino Bluetooth Controller) that converts voice commands to serial data and sends it to the Arduino via Bluetooth.
  Bluetooth Module (HC-05 or HC-06): For wireless communication with the smartphone.
  Battery Pack: Powers the Arduino and motors.

## Working Principle

  ### Voice Input:
  The user speaks a command (e.g., "Forward," "Stop").
  A smartphone app or a voice recognition module interprets the command and sends corresponding serial data to the Arduino UNO via Bluetooth.

  ### Command Processing:
  The Arduino receives the command and matches it to predefined actions (e.g., move forward, backward, stop).

  ### Motor Control:
  Based on the command, the Arduino sends signals to the motor driver module to control the direction and speed of the motors.

 # How to Set Up
## 1. Hardware Connections:

 ### Motors to Motor Driver:
  Connect DC motors to the L298N motor driver outputs (e.g., M1 and M2).
  Connect the motor driver input pins to Arduino (e.g., D3, D4, D5, D6).
  ### Bluetooth Module:
  TX to Arduino RX.
  RX to Arduino TX.
  ### Power:
  Connect the battery pack to the motor driver and Arduino.

## 2. Software Setup:

  Use a smartphone app like Arduino Bluetooth Controller.
        Configure it to send specific characters for each command (e.g., "F" for forward, "S" for stop).

## 3. Upload Code:

  Upload the provided code to the Arduino UNO using the Arduino IDE.

## 4. Test:

  Pair the Bluetooth module with your smartphone.
  Launch the app, speak a command (or use buttons), and observe the robot's movements.

## Commands and Behavior

  "Forward" (F): Moves the robot forward.
  "Backward" (B): Moves the robot backward.
  "Left" (L): Turns the robot left.
  "Right" (R): Turns the robot right.
  "Stop" (S): Stops all motors.

## Applications

  Educational Robotics: Demonstrates wireless control concepts.
  Assistive Technology: Helps individuals control devices using voice.
  Smart Vehicles: Basis for developing autonomous or smart robots.

