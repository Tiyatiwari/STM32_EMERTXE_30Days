# EV Simulation & Core Physics Engine (STM32)

A real-time embedded firmware application built for the **STM32F103C8T6 microcontroller** (ARM Cortex-M3). This project forms the core hardware-in-the-loop (HIL) physics backend for a multi-stage EV & ADAS Dashboard project, running a physics-based simulation loop at 100 Hz ($dt = 0.01\text{ s}$).

## 📸 Simulation Telemetry Verification
Below is the live execution capture from PicSimLab showing calibrated data strings streaming successfully over UART:



## 🛠️ Implemented Core Features

* **Lumped Inertia Speed Modeling:** Computes live vehicle velocity using real-time Euler Integration. It calculates aerodynamic drag force ($F_{drag} = v \times \text{coeff}$) and balances it against active motor torque to determine dynamic acceleration.
* **State of Charge (SOC) Energy Integration:** Tracks battery depletion by calculating total power demand. It combines active mechanical work load ($P_{mech} = \tau \times \omega$) with motor copper winding thermal losses ($I^2R$ heating) to prevent zero-drain states at a standstill.
* **Multi-Drive Mode Range Prediction:** Real-time distance-to-empty ($km$) calculation that dynamically updates based on the battery percentage and active driving profile efficiency penalties ($\eta$ factor) for **ECO**, **NORMAL**, and **SPORT** modes.
* **Regenerative Braking Energy Recovery:** Monitors the brake pedal via ADC. Once past a 5% deadzone threshold, it applies scaled negative torque to slow down the vehicle and generate negative kilowatts, actively recharging the battery capacity (`SOC`).
* **Thermal Management Simulation:** A basic thermodynamic block that handles motor heat warm-up based on a 5% system loss coefficient, balanced against a linear ambient cooling model.

## 📁 Firmware Architecture
* `Core/Src/ev_control.c`: Core modular physics processing, mathematical integration equations, and state update algorithms.
* `Core/Src/main.c`: Hardware clock settings, peripheral initializations, and main sequential execution loop.
* `Core/Inc/ev_control.h`: Data structures (`EV_HandleTypeDef`), driving mode type definitions, and exposed function hooks.
* `Core/Inc/common.h`: Global configuration macros, physical limits, and vehicle parameter constants.
