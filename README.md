#include <Arduino.h>
const int sensor_pin = A1;
float resolution;                                
int measurings;
float voltage;
float pHvalue;
float b = 0.00;
float m = 0.167;

void setup() {
  Serial.begin(9600);
  resolution = 1024.0;
delay(100);
}

void loop() {
   measurings=0;
for (int i = 0; i < 10; i++)                   
  {
    measurings = measurings + analogRead(A0);     
    delay(10);                                  
  }
    voltage = ((5 / resolution) * (measurings/10)); 
                                                   
    pHvalue = ((7 + ((2.5 - voltage) / m)))+ b; 

  float moisture_percentage;
  int sensor_analog; 

  
  sensor_analog = analogRead(sensor_pin);
  moisture_percentage = ( 100 - ( (sensor_analog/1023.00) * 100 ) );
  Serial.print("Moisture Percentage = ");
  Serial.print(moisture_percentage);
  Serial.print("%\n\n");
   Serial.print("pH= ");                          
    Serial.println(pHvalue);
  delay(1000);
}
