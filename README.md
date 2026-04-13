# Drone Navigation System (Unreal Engine 5)

## Overview

This project implements a flyable drone system in Unreal Engine 5 using Blueprints. The system supports smooth takeoff and landing, directional movement, and altitude control, along with a simple test environment for navigation.

The focus of this project was building a clean, modular control system with clear state transitions and exposing functionality that can be called externally.

---

## Demo Controls

* **F** → Toggle drone state (required to enable movement)
* **W / A / S / D** → Horizontal movement
* **Q / E** → Vertical movement
* **Mouse** → Yaw rotation

### Control Flow

* Press **F** to initiate takeoff and enable movement
* While flying, use movement controls to navigate
* Press **F** again to initiate landing
* After landing, the drone remains in a grounded/landing state and cannot take off again within the same session

---

## Project Setup

1. Open the project in **Unreal Engine 5.3+**
2. If the main level is not automatically loaded:
   - Navigate to the **Content Browser → Levels folder**
   - Open the level named **Level**
3. Press **Play**
4. Use **F** to begin controlling the drone

---

## System Design

### Drone State System

The drone operates using a simple state-based system:

* **Grounded** → Drone is landed and movement is disabled
* **Flying** → Full directional control enabled
* **Landing** → Controlled descent until grounded

State transitions are triggered via the **F key**, ensuring clear and controlled switching between modes.

---

### Movement System

Movement is implemented using velocity-based updates applied every frame. The system supports:

* Forward / backward and lateral motion
* Vertical ascent and descent
* Yaw rotation via mouse input

Collision-aware movement is enabled using sweep-based translation to ensure the drone interacts correctly with the environment.

---

### Landing Logic

Landing is handled through a controlled descent mechanism:

* Gradual reduction in altitude
* Automatic stop upon reaching ground
* Movement disabled once grounded

This ensures stable and predictable landing behavior.

---

## Blueprint-Callable Functions

The following functions are exposed for external control:

### `FlyTo(X, Y, Z)`

Moves the drone toward a target world position.

Internally, this sets a target location and computes a direction vector from the current position to the goal. The drone updates its velocity each frame to move toward the target until it is within a small threshold distance, at which point movement stops.

### How to Test

This function can be tested by calling it on **Event BeginPlay** in the Drone Blueprint or Level Blueprint with a target world position (X, Y, Z). When the simulation starts, the drone will automatically move toward the specified location.

---

### `GetDroneState()`

Returns the current state of the drone:

* Grounded
* Flying
* Landing

This reads from the internal state variable that governs movement and input handling, which is updated based on takeoff and landing transitions.

### How to Test

This can be tested by calling the function and printing the result using a **Print String** node. For example, bind it to a key press or call it during Tick to observe state transitions in real time.

---

### `GetAltitude()`

Returns the current height of the drone above ground.

This is computed using the drone’s world Z position relative to the ground plane, providing a simple measure of vertical displacement.

### How to Test

This can be tested by calling the function and printing the output using a **Print String** node while flying the drone. The value should increase as the drone ascends and decrease during descent.

---

## Level Design

The test level is a minimal drone navigation environment designed for clarity and functionality.

It includes:

* A flat ground area
* A dedicated landing pad
* A structured obstacle course composed of high walls and vertical pillars

The landing pad is positioned at the far end of the level and is partially concealed behind a narrow opening between two large wall obstacles, encouraging controlled navigation through the environment.

The layout is intentionally simple to highlight control precision and system behavior rather than visual complexity.

---

## Assets

* Drone model: https://sketchfab.com/3d-models/chatgptxtripo-fpv-drone-dbc45c76dd474432a52f06b99f21d526#download

---

## Screenshots

![WhatsApp Image 2026-04-13 at 1 06 55 AM](https://github.com/user-attachments/assets/bc363e6d-1846-4424-92f0-6072f2415b84)
![WhatsApp Image 2026-04-13 at 1 07 15 AM](https://github.com/user-attachments/assets/d87c2843-e36d-40b6-8255-34a7e64cd18c)
![WhatsApp Image 2026-04-13 at 1 07 32 AM](https://github.com/user-attachments/assets/4cbacae3-ed43-4bcf-96b8-9d15b91b88d3)
![WhatsApp Image 2026-04-13 at 1 08 02 AM](https://github.com/user-attachments/assets/ac2925c1-1312-4e88-add0-b2707b66ed35)
![WhatsApp Image 2026-04-13 at 1 09 30 AM](https://github.com/user-attachments/assets/2c5c3b0a-e8af-4b4f-810f-09c692137655)






---
