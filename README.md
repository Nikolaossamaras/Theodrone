# Theodrone

Theodrone is a small quadcopter I'm building myself, roughly 130mm x 130mm x 30mm. It's my first drone project.

## What it is

A basic quadcopter — 4 motors, a custom frame I designed and printed myself, and a custom PCB that handles power, charging, and motor control. The board is built around an ESP32-WROOM-32, an MPU-6050 for orientation sensing, a TP4056 for LiPo charging, and a CH340C for USB communication with the ESP32 during flashing/debugging.

## Why I built it

I originally wanted to build a thermal drone, but after looking at the cost of thermal cameras and displays, I decided to start with a basic drone first, since I'd never built one before. This project is meant to get the fundamentals down — frame, power system, motor control, sensing — before adding anything more complicated.

## How it works

The ESP32 is the main controller. It reads orientation data from the MPU-6050 over I2C and controls each motor through its own low-side NMOS switch (AO3400A), one per motor, so each motor circuit can be enabled or disabled independently by a GPIO pin. Power comes from a single-cell LiPo battery, charged through the TP4056 over USB-C. The CH340C provides a USB-to-serial bridge so the board can be flashed and debugged over the same USB-C port.

## Repo contents

- **Cad/** — Fusion 360 frame design (`drone.f3z`)
- **pcb_files/** — KiCad project files, schematic, Gerbers, and the component placement/position file
- **dronev2_BOM.csv** — bill of materials with footprints and part numbers for ordering components

## Current status

The board design is done and the Gerbers are ready to send to a fab. A few nets on the current revision aren't routed and are being connected by hand with jumper wires after assembly rather than in copper — this is noted so it's clear the board as fabricated isn't 100% routed on its own. The exact ESP32-WROOM-32 module variant should be double-checked against the footprint in the schematic before ordering parts, since some variants (particularly -32U) use a different antenna setup and won't fit.

## Building it

1. Order the bare PCB using the Gerber files in `pcb_files/`.
2. Buy the components listed in `dronev2_BOM.csv`.
3. Hand-solder the board — most parts are fine with a regular soldering iron, but the ESP32 module and the MPU-6050 (QFN package) are much easier with solder paste and a hot air rework tool, since their pads aren't accessible from the side.
4. Add the manual jumper wires for the unrouted nets mentioned above.
5. Check continuity with a multimeter before powering it on for the first time.
## Schematic 
<img width="1139" height="775" alt="Screenshot 2026-08-18 190407" src="https://github.com/user-attachments/assets/afeee9d9-ad4a-46eb-a4da-45cfe7c571a0" />

## PCB Preview
<img width="813" height="756" alt="image" src="https://github.com/user-attachments/assets/3e815508-b930-491d-a348-8a3f3f4e2c00" />

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
