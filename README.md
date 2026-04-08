# Tank Level Control with HMI

PLC: Siemens S7-1500 (CPU 1511-1 PN)
HMI: Siemens KTP700 Basic PN
Software: TIA Portal V21
Language: Ladder (LAD) + WinCC Basic

## Description
Tank level control system with HMI visualization. Implements 
automatic and manual pump control, drain valve, emergency stop, 
level simulation and real-time HMI monitoring.

## Tag Table

Pump — Bool — %Q0.0 — Fill pump output
Drain_Valve — Bool — %Q0.1 — Drain valve output
Alarm_Light — Bool — %Q0.2 — Alarm indicator
Level_Low — Bool — %I0.0 — Low level sensor
Level_High — Bool — %I0.1 — High level sensor
Emergency_Stop — Bool — %I0.2 — Emergency stop input
Auto_Mode — Bool — %M0.0 — Automatic mode flag
Manual_Mode — Bool — %M0.1 — Manual mode flag
Tank_Level — Int — %MW0 — Tank level value (0-100)
Manual_Pump_On — Bool — %M0.2 — Manual pump HMI button

## Program Logic

Network 1 — Auto mode pump control
Network 2 — Drain valve control
Network 3 — Emergency alarm
Network 4 — Manual mode pump control
Network 5 — Tank level simulation (ADD/SUB)

## HMI Screen Elements

- Tank level bar — connected to Tank_Level (0-100)
- Start Pump button — sets Manual_Pump_On
- Stop Pump button — resets Manual_Pump_On
- Alarm indicator — circle turns red when Emergency_Stop active
- Mode display — shows AUTO or MANUAL mode
- Numeric display — shows exact Tank_Level value

## System Operation
- AUTO MODE: Pump starts when level is low, stops when level is high
- MANUAL MODE: Operator controls pump from HMI buttons
- Emergency Stop: Stops pump and drain valve, activates alarm
- Tank Level: Increases +1 per scan when pump active, -1 when draining

## Network Configuration
- PLC_1: 192.168.0.1
- HMI_1: 192.168.0.2
- Protocol: PROFINET (PN/IE)

## Software Required
- TIA Portal V17 or higher
- SIMATIC S7-PLCSIM V21 for simulation
