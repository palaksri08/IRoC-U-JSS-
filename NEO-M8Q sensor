// Include required libraries
#include <Wire.h>                  // I2C communication
#include <SparkFun_u-blox_GNSS_Arduino_Library.h> // u-blox GNSS Library

// Create GNSS sensor object
SFE_UBLOX_GNSS myGPS;

void setup() {
    // Start Serial Monitor
    Serial.begin(115200);
    while (!Serial);  // Wait for serial connection

    // Initialize I2C
    Wire.begin();
    delay(100);

    Serial.println("Initializing NEO-M8Q GPS...");

    // Initialize GPS module
    if (!myGPS.begin()) {
        Serial.println("NEO-M8Q not detected! Check wiring.");
        while (1);  // Halt execution if sensor is not found
    }

    Serial.println("NEO-M8Q GPS initialized successfully!");

    // Configure GPS update rate (1Hz)
    myGPS.setNavigationFrequency(1);
}

void loop() {
    // Check if new GPS data is available
    if (myGPS.getPVT()) {
        // Read Latitude and Longitude
        Serial.print("Latitude: ");
        Serial.print(myGPS.getLatitude() / 10000000.0, 7);  // Convert to decimal degrees
        Serial.print("°, Longitude: ");
        Serial.print(myGPS.getLongitude() / 10000000.0, 7); // Convert to decimal degrees
        Serial.println("°");

        // Read Altitude (meters)
        Serial.print("Altitude: ");
        Serial.print(myGPS.getAltitude() / 1000.0, 2);  // Convert to meters
        Serial.println(" m");

        // Read Speed (m/s)
        Serial.print("Speed: ");
        Serial.print(myGPS.getGroundSpeed() / 1000.0, 2);
        Serial.println(" m/s");

        // Read Fix Type
        Serial.print("Fix Type: ");
        Serial.println(myGPS.getFixType()); // 0 = No fix, 2 = 2D, 3 = 3D

        Serial.println("--------------------------");
    } else {
        Serial.println("Waiting for GPS fix...");
    }

    delay(1000);  // Wait before next reading
}
