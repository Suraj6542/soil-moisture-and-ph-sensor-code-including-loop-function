const int sensor_pin = A1;         
const int pH_sensor_pin = A0;       
unsigned long int avgValue;         
float b;
int buf[10],temp;

void setup()
{
  pinMode(13, OUTPUT);            
  Serial.begin(9600);             
  Serial.println("Ready");          
}

void loop()
{
  // Soil Moisture Sensor Code
  float moisture_percentage;
  int sensor_analog;
  sensor_analog = analogRead(sensor_pin);
  moisture_percentage = (100 - ((sensor_analog/1023.00) * 100));
  Serial.print("Moisture Percentage = ");
  Serial.print(moisture_percentage);
  Serial.print("%\n\n");

  // pH Sensor Code
  for(int i=0; i<10; i++)           
  { 
    buf[i] = analogRead(pH_sensor_pin);
    delay(10);
  }

  for(int i=0; i<9; i++)           
  {
    for(int j=i+1; j<10; j++)
    {
      if(buf[i] > buf[j])
      {
        temp = buf[i];
        buf[i] = buf[j];
        buf[j] = temp;
      }
    }
  }

  avgValue = 0;
  for(int i=2; i<8; i++)            
    avgValue += buf[i];

  float phValue = (float)avgValue * 5.0 / 1024 / 6; 
  phValue = 3.5 * phValue;           

  Serial.print("pH:");  
  Serial.print(phValue, 2);
  Serial.println(" ");

  digitalWrite(13, HIGH);          
  delay(800);
  digitalWrite(13, LOW);          
  delay(200);
}
