# Arduino-Password-Protected-Lock-System-with-Keypad-LCD-LEDs-and-Buzzer-Step-by-Step-Tutorial
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
