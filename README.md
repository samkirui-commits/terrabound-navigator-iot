/* * TerraBound Smart Hub v1.0 
 * Connects the Bamboo Tower to the TerraBound Navigator App
 */

#define BLYNK_TEMPLATE_ID "Your_Template_ID"
#define BLYNK_DEVICE_NAME "TerraBound_Hub"
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

// Your WiFi credentials
char auth[] = "Your_Blynk_Auth_Token";
char ssid[] = "Your_WiFi_Name";
char pass[] = "Your_WiFi_Password";

// Pins for sensors and pump
const int pHSensorPin = 34;
const int waterLevelPin = 35;
const int pumpRelayPin = 13;

void setup() {
  pinMode(pumpRelayPin, OUTPUT);
  Blynk.begin(auth, ssid, pass);
}

void loop() {
  Blynk.run();
  
  // Read pH Value
  int rawPH = analogRead(pHSensorPin);
  float voltage = rawPH * (3.3 / 4095.0);
  float phValue = 3.5 * voltage; // Simple calibration logic
  
  // Read Water Level
  int waterLevel = analogRead(waterLevelPin);
  
  // Send data to the TerraBound App
  Blynk.virtualWrite(V1, phValue);     // Gauge in App
  Blynk.virtualWrite(V2, waterLevel);   // Level in App
  
  delay(2000); // Send data every 2 seconds
}

// Button in App to control the pump
BLYNK_WRITE(V3) {
  int relayStatus = param.asInt();
  digitalWrite(pumpRelayPin, relayStatus);
}
