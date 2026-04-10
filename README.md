# 🎵 Invisible Motion-Triggered Sound System

## 📌 Project Overview
The **Invisible Motion-Triggered Sound System** is a smart and compact alert system that detects nearby objects or human presence and automatically produces a sound alert. The system is designed to remain hidden inside an enclosure, making it visually unobtrusive while still being highly functional.

---

## 🚀 Features
- 🔍 Motion detection using ultrasonic sensor  
- 🔊 Automatic sound/melody alert  
- 📟 Real-time distance display (OLED)  
- 🎯 Hidden / invisible setup  
- 💰 Low-cost and efficient  

---

## 🧠 Problem Statement
Traditional alert systems are often visible, expensive, and lack flexibility. This project aims to create a **low-cost, hidden, and smart alert system** that can detect motion and respond instantly without exposing hardware.

---

## 🌍 SDG Mapping
This project aligns with:
- **SDG 9: Industry, Innovation, and Infrastructure**
- Promotes affordable and smart technological solutions

---

## 🛠️ Components Used
- ESP8266 (NodeMCU)
- HC-SR04 Ultrasonic Sensor
- 0.96” OLED Display (SSD1306)
- Piezo Buzzer
- Breadboard
- Jumper Wires
- Resistors (for voltage divider)

---

## ⚙️ Working Principle
1. The ultrasonic sensor measures the distance of nearby objects.
2. The ESP8266 processes this data.
3. If an object is detected within a set range (e.g., 50 cm):
   - The buzzer plays a sound or melody.
   - The OLED display shows the distance.
4. If no object is nearby, the system remains idle.

---

## 🔌 Circuit Connections

### Ultrasonic Sensor
- VCC → 5V  
- GND → GND  
- TRIG → GPIO14 (D5)  
- ECHO → GPIO12 (D6) *(via voltage divider)*  

### Buzzer
- + → GPIO13 (D7)  
- – → GND  

### OLED Display (I2C)
- VCC → 3.3V  
- GND → GND  
- SDA → D2  
- SCL → D1  

---

## 💻 Code
```cpp
#define TRIG 14
#define ECHO 12
#define BUZZER 13

long duration;
int distance;

void setup() {
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(BUZZER, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);

  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);

  duration = pulseIn(ECHO, HIGH);
  distance = duration * 0.034 / 2;

  Serial.println(distance);

  if(distance < 50) {
    tone(BUZZER, 1000);
    delay(200);
    tone(BUZZER, 1500);
    delay(200);
    tone(BUZZER, 2000);
    delay(200);
    noTone(BUZZER);
  }

  delay(100);
}
