---
layout: post
title: Plant O Lingo
description:  
    Plant O Lingo is a smart, modular plant care system developed using the iterative engineering design process. It monitors soil moisture using sensors, automatically waters the plant via a solenoid valve, and displays plant health status on an LCD. The structure is a scalable acrylic frame, integrating adjustable components, lighting, and communication systems to notify users of plant needs via text.
skills: 
  - Sensor integration
  - Circuit design
  - Embedded systems (Arduino)
  - CAD modeling (SolidWorks)
  - 3D printing
  - Acrylic prototyping
  - Serial communication
  - LCD interface

main-image: /plantOLingo.jpg
---

---

## Demo
<br>
{% include youtube-video.html id="QMqYJ8tsa5o" autoplay="false" %}
<br>

This Arduino-based smart plant monitoring system automates plant care by continuously checking soil moisture levels and providing responsive feedback to the user. It uses two analog moisture sensors connected to the Arduino to read the water content in the soil. By powering the sensors only during readings, the design prevents corrosion and conserves energy. Depending on the results, the system decides whether the plant needs more water, less water, or is in a healthy state. A solenoid valve is activated to water the plant if the moisture level is too low, delivering water through a controlled 4-second release. Meanwhile, a liquid crystal display (LCD) updates in real-time to inform the user of the plant’s condition.

In addition to moisture sensing and watering, the system also includes a light connected to an output pin, which is toggled each cycle—possibly to simulate day/night cycles or support plant growth. The user interface is simple but effective, displaying direct messages such as “plant needs more water” or “plant has good water” to communicate the system’s assessment. The entire monitoring and watering cycle is designed to run once every 24 hours, minimizing power consumption while still ensuring the plant is regularly maintained. This approach provides a low-maintenance, user-friendly solution for plant care that merges basic electronics with functional automation.

<br>


## Plant O Lingo

<br>
{% include image-gallery.html images="Plant.jpg" height="400" %}



## Arduino Code
<pre><code class="language-cpp">

#include <LiquidCrystal.h>         

LiquidCrystal lcd(13, 12, 11, 10, 9, 8);  
int SensorPin1 = A0;
int SensorPin2 = A1;
int sensorValue;
int soilPower1 = 7;
int soilPower2 = 6;
int light = A2;
int solenoid = A3;

void setup() {                     
  Serial.begin(9600);
  Serial.print("Soil Moisture = ");

  pinMode(solenoid, OUTPUT);
  pinMode(light, OUTPUT);
  

  pinMode(soilPower1, OUTPUT);
  pinMode(soilPower2, OUTPUT);
  digitalWrite(soilPower1, LOW);
  digitalWrite(soilPower2, LOW);  
  
  
  lcd.begin(16, 2);                 
  lcd.clear();                      
}

void loop() {
   digitalWrite(light, LOW);
   delay(2000);
   digitalWrite(light, HIGH);
   
   for (int i = 0; i <= 10; i++) { 

   digitalWrite(soilPower1, HIGH);
   digitalWrite(soilPower2, HIGH);
   delay(10);
   digitalWrite(soilPower1, LOW);
   digitalWrite(soilPower2, LOW);
   sensorValue = sensorValue + analogRead(SensorPin1)+analogRead(SensorPin2); 
   delay(1000); 
   } 

   sensorValue = sensorValue/20;
   lcd.setCursor(0,0);
   lcd.print(sensorValue);

   if(sensorValue < 450){
     lcd.clear();
     lcd.setCursor(0,0);
     lcd.print("plant needs");
     lcd.setCursor(0,1);
     lcd.print("more water");
     delay(1000);
     lcd.clear();

     digitalWrite(solenoid, HIGH);
     delay(4000);
     digitalWrite(solenoid, LOW);
   }
   else if(sensorValue > 520){
     lcd.clear();
     lcd.setCursor(0,0);
     lcd.print("plant needs");
     lcd.setCursor(0,1);
     lcd.print("less water");
     delay(1000);
     lcd.clear();
   }
   else{
     lcd.clear();
     lcd.setCursor(0,0);
     lcd.print("plant has");
     lcd.setCursor(0,1);
     lcd.print("good water");
     delay(1000);
     lcd.clear();
   }
  delay(86400000);
}  
</code></pre>