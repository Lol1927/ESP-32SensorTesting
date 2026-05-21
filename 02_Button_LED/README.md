# 02 - Button + LED

Press the button to turn the LED on. Release to turn it off.  
This test introduces digital input reading and the internal pull-up resistor.

---

## Components Used

| Component | Quantity |
|-----------|----------|
| ESP-32 Dev Board | 1 |
| LED (any color) | 1 |
| 1K Resistor | 1 |
| Push Button | 1 |
| Breadboard | 1 |
| Jumper Wires | 3 |

---

## Wiring

```
ESP32 GPIO2 → Resistor (1K) → LED(+) → LED(-) → GND
ESP32 GPIO4 → Button → GND
```

### Pin Connections

| ESP32 Pin | Connected To |
|-----------|-------------|
| GPIO2 (D2) | 1K resistor → LED long leg (+) |
| GND | LED short leg (-) and one side of button |
| GPIO4 (D4) | Other side of button |

---

## What is INPUT_PULLUP?

Normally a button needs an external resistor to work correctly.  
`INPUT_PULLUP` activates a resistor built inside the ESP32, so no external resistor is needed for the button.

```
Button NOT pressed → GPIO4 internally pulled to 3.3V → reads HIGH → LED OFF
Button pressed     → GPIO4 connects to GND → reads LOW → LED ON
```

---

## Code

```cpp
#define LED_PIN    2
#define BUTTON_PIN 4

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {
  if (digitalRead(BUTTON_PIN) == LOW) {
    digitalWrite(LED_PIN, HIGH);  // Button pressed → LED ON
  } else {
    digitalWrite(LED_PIN, LOW);   // Button released → LED OFF
  }
}
```

---

## Expected Result

- Button pressed → LED turns ON
- Button released → LED turns OFF
