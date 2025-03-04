Circuit Documentation
Summary
This circuit is designed to control a pair of hobby gearmotors using an L298N DC motor driver, which is interfaced with an Arduino UNO microcontroller. The Arduino UNO receives commands via a Bluetooth connection through an HC-05 Bluetooth Module. The motors can be controlled to move in different directions (forward, backward, left, right) or to stop, based on the commands received. The circuit is powered by a 12V battery, which supplies power to the motor driver and indirectly to the Arduino and Bluetooth module.
Component List
Arduino UNO
Microcontroller board based on the ATmega328P
Used for processing and sending control signals to the motor driver
Interfaces with the HC-05 Bluetooth Module for wireless communication
L298N DC Motor Driver
Dual H-Bridge motor driver capable of driving two DC motors
Receives control signals from the Arduino UNO to drive the motors
Powered directly by the 12V battery
HC-05 Bluetooth Module
Wireless communication module that enables Bluetooth connectivity
Allows the Arduino UNO to receive commands wirelessly from a Bluetooth-enabled device
Battery 12V
Provides the main power source for the motor driver and indirectly for the Arduino and Bluetooth module
Hobby Gearmotor with 48:1 Gearbox (x2)
DC motors with gear reduction
Driven by the L298N motor driver to perform mechanical movements
Comments
Placeholder components for additional notes or documentation (not physically present in the circuit)
Wiring Details
Arduino UNO
5V connected to HC-05 Bluetooth Module VCC
GND connected to HC-05 Bluetooth Module GND and battery (-)
D0 (RX) connected to HC-05 Bluetooth Module TXD
D1 (TX) connected to HC-05 Bluetooth Module RXD
Digital pins D8, D9, D10, D11 used to control the L298N motor driver
L298N DC Motor Driver
12V connected to battery (+)
GND connected to battery (-)
OUT1, OUT2 connected to one Hobby Gearmotor
OUT3, OUT4 connected to the other Hobby Gearmotor
IN1, IN2, IN3, IN4 controlled by Arduino digital pins
HC-05 Bluetooth Module
VCC connected to Arduino 5V
GND connected to Arduino GND
TXD connected to Arduino D0 (RX)
RXD connected to Arduino D1 (TX)
Battery 12V
(+) connected to L298N 12V
(-) connected to Arduino GND and L298N GND
Hobby Gearmotor with 48:1 Gearbox
Two motors, each connected to two output pins of the L298N motor driver
Documented Code
#include <SoftwareSerial.h>

SoftwareSerial BT(2, 3); // RX, TX for Bluetooth
int IN1 = 8, IN2 = 9, IN3 = 10, IN4 = 11; // Motor driver pins

void setup() {
    Serial.begin(9600);
    BT.begin(9600);
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
}

void loop() {
    if (BT.available()) {
        char command = BT.read();
        Serial.println(command);
        controlCar(command);
    }
}

void controlCar(char command) {
    switch (command) {
        case 'F': // Forward
            digitalWrite(IN1, HIGH);
            digitalWrite(IN2, LOW);
            digitalWrite(IN3, HIGH);
            digitalWrite(IN4, LOW);
            break;
        case 'B': // Backward
            digitalWrite(IN1, LOW);
            digitalWrite(IN2, HIGH);
            digitalWrite(IN3, LOW);
            digitalWrite(IN4, HIGH);
            break;
        case 'L': // Left
            digitalWrite(IN1, LOW);
            digitalWrite(IN2, HIGH);
            digitalWrite(IN3, HIGH);
            digitalWrite(IN4, LOW);
            break;
        case 'R': // Right
            digitalWrite(IN1, HIGH);
            digitalWrite(IN2, LOW);
            digitalWrite(IN3, LOW);
            digitalWrite(IN4, HIGH);
            break;
        case 'S': // Stop
            digitalWrite(IN1, LOW);
            digitalWrite(IN2, LOW);
            digitalWrite(IN3, LOW);
            digitalWrite(IN4, LOW);
            break;
    }
}


This code is designed to run on the Arduino UNO and controls the motors via the L298N motor driver based on the commands received from the HC-05 Bluetooth Module. The SoftwareSerial library is used to create a serial communication channel on pins 2 and 3 for Bluetooth communication. The controlCar function interprets the received character commands and sets the motor driver pins accordingly to control the motors' direction and speed.
