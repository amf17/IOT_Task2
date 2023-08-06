#  Arduino Communication and LED Control with Pushbutton

## Introduction:

This report documents a simple Arduino project that involves communication between two Arduino boards and controlling an LED using a pushbutton. The project uses Serial communication to send the state of a pushbutton from one Arduino board to another, and based on the received state, the second Arduino controls an LED. The goal is to demonstrate basic communication between two Arduino boards and showcase LED control using a pushbutton.

## Hardware Setup:
1- Arduino Board 1 (Sender):

Pin 2: Connected to a pushbutton with a pull-up resistor.
Serial Communication: Connected to a computer via USB for monitoring and debugging.

2- Arduino Board 2 (Receiver):

Pin 13: Connected to an LED.
Serial Communication: Connected to Arduino Board 1 via a wired connection.

## Code Description:

1- Arduino Board 1 (Sender) Code:
```
void setup() {
  // Start serial connection
  Serial.begin(9600);
  // Configure pin 2 as an input and enable the internal pull-up resistor
  pinMode(2, INPUT_PULLUP);
}

void loop() {
  // Read the pushbutton value into a variable
  int sensorVal = digitalRead(2);
  // Send the pushbutton value to Arduino2 via Serial communication
  Serial.println(sensorVal);
  delay(100); // A small delay to avoid flooding the Serial communication
}

```
The sender Arduino board sets up Serial communication with a baud rate of 9600 and configures Pin 2 as an input with an internal pull-up resistor enabled.

In the loop function, it reads the state of the pushbutton connected to Pin 2 using the digitalRead() function.

The read value of the pushbutton is sent to Arduino Board 2 (Receiver) via Serial communication using the Serial.println() function.

A small delay of 100 milliseconds is added to avoid excessive data transmission through Serial.


2- Arduino Board 2 (Receiver) Code:

```
int ledPin = 13; // LED connected to pin 13

void setup() {
  // Start serial connection
  Serial.begin(9600);
  // Configure pin 13 as an output
  pinMode(ledPin, OUTPUT);
}

void loop() {
    int sensorVal = Serial.parseInt();

    // Keep in mind the pull-up means the pushbutton's logic is inverted.
    // It goes HIGH when it's open, and LOW when it's pressed.
    // Turn on the LED when the button's pressed, and off when it's not:
    if (sensorVal == HIGH) {
      digitalWrite(ledPin, LOW);
    } else {
      digitalWrite(ledPin, HIGH);
    }
  }
```
The receiver Arduino board sets up Serial communication with a baud rate of 9600 and configures Pin 13 as an output to control the LED.

In the loop function, it listens for incoming Serial data from Arduino Board 1 (Sender) using the Serial.parseInt() function.

The received value is stored in the sensorVal variable.

If the received value is HIGH (indicating the pushbutton is not pressed), the LED connected to Pin 13 is turned on by setting it to LOW.

If the received value is LOW (indicating the pushbutton is pressed), the LED is turned off by setting Pin 13 to HIGH.

## Conclusion:

This Arduino project successfully demonstrates a basic communication setup between two Arduino boards using Serial communication. The first Arduino (Sender) reads the state of a pushbutton and sends its state to the second Arduino (Receiver) via Serial. The receiver Arduino then controls an LED based on the received pushbutton state. This project can serve as a starting point for more complex Arduino projects involving communication between multiple boards and various sensor inputs.

![image](https://github.com/amf17/IOT_Task2/assets/139582388/63544e2e-b8f1-40ad-b609-b7af0f64a051)
