# 🚦 Traffic Light System – Overview & Implementation Guide

## 🎨 Visual Components
### ➤ Light Materials
- **Lights ON**: Materials with **emission enabled** for glowing effect
- **Lights OFF**: Other materials almost similar but with **emission disabled**
- **Pedestrian Symbols**: Two sprites for the orange hand and the character sprite
- **Pedestrian Counter**: implemented using a MeshInstance3D to display the countdown.
---

## ⚙️ Script Architecture
### 🚦 Traffic Light Behavior (`traffic_light` script)
Each individual traffic light includes:
- **State Management**: Controls light sequence using `LightState` enum: `{ RED, GREEN, YELLOW }`
- **Virtual Obstacle**: Movable collision object that **blocks or allows** car passage
- **Direction Property**: Defines orientation (`NS` or `EW`)

### 🚶 Pedestrian Traffic Light Behavior (`pedestrian_traffic_light` script)
Each individual traffic light includes:
- **Timer Node**: `blink_timer` controls the blinking of the orange hand symbol.
- **Virtual Obstacle**: Movable collision object that **blocks or allows** pedestrian passage
- **Direction Property**: Defines orientation (`NS` or `EW`)

### 🏘️ Intersection Controller (`traffic_light_manager` script)
- **Centralized Control**: Manages multiple traffic lights (both types) at an intersection
- **Direction-Based Logic**: Activates lights based on their **direction property**
- **Automatic Cycling**: Switches active direction every `green_light_duration` + `yellow_light_duration` seconds
- **Pedestrian light handling**: `walk_man_ratio` defines the duration of the walking symbol relative to the cycle.
- **Configurable Timing**: `green_light_duration` can be **adjusted in the Inspector**

---

## 🔄 System Flow
1. `traffic_light_manager` determines which direction should have car traffic lights and pedestrian traffic lights
4. Individual `traffic_light` and  `pedestrian_traffic_light` scripts respond by:
  - Changing light colors
  - Moving virtual obstacles to block/unblock traffic
5. Process repeats every `green_light_duration` + `yellow_light_duration` seconds

---

# 🚗 Moving Objects System

This system handles the behavior of moving entities such as **cars** and **pedestrians**. Both use path3d and pathFollow with different scripts.

### Movement

- Cars and pedestrians follow **Path3D** (predefined paths).
- Once a car reaches the end of the path, it **respawns** at the beginning.

### Triggers 

Cars use several triggers placed in front of them to observe their environment. These triggers:

- Are positioned using their **Node’s Transform**.
- Can **follow the path** or **stay in front** of the object.
- Pedestrians only use one in front of them..

#### Car Triggers Path Following Behavior

- If the Trigger is in the list `TriggersOnCurve`, it **follows the path** and its position adjusts based on car speed.
- If the Trigger is in **neither list**, it remains fixed relative to the car and **is not influenced** by speed

### Vertical Position Correction

- Two raycasts up and down are used to ajdust the vertical position of moving objects. 
