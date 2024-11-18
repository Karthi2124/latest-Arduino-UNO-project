# Code Overview
## 1. Libraries and Definitions

  AFMotor.h: The library is used to control DC motors with an Adafruit motor driver shield.
  Macros:
        u1_triger_high and u1_triger_low are macros for controlling the trigger pin of the ultrasonic sensor.

## 2. Global Variables

  AF_DCMotor motorX: Represents four motors (motor1, motor2, motor3, motor4) connected to the Adafruit shield.
  ult: Stores the distance measured by the ultrasonic sensor.
  command: Holds the Bluetooth command received from the serial input.

## 3. Setup Function

void setup() {
    Serial.begin(9600); // Initialize serial communication for Bluetooth or debugging.
    pinMode(A0, OUTPUT); // Ultrasonic trigger pin.
    pinMode(A1, INPUT);  // Ultrasonic echo pin.
    pinMode(IR_PIN, INPUT); // IR sensor input.
    
  motorX.setSpeed(255); // Set all motors to full speed.
}

  Purpose: Configures pins and initializes communication for motors, sensors, and serial communication.

## 4. Loop Function

The main logic evaluates sensor inputs and controls the robot's motion based on these inputs and Bluetooth commands.

 ### Ultrasonic Sensor Check:
      Distance (ult) is measured using read_ultrasonic1(). If the distance is less than 20 cm, the robot stops.

 ### IR Sensor Check:
        If the IR sensor detects an obstacle (irValue == LOW), the robot stops.

 ### Bluetooth Commands:
        Commands are read from the serial input and executed using handleOtherCommands().

## 5. Command Handling

void handleOtherCommands(char command) {
    if (Serial.available() > 0) {
        char command = Serial.read(); // Read the command.
        switch (command) {
            case '1': moveForward(); break;    // Forward
            case '2': moveBackward(); break;   // Backward
            case '3': turnLeft(); break;       // Turn Left
            case '4': turnRight(); break;      // Turn Right
            case '5': stopRobot(); break;      // Stop
        }
    }
}

  ### Each command corresponds to a specific movement:
        '1': Move forward.
        '2': Move backward.
        '3': Turn left.
        '4': Turn right.
        '5': Stop.

## 6. Movement Functions

  Each movement is defined by setting the motor speeds and directions using the AF_DCMotor API.

### Example for moving forward:

void moveForward() {
    motor1.run(FORWARD);
    motor2.run(FORWARD);
    motor3.run(FORWARD);
    motor4.run(FORWARD);
}

  Similar functions control other movements like moving backward, turning left, and turning right.

## 7. Sensor Functions

  ### Ultrasonic Sensor:

unsigned int read_ultrasonic1() {
    u1_triger_low; delay(1); // Set trigger low, wait 1 ms.
    u1_triger_high; delay(10); // Set trigger high, wait 10 ms.
    u1_triger_low; // Set trigger low again.
    ultrasonic = pulseIn(ultra1, HIGH) / 56.0; // Measure echo time and convert to distance.
    return ultrasonic;
}

  Sends a trigger pulse and measures the echo time to calculate the distance.

### How It Works

  Setup Phase:
        Configures pins, motors, and sensors.
        Sets motor speeds to full by default.

  Execution Phase (Loop):
        Reads the distance using the ultrasonic sensor.
        Reads the obstacle status using the IR sensor.
        Listens for commands from Bluetooth (via Serial).

  Behavior:
        Stops if the ultrasonic or IR sensor detects obstacles.
        Executes movements (forward, backward, etc.) based on Bluetooth commands.

## Applications

  Obstacle Avoidance: Stops when an object is detected within 20 cm (ultrasonic sensor) or by the IR sensor.
  Remote Control: Users can control the robot using a Bluetooth app or terminal commands.
  Autonomous Navigation: Combines sensor inputs with predefined logic to navigate autonomously.
