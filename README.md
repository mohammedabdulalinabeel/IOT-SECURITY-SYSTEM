🚀 Project Title
IoT Motion-Based Security System
Build a Security System That Detects Motion, Captures Images, and Sends Alerts to a Mobile App

📋 Intern Details

👨‍💼 Name: Mohammed Abdul Ali Nabeel

🎓 Intern ID: CITS0D781

🏢 Company: CodTech IT Solutions

🌐 Domain: Internet of Things

📅 Internship Duration: 4 Weeks

🧑‍🏫 Mentor: Neela Santhosh

📌 Project Overview
This project presents a smart IoT-based security system using an ESP32-CAM and PIR motion sensor. When motion is detected, the ESP32-CAM captures an image and sends it as an alert via the Telegram bot to a mobile device in real-time. This prototype demonstrates a low-cost, Internet-connected security solution for homes or offices.

🔧 Components Required
Component     	Quantity
ESP32-CAM	        1
PIR Motion Sensor	1
FTDI Programmer	  1
Jumper Wires	    As needed
Breadboard	      1
Telegram App    	1
Wi-Fi Connection	Required

🧩 Circuit Connections
PIR Sensor to ESP32-CAM:

PIR Sensor	ESP32-CAM
VCC	       5V
GND	       GND
OUT	       GPIO 13

FTDI Programmer to ESP32-CAM:

FTDI Pin	ESP32-CAM Pin
TX	       U0R (RX)
RX	       U0T (TX)
GND	       GND
5V	       5V
IO0	       GND (for uploading code only)

⚙️ Working Principle
PIR sensor detects motion in its range.

ESP32-CAM captures an image upon motion trigger.

Image is sent to a pre-configured Telegram bot.

User receives the photo alert in real-time on their smartphone.


🧩 Circuit Diagram
<img width="1536" height="1024" alt="ChatGPT Image Jul 14, 2025, 08_36_35 PM" src="https://github.com/user-attachments/assets/9a685086-ffe3-4b63-aef6-a7fe26803a51" />
