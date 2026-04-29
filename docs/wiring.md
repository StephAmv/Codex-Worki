# Wiring (Raspberry Pi Pico W)

## Overview

The design contains:
- One 4x4 matrix keypad (R1-R4, C1-C4)
- 12 LEDs with dedicated GPIO outputs
- 220Ω series resistor per LED
- 1kΩ pull-up resistor on each keypad row line to 3.3V

## GPIO Pin Mapping

### Keypad Lines

| Keypad Signal | Pico W GPIO | Notes |
|---|---:|---|
| C1 | GP19 | Column input/output via Keypad library |
| C2 | GP18 | Column input/output via Keypad library |
| C3 | GP17 | Column input/output via Keypad library |
| C4 | GP16 | Column input/output via Keypad library |
| R1 | GP26 | Row line with external 1kΩ pull-up to 3V3 |
| R2 | GP22 | Row line with external 1kΩ pull-up to 3V3 |
| R3 | GP21 | Row line with external 1kΩ pull-up to 3V3 |
| R4 | GP20 | Row line with external 1kΩ pull-up to 3V3 |

### LED Outputs

| LED Label | Pico W GPIO | Color | Behavior |
|---|---:|---|---|
| 1 | GP11 | Blue | ON when key `1` pressed |
| 2 | GP10 | Blue | ON when key `2` pressed |
| 3 | GP9 | Blue | ON when key `3` pressed |
| 4 | GP8 | Blue | ON when key `4` pressed |
| 5 | GP7 | Blue | ON when key `5` pressed |
| 6 | GP6 | Blue | ON when key `6` pressed |
| 7 | GP5 | Blue | ON when key `7` pressed |
| 8 | GP4 | Blue | ON when key `8` pressed |
| A | GP3 | Red | ON when key `A` pressed |
| B | GP2 | Red | ON when key `B` pressed |
| C | GP28 | Red | ON when key `C` pressed |
| D | GP27 | Red | ON when key `D` pressed |

## Power and Ground

- All LED cathodes go to common GND.
- Each LED anode connects to its GPIO through a 220Ω resistor.
- Keypad row pull-up network ties rows R1-R4 to 3V3 using 1kΩ resistors.

## Connection Assumptions

From the provided `diagram.json`, the project uses:
- `wokwi-pi-pico` part (electrically compatible mapping for Pico W GPIO usage here)
- External pull-ups on rows (not strictly required by all keypad scans, but retained as designed)
