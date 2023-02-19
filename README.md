# soil-moisture-and-ph-sensor-code-including-loop-function

int pHSense = A0;
int soilhum = A1;
int samples = 10;
float adc_resolution = 1024.0;

float ph(float voltage) {
  return 7 + ((2.5 - voltage) / 0.18);
}

void setup() {
  Serial.begin(9600);
}

void loop() {

  int measurings = 0;
  int soilwater = 0;

  soilwater = analogRead(A2);

  for (int i = 0; i < samples; i++) {
    measurings += analogRead(pHSense);
    delay(10);
  }

  float voltage = 5 / adc_resolution * measurings / samples;
  Serial.print("pH= ");
  Serial.println(ph(voltage));
  Serial.print(",");
  Serial.println(soilwater);
  delay(3000);
}
