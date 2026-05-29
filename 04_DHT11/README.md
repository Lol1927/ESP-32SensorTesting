# 04 - DHT11 Temperature & Humidity Sensor

## What is the DHT11?

The DHT11 is a digital sensor that measures both **temperature** and **humidity** at the same time.  
It has a built-in microcontroller that processes the raw sensor data and sends it digitally to the ESP32.

---

## How Does It Detect Temperature?

The DHT11 uses a **NTC Thermistor** (Negative Temperature Coefficient resistor) inside.

```
Temperature UP  →  Resistance DOWN  →  Voltage changes  →  Converted to °C
Temperature DOWN →  Resistance UP   →  Voltage changes  →  Converted to °C
```

- NTC means: as temperature **rises**, resistance **falls**
- The built-in chip measures this resistance and calculates the temperature value
- Measurement range: **0°C ~ 50°C**

---

## How Does It Detect Humidity?

The DHT11 uses a **Capacitive Humidity Sensor** inside.

```
         Electrode
            │
  ┌─────────┴─────────┐
  │  moisture-absorbing│  ← humidity-sensitive material
  │      material      │
  └─────────┬─────────┘
            │
         Electrode
```

- The moisture-absorbing material sits between two electrodes
- When humidity is **high** → more water molecules absorbed → **capacitance increases**
- When humidity is **low** → fewer water molecules → **capacitance decreases**
- The built-in chip measures this capacitance change and calculates the humidity percentage
- Measurement range: **20% ~ 80% RH**

---

## Wiring

| DHT11 Module Pin | ESP32 Pin |
|-----------------|-----------|
| S (Signal) | D15 (GPIO15) |
| VCC (+) | 3V3 |
| GND (-) | GND |

---

## Code Explanation

```cpp
#include "DHT.h"
```
Loads the Adafruit DHT library — handles all communication with the sensor.

```cpp
#define DHT_PIN 15
#define DHT_TYPE DHT11
```
Sets the data pin (GPIO15) and sensor type.

```cpp
DHT dht(DHT_PIN, DHT_TYPE);
```
Creates a DHT object using the pin and type defined above.

```cpp
dht.begin();
```
Initializes the sensor on startup.

```cpp
float humidity = dht.readHumidity();
float temperature = dht.readTemperature();
```
Reads the current humidity (%) and temperature (°C) from the sensor.

```cpp
if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
}
```
`isnan()` checks if the value is invalid (not a number).  
If the sensor fails to respond, it prints an error and skips the rest of the loop.

```cpp
delay(2000);
```
DHT11 needs at least **2 seconds** between readings — it cannot measure faster than this.

---

## Serial Monitor Output

```
Temperature: 25.00 C  |  Humidity: 45.00 %
Temperature: 25.00 C  |  Humidity: 45.00 %
```

Baud rate: **115200**
