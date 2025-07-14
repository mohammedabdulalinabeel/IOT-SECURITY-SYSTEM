# IOT MOTION-BASED-SECURITY-SYSTEM
 Project Title
IoT Motion-Based Security System
Build a Security System That Detects Motion, Captures Images, and Sends Alerts to a Mobile App

 Intern Details
 Name: Mohammed Abdul Ali Nabeel

 Intern ID: CITS0D781

 Company: CodTech IT Solutions

 Domain: Internet of Things

 Internship Duration: 4 Weeks

 Mentor: Neela Santhosh

 Project Overview
This project presents a smart IoT-based security system using an ESP32-CAM and PIR motion sensor. When motion is detected, the ESP32-CAM captures an image and sends it as an alert via the Telegram bot to a mobile device in real-time. This prototype demonstrates a low-cost, Internet-connected security solution for homes or offices.

 Components Required
Component	              Quantity
ESP32-CAM	                1
PIR Motion Sensor	        1
FTDI Programmer          	1
Jumper Wires         	As needed
Breadboard	              1
Telegram App            	1
Wi-Fi Connection     	Required

 Circuit Connections
PIR Sensor to ESP32-CAM:

PIR Sensor	ESP32-CAM
VCC	        5V
GND	        GND
OUT	        GPIO 13

FTDI Programmer to ESP32-CAM:

FTDI Pin  	ESP32-CAM Pin
TX	         U0R (RX)
RX	U0T        (TX)
GND	          GND
5V	           5V
IO0	          GND (for uploading code only)

⚙ Working Principle
PIR sensor detects motion in its range.
ESP32-CAM captures an image upon motion trigger.
Image is sent to a pre-configured Telegram bot.
User receives the photo alert in real-time on their smartphone.

CODE:

#include <WiFi.h>
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>
#include "esp_camera.h"

const char* ssid = "YourWiFi";
const char* password = "YourPassword";

#define BOTtoken "YourTelegramBotToken"
#define CHAT_ID "YourChatID"

WiFiClientSecure client;
UniversalTelegramBot bot(BOTtoken, client);

#define PIR_PIN 13
unsigned long lastSendTime = 0;
const unsigned long interval = 10000;

void setup() {
  Serial.begin(115200);
  pinMode(PIR_PIN, INPUT);

  camera_config_t config;
  config.ledc_channel = LEDC_CHANNEL_0;
  config.ledc_timer = LEDC_TIMER_0;
  config.pin_d0 = 5;
  config.pin_d1 = 18;
  config.pin_d2 = 19;
  config.pin_d3 = 21;
  config.pin_d4 = 36;
  config.pin_d5 = 39;
  config.pin_d6 = 34;
  config.pin_d7 = 35;
  config.pin_xclk = 0;
  config.pin_pclk = 22;
  config.pin_vsync = 25;
  config.pin_href = 23;
  config.pin_sscb_sda = 26;
  config.pin_sscb_scl = 27;
  config.pin_pwdn = 32;
  config.pin_reset = -1;
  config.xclk_freq_hz = 20000000;
  config.pixel_format = PIXFORMAT_JPEG;
  config.frame_size = FRAMESIZE_VGA;
  config.jpeg_quality = 10;
  config.fb_count = 2;

  if (esp_camera_init(&config) != ESP_OK) {
    Serial.println("Camera init failed");
    return;
  }

  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  client.setInsecure();
  Serial.println("\nWiFi connected");
  bot.sendMessage(CHAT_ID, "Security Bot Activated", "");
}

void loop() {
  if (digitalRead(PIR_PIN) == HIGH && millis() - lastSendTime > interval) {
    sendPhoto();
    lastSendTime = millis();
  }
}

void sendPhoto() {
  camera_fb_t *fb = esp_camera_fb_get();
  if (!fb) {
    Serial.println("Camera capture failed");
    return;
  }

  bot.sendPhotoByBinary(CHAT_ID, "image/jpeg", fb->len, fb->buf, "Intruder.jpg", "");
  esp_camera_fb_return(fb);
  Serial.println("Photo sent to Telegram!");
}


  Circuit Diagram
 <img width="1536" height="1024" alt="ChatGPT Image Jul 14, 2025, 08_36_35 PM" src="https://github.com/user-attachments/assets/481a38c7-b728-496d-b30a-1d2b4da7029f" />


 
