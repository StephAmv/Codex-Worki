# Firmware Architecture

## Code Model

The firmware in `src/main.cpp` follows the Arduino execution model:

1. `setup()` runs once:
   - Configures all 12 LED pins as outputs.
   - Initializes all LEDs to LOW/OFF.
2. `loop()` runs repeatedly:
   - Reads one key event from `keypad.getKey()`.
   - If a valid key exists, dispatches behavior through `switch (key)`.
   - Sleeps for 10 ms.

## Module-Level Responsibilities

- **Key matrix definition**: `keys[4][4]` maps physical keypad positions to symbolic keys.
- **GPIO layout arrays**:
  - `ledPins[12]`
  - `rowPins[4]`
  - `colPins[4]`
- **Input driver**: `Keypad keypad = Keypad(...)` handles row/column scanning.
- **Output actions**:
  - Single LED ON actions (`'1'..'8'`, `'A'..'D'`)
  - Group ON/OFF actions (`'9'`, `'0'`, `'*'`, `'#'`)

## Behavioral Notes

- LEDs are latching in software (turn on/off explicitly and remain in that state).
- Numeric and alpha LED groups are controlled independently by different key sets.
- No network stack, interrupts, timers, or RTOS tasks are used.

## Why This Structure

The repository separates concerns cleanly:
- `src/` holds firmware source.
- `docs/` captures hardware and software design intent.
- `wokwi/` stores simulator wiring data.
- `include/` is reserved for future headers as the project grows.
