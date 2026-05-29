# 03 - Potentiometer (Analog Input)

## What is a Potentiometer?

A potentiometer is a variable resistor with a rotatable knob.  
When you turn the knob, the resistance changes — and so does the output voltage.  
It works like a volume knob: turn it to control how much signal comes through.

The B103 potentiometer used in this kit has a resistance range of **0Ω to 10,000Ω (10KΩ)**.

---

## Legs and Their Roles

```
      [ Knob ]
         |
  ┌──────┴──────┐
  │             │
Left          Right
(3V3)         (GND)
       ↑
     Middle
    (Signal)
```

| Leg | Connected To | Role |
|-----|-------------|------|
| Left | 3V3 (3.3V) | Power input — supplies voltage to the potentiometer |
| Middle (Wiper) | D2 (GPIO2) | Signal output — voltage changes as you turn the knob |
| Right | GND | Ground — completes the circuit |

---

## How It Works

The potentiometer acts as a **voltage divider**.  
The middle leg (wiper) reads a voltage between 0V and 3.3V depending on the knob position.

| Knob Position | Voltage at Middle Leg | ADC Value |
|--------------|----------------------|-----------|
| Turned fully to GND side | 0.00 V | 0 |
| Middle | 1.65 V | ~2048 |
| Turned fully to 3V3 side | 3.30 V | 4095 |

The ESP32 ADC converts this voltage into a number from **0 to 4095** (12-bit resolution).

---

## Wiring

| Potentiometer Leg | ESP32 Pin |
|-------------------|-----------|
| Left | 3V3 |
| Middle (Wiper) | D2 (GPIO2) |
| Right | GND |
