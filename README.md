# Pico W Keypad-to-LED Controller

A Raspberry Pi Pico W project that reads a 4x4 membrane keypad and drives 12 discrete LEDs.

The firmware logic maps keypad keys to LED outputs:
- Numeric keys (`1`-`8`) switch on individual blue LEDs.
- `9` turns on all blue LEDs, `0` turns them off.
- Letter keys (`A`-`D`) switch on individual red LEDs.
- `*` turns on all red LEDs, `#` turns them off.

> **Important:** The source logic is preserved exactly from the provided code. This repository focuses on structure and documentation.

## Repository Structure

```text
.
├── CMakeLists.txt
├── src/
│   └── main.cpp
├── include/
├── docs/
│   ├── architecture.md
│   └── wiring.md
└── wokwi/
    └── diagram.json
```

## Features

- 4x4 keypad matrix input (rows + columns).
- 12 independent LED channels.
- Group control shortcuts for blue and red LED banks.
- Wiring compatible with Wokwi Pico simulation and real Pico W hardware.

## Hardware Bill of Materials

Derived from `wokwi/diagram.json`:

- 1x Raspberry Pi Pico/Pico W (`wokwi-pi-pico`)
- 1x 4x4 membrane keypad (`wokwi-membrane-keypad`)
- 12x LEDs (`8 blue + 4 red`)
- 12x 220Ω resistors (LED current limiting)
- 4x 1kΩ resistors (keypad row pull-ups)
- Jumper wires

## Build / Run Options

The provided firmware uses Arduino-style APIs (`setup`, `loop`, `Keypad.h`, `digitalWrite`, etc.).

### A) Wokwi Simulation (recommended with current code)

1. Open [wokwi.com](https://wokwi.com/).
2. Create/import a Raspberry Pi Pico W project.
3. Copy `src/main.cpp` into the sketch source.
4. Replace the project `diagram.json` with `wokwi/diagram.json`.
5. Ensure `Keypad` library is enabled in Wokwi libraries.
6. Start simulation and press keypad buttons.

### B) Real Hardware (Pico W)

You can run this via an Arduino-core workflow targeting Pico W (because code is Arduino-style):

1. Install Arduino IDE or PlatformIO.
2. Install **Raspberry Pi Pico/RP2040** board package.
3. Install **Keypad** library.
4. Select board: **Raspberry Pi Pico W**.
5. Wire hardware exactly as documented in `docs/wiring.md`.
6. Upload firmware and validate behavior.

## Pico SDK Note

A `CMakeLists.txt` scaffold is included for repository consistency with C/C++ projects. The current source is **not** native Pico SDK style and would require API porting to compile directly with Pico SDK (intentionally not done to avoid logic rewrites).

## Wi-Fi / Security

- This project does **not** use Wi-Fi in its current firmware.
- No credentials are required.
- If Wi-Fi is added later, keep credentials in a local config file excluded by `.gitignore`.

> Note: `wokwi/diagram.json` is a compact checked-in scaffold; use the full provided diagram content when recreating the exact visual layout.
