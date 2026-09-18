#include <WiFi.h>
#include <Wire.h>
#include <Adafruit_INA219.h>
#include <ThingSpeak.h>

const char* WIFI_SSID = "YOUR_WIFI_NAME";
const char* WIFI_PASSWORD = "YOUR_WIFI_PASSWORD";
unsigned long CHANNEL_ID = YOUR_CHANNEL_ID;
const char* API_KEY = "YOUR_WRITE_API_KEY";

WiFiClient client;
Adafruit_INA219 ina219;
unsigned long lastUpload = 0, lastEnergyTime = 0;
const unsigned long uploadInterval = 15000;
double energyWh = 0.0;

void setup() {
  Serial.begin(115200);
  Wire.begin();

  if (!ina219.begin()) {
    Serial.println("INA219 not detected. Check wiring.");
    while (true) delay(1000);
  }

  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  Serial.print("Connecting to Wi-Fi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWi-Fi connected!");

  ThingSpeak.begin(client);
  lastEnergyTime = millis();
}

void loop() {
  float voltage = ina219.getBusVoltage_V();
  float currentA = ina219.getCurrent_mA() / 1000.0;
  float powerW = voltage * currentA;

  unsigned long now = millis();
  energyWh += powerW * ((now - lastEnergyTime) / 3600000.0);
  lastEnergyTime = now;

  Serial.printf("Voltage: %.2f V | Current: %.3f A | Power: %.2f W | Energy: %.4f Wh\n",
                voltage, currentA, powerW, energyWh);

  if (millis() - lastUpload >= uploadInterval &&
      WiFi.status() == WL_CONNECTED) {
    ThingSpeak.setField(1, voltage);
    ThingSpeak.setField(2, currentA);
    ThingSpeak.setField(3, powerW);
    ThingSpeak.setField(4, energyWh);

    int result = ThingSpeak.writeFields(CHANNEL_ID, API_KEY);
    Serial.printf("ThingSpeak result: %d\n", result);
    lastUpload = millis();
  }

  delay(1000);
}

/*
SAFETY: This project is for LOW-VOLTAGE DC demonstration only.
Do NOT connect ESP32/INA219 directly to 230 V AC mains.
*/
