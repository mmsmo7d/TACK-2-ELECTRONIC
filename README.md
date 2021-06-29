# TACK-2-ELECTRONIC
Specifications

    Output A, Output B – To connect two motors.
    Driver Power Input – Board can accept 5V to 35V which will act as the power supply to motor and internal 5V voltage regulator (if it is enabled using jumper).
    GND – Common Ground
    5V Output / Logic Input Voltage – This pin will give 5V output if the on-board regulator is enabled using the jumper, other we should give the logic supply (5V in the case of Arduino Uno) to this pin.
    IN1, IN2, IN3, IN4 – H-Bridge control inputs which can be used to control direction of motors.
    Enable A and Enable B pins are used for enabling each bridge or for controlling the speed of the motors using PWM.





Description

    As mentioned above L298N contains two pairs output which are connected to a pair of DC motors.
    The positive of battery is connected to the Power Input of the L298N module and negative is connected to GND.
    The 5V pin of the driver is connected to the Vin pin of the Arduino to power the Arduino board.
    Input 1 and Input 2 pins are used to control the direction of Motor 1 is connected to pin 13, pin 12 of the Arduino respectively.
    Input 3 and Input 4 pins are used to control the direction of Motor 2 is connected to pin 11, pin 10 of the Arduino respectively.
    Enable A and Enable B are connected to the pin 9 and pin 3 of Arduino, which are used to control the speed of motors using PWM.


Program code
// Motor A connections
int enA = 9;
int in1 = 13;
int in2 = 12;
// Motor B connections
int enB = 3;
int in3 = 11;
int in4 = 10;

void setup() {
    pinMode(enA, OUTPUT);
    pinMode(enB, OUTPUT);
    pinMode(in1, OUTPUT);
    pinMode(in2, OUTPUT);
    pinMode(in3, OUTPUT);
    pinMode(in4, OUTPUT);
	
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);
}

void loop() {
    directionControl();
    delay(1000);
    speedControl();
    delay(1000);
}
void directionControl() {
    // Set motors to maximum speed
    // PWM value ranges from 0 to 255
    analogWrite(enA, 255);
    analogWrite(enB, 255);

    // Turn on motor A & B
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);
    delay(2000);

    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);
    delay(2000);
	
    // Turn off motors
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);
}
void speedControl() {
    // Turn on motors
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);
	
    for (int i = 0; i < 256; i++) {
        analogWrite(enA, i);
        analogWrite(enB, i);
        delay(20);
    }
	
    for (int i = 255; i >= 0; --i) {
        analogWrite(enA, i);
        analogWrite(enB, i);
        delay(20);
    }
	
    // Now turn off motors
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);
}
 









