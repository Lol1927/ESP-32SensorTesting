# 01 - LED Blink

The first and most fundamental test for the ESP-32 Super Starter Kit.  
This test verifies that the development environment is working correctly and introduces the basic concepts of digital output, resistors, and circuit wiring.

---

## Components Used

| Component | Quantity |
|-----------|----------|
| ESP-32 Dev Board | 1 |
| LED (any color) | 1 |
| 1K Resistor | 1 |
| Breadboard | 1 |
| Jumper Wires | 2 |

---

## What is D2 (GPIO2)?

D2 is a **GPIO (General Purpose Input/Output)** pin on the ESP32.  
Think of it as a controllable switch built into the ESP32.

- When the code sends `HIGH` → D2 outputs **3.3V** → LED turns **ON**
- When the code sends `LOW` → D2 outputs **0V** → LED turns **OFF**

We can control this pin directly through code, which is what makes the ESP32 so powerful.

---

## What is GND?

GND stands for **Ground (0V)**.  
Electricity always needs a start point and an end point to flow.

- **D2** = where electricity comes out (3.3V)
- **GND** = where electricity returns (0V)

Without GND, the circuit is incomplete and no current flows.  
Think of it like a water pipe: D2 is the faucet, GND is the drain.

---

## What are Jumper Wires?

Jumper wires are simply **connection cables** used on a breadboard.  
They have no special electrical function — they just connect one point to another.

---

## Why is a Resistor Needed?

Without a resistor, too much current flows through the LED, which causes it to **burn out instantly**.

The resistor **limits the total current** in the circuit to a safe level, protecting the LED.

---

## Does the Resistor Position Matter?

**No — the position does not matter.**

Because this is a **series circuit**, current flows in a single path:

```
D2 → Resistor → LED → GND
```
or
```
D2 → LED → Resistor → GND
```

In a series circuit, the current is **the same at every point**.  
So no matter where the resistor is placed, it limits the current for the entire circuit equally.

Think of it like stepping on a hose in the middle — whether you step near the faucet or near the drain, the flow of water through the entire hose is reduced.

---

## Wiring Diagram

```
ESP32                        Breadboard
──────                       ──────────

GPIO2 (D2) ──── wire ──── [Resistor 1K] ──── LED(+, long leg)
                                              LED(-, short leg) ──── wire ──── GND
```

### Pin Connections

| ESP32 Pin | Connected To |
|-----------|-------------|
| GPIO2 (D2) | One leg of the 1K resistor |
| GND | Short leg (-) of the LED |

---

## Code

```cpp
#define LED_PIN 2

void setup() {
  pinMode(LED_PIN, OUTPUT);  // Set GPIO2 as output
}

void loop() {
  digitalWrite(LED_PIN, HIGH);  // Output 3.3V → LED ON
  delay(1000);                  // Wait 1 second
  digitalWrite(LED_PIN, LOW);   // Output 0V → LED OFF
  delay(1000);                  // Wait 1 second
  // Repeat forever
}
```

### Code Explanation

| Line | What it does |
|------|-------------|
| `#define LED_PIN 2` | Names pin 2 as "LED_PIN" for readability |
| `pinMode(LED_PIN, OUTPUT)` | Tells ESP32 that GPIO2 will send signals (not receive) |
| `digitalWrite(LED_PIN, HIGH)` | Sends 3.3V to GPIO2 → LED turns ON |
| `delay(1000)` | Pauses the program for 1000ms (1 second) |
| `digitalWrite(LED_PIN, LOW)` | Sends 0V to GPIO2 → LED turns OFF |

---

## Expected Result

The LED blinks on and off every **1 second**.  
If it does, the development environment is working correctly and you are ready for the next test.
