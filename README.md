void setup() {
pinMode(7,INPUT);
Serial.begin(9600);
pinMode(13,OUTPUT);
}
void loop() {
Serial.print("IRSensorip ");
Serial.println(digitalRead(7));
if(digitalRead(7)==0)
{
digitalWrite(13,HIGH);
}
else{
digitalWrite(13,LOW);
}
}

#dht
#include "DHT.h"
#define DHTPIN 2 // what pin we're connected to
#define DHTTYPE DHT11 // DHT 11
// Initialize DHT sensor for normal 16mhz Arduino
DHT dht(DHTPIN, DHTTYPE);
void setup() {
Serial.begin(9600);
Serial.println("DHTxx test!");
dht.begin();
}
void loop() {
// Wait a few seconds betweenmeasurements.
delay(2000);
// Reading temperature or humidity takes about 250 milliseconds!
// Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
float h = dht.readHumidity();
// Read temperature as Celsius
float t = dht.readTemperature();
// Read temperature as Fahrenheit
float f = dht.readTemperature(true);
// Check if any reads failed and exit early (to try again).
if (isnan(h) || isnan(t) || isnan(f)) {
Serial.println("Failed to read from DHT sensor!");
return;
}
// Compute heat index
// Must send in temp in Fahrenheit!
float hi = dht.computeHeatIndex(f, h);
Serial.print("Humidity: ");
Serial.print(h);
Serial.print(" %\t");
Serial.print("Temperature: ");
Serial.print(t);
Serial.print(" *C ");
Serial.print(f);
Serial.print(" *F\t");
Serial.print("Heat index: ");
Serial.print(hi);
Serial.println(" *F");
}
