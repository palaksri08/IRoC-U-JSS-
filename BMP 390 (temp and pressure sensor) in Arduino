// Include necessary libraries
#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_BMP3XX.h>

// Create BMP390 sensor object
Adafruit_BMP3XX bmp;

void setup() {
    // Start Serial Monitor
    Serial.begin(115200);
    while (!Serial);  // Wait for Serial Monitor to open

    // Initialize I2C communication
    Wire.begin();
    delay(100);

    Serial.println("Initializing BMP390 Sensor...");

    // Initialize BMP390 with I2C
    if (!bmp.begin_I2C()) {
        Serial.println("BMP390 not detected! Check wiring.");
        while (1);  // Halt execution if sensor is not found
    }

    Serial.println("BMP390 initialized successfully!");

    // Set sensor configurations
    bmp.setTemperatureOversampling(BMP3_OVERSAMPLING_8X);
    bmp.setPressureOversampling(BMP3_OVERSAMPLING_16X);
    bmp.setIIRFilterCoeff(BMP3_IIR_FILTER_COEFF_3);
    bmp.setOutputDataRate(BMP3_ODR_50_HZ);
}

void loop() {
    // Check if sensor readings are available
    if (!bmp.performReading()) {
        Serial.println("Failed to read data from BMP390!");
        return;
    }

    // Print Pressure in Pascals
    Serial.print("Pressure: ");
    Serial.print(bmp.pressure);
    Serial.println(" Pa");

    // Print Temperature in Celsius
    Serial.print("Temperature: ");
    Serial.print(bmp.temperature);
    Serial.println(" °C");

    // Calculate Altitude (Assumes Sea Level Pressure = 1013.25 hPa)
    float altitude = bmp.readAltitude(1013.25);
    Serial.print("Altitude: ");
    Serial.print(altitude);
    Serial.println(" m");

    Serial.println("--------------------------");

    delay(1000);  // Wait before the next reading
}
