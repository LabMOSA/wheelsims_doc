# Hardware overview

The WheelSims system combines:

- **Haptics** - so that the user feels realistic forces at the wheels
- **Virtual Reality** - so that the user feels where they navigate
- **Incline Platform** - so that the user feels the difference between ascending, descending or crossing a slope.

These three systems are independent. For example, it is not required to have an haptic system to navigate in virtual reality. They are complementary, they add realism to the simulation.

This figure illustrates the data flow between the different systems:


```mermaid
flowchart TD

force_sensor["<b>Force Sensor</b><br/>(AMTI force cell)"]
haptics["<b>Haptics System</b><br/>(Simulink Real-Time)"]
unity["<b>Virtual Reality System</b><br/>(Godot)"]
motors["<b>Motors</b><br/>(attached to rollers)"]
rollers["<b>Rollers</b>"]
projectors["<b>Projectors</b>"]
dbox["<b>Incline platform</b><br/>(D-Box System)"]

force_sensor -->|Force| haptics
haptics -->|Torque command| motors
motors --> rollers
rollers -->|Speed| haptics
rollers -->|Speed| unity
unity -->|Visual| projectors
unity -->|Incline| dbox
unity -->|Rolling Resistance| haptics

```
