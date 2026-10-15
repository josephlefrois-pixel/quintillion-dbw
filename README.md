# Quintillion DBW (Drive-By-Wire) 🏎️⚡

## The Mission
The Quintillion is a street-legal, enclosed, three-wheeled hybrid autocycle (reverse trike). 
The core mission of this project is to eliminate the severe cost barriers of modern commuting by replacing heavy automotive construction with a lightweight **4130 chromoly steel spaceframe** and replacing expensive, heavy mechanical linkages with edge-compute software.

By targeting a sub-600 lb curb weight and an aggressive $18k–$24k MSRP, the Quintillion bridges the gap between the affordability of a motorcycle and the enclosed safety of a commuter car.

## The Hardware Constraints (The Physical Problems)
To achieve radical cost reduction and weight savings, the Quintillion utilizes a **Through-The-Road (TTR) Parallel Hybrid** setup:
*   **Front Axle:** Dual 72V electric hub motors (immediate torque).
*   **Rear Axle:** Single internal combustion engine (e.g., KTM 390 / Minarelli) for continuous range.
*   **Chassis:** 3-wheeled tadpole layout (yaw-sensitive at high speeds).

Because there is no physical driveshaft connecting the front and rear wheels, the physical hardware is inherently unsynchronized and prone to snap-oversteer or traction loss.

## The Software Solution (This Repository)
We cannot fix these physical desynchronization problems with heavier mechanical parts without ruining the startup cost model. Instead, we fix them with silicon. 

This repository contains the C++20 Drive-By-Wire (DBW) architecture running on an onboard **Nvidia Jetson** edge-compute module. The software acts as the digital nervous system, solving the hardware constraints in real-time:

1.  **Active Torque Blending (`TorqueBlender`):** Dynamically monitors throttle input to perfectly synchronize the immediate electric punch of the front wheels with the delayed mechanical ramp-up of the rear engine.
2.  **Digital ABS & Traction Control:** Reads wheel speed sensors at high frequencies to detect micro-slips, feathering the electric motors and electronic braking actuators to prevent the chromoly frame from losing lateral grip.
3.  **Dynamic Ackermann & Yaw Stabilization:** Fuses data from 77GHz mmWave radar and 6-axis IMUs to constantly adjust steering angles digitally, taming the pendulum effect inherent in three-wheeled vehicles.

## Tech Stack
*   **Language:** C++20
*   **Build System:** CMake (FetchContent)
*   **Math/Kinematics:** Eigen3
*   **Testing:** Google Test (gtest)
