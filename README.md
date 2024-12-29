# Arduino-Password-Protected-Lock-System-with-Keypad-LCD-LEDs-and-Buzzer-Step-by-Step-Tutorial
# Arduino Password-Protected Lock System

## Overview
This project demonstrates a password-protected lock system using an Arduino. It uses a 4x4 keypad for input, a 16x2 I2C LCD for feedback, LEDs for status indication, and a buzzer for auditory feedback.

---

## Components and Connections
| **Component**         | **Pin**                   | **Arduino Pin**                |
|------------------------|---------------------------|---------------------------------|
| **4x4 Keypad**         | R1, R2, R3, R4           | Pins 2, 3, 4, 5               |
|                        | C1, C2, C3, C4           | Pins 6, 7, 8, 9               |
| **16x2 I2C LCD**       | GND                      | GND                           |
|                        | VCC                      | 5V                            |
|                        | SDA                      | A4                            |
|                        | SCL                      | A5                            |
| **Piezo Buzzer**       | Positive Terminal         | Pin 10                        |
|                        | Negative Terminal         | GND                           |
| **LEDs**               | Green LED Positive Terminal | Pin 11 (via 220-ohm resistor) |
|                        | Green LED Negative Terminal | GND                           |
|                        | Red LED Positive Terminal | Pin 12 (via 220-ohm resistor) |
|                        | Red LED Negative Terminal | GND                           |

---

## System Workflow
1. **Password Entry**:
   - Use the 4x4 keypad to enter the password.
   - Press `#` to submit the password.
   - Press `*` to clear the input.

2. **Feedback**:
   - **Correct Password**:
     - Green LED lights up for 1 second.
     - Buzzer emits a 1 kHz beep for 500 ms.
     - LCD displays "Access Granted!" for 1 second, then resets.
   - **Incorrect Password**:
     - Red LED lights up for 1 second.
     - Buzzer emits a 300 Hz beep for 1 second.
     - LCD displays "Access Denied!" for 1 second, then resets.

3. **Automatic Reset**:
   - After any attempt, the system clears the input and displays "Enter Password:" for the next attempt.

---

## Arduino Code

Here’s the Arduino code for the password-protected lock system:

```cpp
#include <Keypad.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define GREEN_LED 11
#define RED_LED 12
#define BUZZER 10

// Initialize the LCD
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Keypad setup
const byte ROWS = 4; // Four rows
const byte COLS = 4; // Four columns
char keys[ROWS][COLS] = {
  {'1', '2', '3', 'A'},
  {'4', '5', '6', 'B'},
  {'7', '8', '9', 'C'},
  {'*', '0', '#', 'D'}
};
byte rowPins[ROWS] = {2, 3, 4, 5}; // Connect to the row pins of the keypad
byte colPins[COLS] = {6, 7, 8, 9}; // Connect to the column pins of the keypad

Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

// Define the password
String password = "1234";
String input = "";

void setup() {
  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  pinMode(BUZZER, OUTPUT);

  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Enter Password:");
}

void loop() {
  char key = keypad.getKey();

  if (key) {
    if (key == '#') {
      checkPassword();
    } else if (key == '*') {
      input = "";
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Enter Password:");
    } else {
      input += key;
      lcd.setCursor(0, 1);
      lcd.print(input);
    }
  }
}

void checkPassword() {
  if (input == password) {
    // Correct password
    digitalWrite(GREEN_LED, HIGH);
    tone(BUZZER, 1000, 500);
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Access Granted!");
    delay(1000);
    digitalWrite(GREEN_LED, LOW);
  } else {
    // Incorrect password
    digitalWrite(RED_LED, HIGH);
    tone(BUZZER, 300, 1000);
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Access Denied!");
    delay(1000);
    digitalWrite(RED_LED, LOW);
  }
  input = "";
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Enter Password:");
}



Connections for the Password-Protected Lock System
Components and Connections
4x4 Keypad

R1, R2, R3, R4 → Arduino 2, 3, 4, 5
C1, C2, C3, C4 → Arduino 6, 7, 8, 9
16x2 I2C LCD (4 pins: GND, VCC, SDA, SCL)

GND → Arduino GND
VCC → Arduino 5V
SDA → Arduino A4
SCL → Arduino A5
Piezo Buzzer

Positive terminal → Arduino 10
Negative terminal → Arduino GND
LEDs

Access Granted LED:
Positive terminal → Arduino 11 (via 220-ohm resistor)
Negative terminal → Arduino GND
Access Denied LED:
Positive terminal → Arduino 12 (via 220-ohm resistor)
Negative terminal → Arduino GND
Steps to Test the System
Upload the Code: Ensure the I2C address of the LCD (0x27 or 0x3F) matches your module. Use the I2C scanner code (if needed) to verify.
Enter Password:
Use the keypad to enter the password.
Press # to submit.
Press * to clear the input at any time.
Feedback:
Correct Password:
Green LED lights up for 1 second.
Buzzer emits a 1 kHz beep for 500 ms.
LCD displays "Access Granted!" for 1 second, then resets.
Incorrect Password:
Red LED lights up for 1 second.
Buzzer emits a 300 Hz beep for 1 second.
LCD displays "Access Denied!" for 1 second, then resets.
Automatic Reset:
After any attempt, the system clears the input and displays "Enter Password:" for the next attempt.
Troubleshooting Tips
If the LCD backlight is on but no text appears:
Use the I2C scanner to check the LCD address.
Adjust the contrast potentiometer on the LCD module.
Ensure all connections are secure and match the specified pins.
Let me know if you encounter any issues or need additional modifications! 😊
