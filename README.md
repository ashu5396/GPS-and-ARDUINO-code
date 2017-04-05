#include "TinyGPS++.h"
#include "SoftwareSerial.h"

SoftwareSerial serial_connection(11,10);
TinyGPSPlus gps;


void setup()
{
 Serial.begin(9600);
 
 serial_connection.begin(9600); 
 delay(1000); 
 }
void loop()
{
 while(serial_connection.available())
 {
  gps.encode(serial_connection.read());
  } 
  if(gps.location.isUpdated())
  {
    Serial.println("Satellite Count:");
    Serial.println(gps.satellites.value());
    Serial.println("Latitude:");
    Serial.println(gps.location.lat(),6);
    Serial.println("Longitude:");
    Serial.println(gps.location.lng(),6);
    Serial.println("Speed MPH:");
    Serial.println(gps.speed.mph());
    Serial.println("Altitude Feet:");
    Serial.println(gps.altitude.feet());
    Serial.println("");
    }
}
