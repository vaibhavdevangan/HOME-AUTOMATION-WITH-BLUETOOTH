# HOME-AUTOMATION-WITH-BLUETOOTH
TASK 3 (EMBEDDED SYSTEM INTERNSHIP)

COMPANY  : CODTECH IT SOLUTIONS

NAME     : VAIBHAV UMESH DEWANGAN

INTERN ID: CT08MYM

DOMAIN   : EMBEDDED SYSTEMS

BATCH DURATION : January 20th,2025 to February 20th,2025 (4 Weeks)

MENTOR NAME: Neela Santhosh Kumar


A simple home automation system using Bluetooth and a Serial Bluetooth Terminal app to control an LED.

Features

✅ Turn LED ON/OFF using Bluetooth commands
✅ Uses a Serial Bluetooth Terminal for communication
✅ Simple and easy to implement


---

Hardware Required

ESP32 module

LED

Resistor (220Ω)

Power Supply



---

Circuit Diagram

![Image](https://github.com/user-attachments/assets/e18cc466-133b-40c4-b52d-ae987a8916a5)

---

Installation & Setup

1. Upload the Code to ESP32

1. Connect your microcontroller to your PC.


2. Open the Arduino IDE.


3. Install the required libraries (if needed).


4. Upload the following code:


include "BluetoothSerial.h"

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run make menuconfig to and enable it
#endif

BluetoothSerial SerialBT;
int received;// received value will be stored in this variable
char receivedChar;// received value will be stored as CHAR in this variable

const char turnON ='a';
const char turnOFF ='b';
const int LEDpin = 23;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("ESP32_Robojax"); //Bluetooth device name
  Serial.println("The device started, now you can pair it with bluetooth!");
  Serial.println("To turn ON send: a");//print on serial monitor  
  Serial.println("To turn OFF send: b"); //print on serial monitor 
  pinMode(LEDpin, OUTPUT);
 
}

void loop() {
    receivedChar =(char)SerialBT.read();

  if (Serial.available()) {
    SerialBT.write(Serial.read());
  
  }
  if (SerialBT.available()) {
    
    SerialBT.print("Received:");// write on BT app
    SerialBT.println(receivedChar);// write on BT app      
    Serial.print ("Received:");//print on serial monitor
    Serial.println(receivedChar);//print on serial monitor    
    //SerialBT.println(receivedChar);//print on the app    
    //SerialBT.write(receivedChar); //print on serial monitor
    if(receivedChar == turnON)
    {
     SerialBT.println("LED ON:");// write on BT app
     Serial.println("LED ON:");//write on serial monitor
     digitalWrite(LEDpin, HIGH);// turn the LED ON
       
    }
    if(receivedChar == turnOFF)
    {
     SerialBT.println("LED OFF:");// write on BT app
     Serial.println("LED OFF:");//write on serial monitor
      digitalWrite(LEDpin, LOW);// turn the LED off 
    }    
     
  

  }
  delay(20);
}


---

2. Connect via Serial Bluetooth Terminal App

1. Install Serial Bluetooth Terminal from the Play Store.


2. Pair your Bluetooth module with your phone.


3. Open the app, connect to your module, and send:

"a" → Turns the LED ON

"b" → Turns the LED OFF


---


WORKING:--


This project allows users to control an LED wirelessly using Bluetooth communication between an ESP32 microcontroller and a mobile phone running the Serial Bluetooth Terminal app.

Step-by-Step Working

1. Bluetooth Communication Setup

The ESP32 has a built-in Bluetooth module, which allows wireless communication with the Serial Bluetooth Terminal app on a smartphone.

The mobile app sends ASCII characters ('a' and 'b') via Bluetooth Serial (UART), which the ESP32 reads and processes.


2. Command Processing in ESP32

The ESP32 continuously listens for incoming Bluetooth data.

When the user sends a command from the Serial Bluetooth Terminal app, the ESP32 reads the received character and performs an action accordingly:

'a' → Turn LED ON

'b' → Turn LED OFF



3. LED Control

If ESP32 receives 'a', it sets the LED pin to HIGH, turning it ON.

If ESP32 receives 'b', it sets the LED pin to LOW, turning it OFF.


4. Serial Monitor Logging

ESP32 prints debug messages ("LED ON" or "LED OFF") to the Serial Monitor for real-time feedback.

This helps in verifying whether the Bluetooth commands are received correctly.


5. Mobile App Interaction

The user interacts with the system via the Serial Bluetooth Terminal app:

  1. Pair the ESP32 Bluetooth with the smartphone.

  2. Open the Serial Bluetooth Terminal app and connect to ESP32.

  3. Send 'a' to turn the LED ON and 'b' to turn it OFF.


-------------------------------------------------

How to Run the Project-->

Clone this repository
https://github.com/vaibhavdevangan/HOME-AUTOMATION-WITH-BLUETOOTH

Open the .ino file in Arduino IDE.

Connect your ESP32 board and select the correct COM Port.

Upload the code to the ESP32.

Open Serial Monitor (Baud rate: 115200).

