# PLC Sorting Cell — SMC Demo (CODESYS)
A compact PLC project for **sorting workpieces** by **material** (metal/non‑metal) and **colour/size** (white/blue, large/small). The system uses a dispenser, press (with analogue stroke feedback), sensors, a turntable, and an evacuation manipulator with a vacuum pad.

# Prerequisites.
Known how to use CODESYS and Simumatik.

## Highlights
- **Modular function blocks**: Output Controller, Dispenser, Press (size), Colour Identifier, Type Identifier, Turntable, Pick‑and‑Drop, System Cycle, Reset.
- **Safety state machine**: `START_UP → RESETTING → IDLE → RUNNING → HALTING → HALT`, plus `WARNING` and `FAULT` (EB).
- **Deterministic timing**: Non‑retriggerable windows; inter‑module delays; conflict guards.
- **Whitelist‑based sorting**: Only allowed types are evacuated; others continue on the turntable.

## System At‑a‑Glance
- **Actuators**: A1/A2 (dispenser grippers), B (press, stroke reading), C & D_1 (turntable), E & F (manipulator), Vacuum pad. 
- **Sensors**: Inductive (metallic/grey), Diffuse (dark/blue). Default white when neither active. 
- **Workpieces**: White, Blue (non‑metal); Grey (metal). Each Large/Small. 

## I/O Quick Map (example)
- **Digital inputs (IW0, bytes inverted)**: `Start`, `Stop`, `Auto/Manual`, `Reset`, `Inductive`, `Emergency`, `Diffuse`.
- **Analogue input**: `IW200` — press stroke (0–10 V typical range).
- **Digital outputs (QW0, bytes inverted)**: Dispenser, Press, Turntable (C, D_1), Manipulator (E/F), Vacuum ON/OFF.
- **Analogue output**: `QW200` for beacon (or `QB200` if using 8‑bit pattern) — keep consistent.

## Demo Tasks (placeholders)
Replace with your links and acceptance checks. Task 4 wording corrected to *small blue*.

1. **Sorting metallic objects** — *(insert video link)*  
2. **Sorting non‑metallic objects** — *(insert video link)*  
3. **Sorting large blue objects** — *(insert video link)*  
4. **Sorting small blue objects** — *(insert video link)*  
5. **Sorting large metallic objects** — *(insert video link)*  
6. **Sorting small metallic objects** — *(insert video link)*  
7. **Sorting small white objects** — *(insert video link)*  
8. **Sorting large white objects** — *(insert video link)*  

## Quick Start
1. Open the project **PLC Challenge - SMC Demo.project** in **CODESYS 3.5+**, and connect to the gateway.
3. Login and download the code into PLC.
3. Open Simumatik, login/signin an account, load the project name "PLC Challenge: SMC Demo" into a workspace, then configure PLC to use OPC UA client protocol. Connect to the gateway and run the simulation.
4. Run the PLC program in CODESYS (F5).
5. Open GVL, set TRUE for workpieces that need to pickup (WP_WHITE_LARGE, WP_BLUE_LARGE, WP_GRAY_LARGE, WP_WHITE_SMALL, WP_BLUE_SMALL, WP_GRAY_SMALL).
5. Reset → **RESETTING** → **IDLE** → Start to run. Stop → **HALTING** → **HALT**. EB ⇒ **FAULT**.
