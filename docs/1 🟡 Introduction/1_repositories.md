# 🟢 GitHub Repositories

The different components of the WheelSims project are hosted on a number of repositories.

## Main repository

The main repository is the [wheelsims](https://github.com/LabMOSA/wheelsims) repository. It includes all the Godot code that connects to the simulator hardware, simulates and renders the different scenes and games. It also implements a control GUI for the clinicians and technicians.

## Secondary repositories

### Documentation

The [wheelsims_doc](https://github.com/LabMOSA/wheelsims_doc) repository contains this website's code as markdown files and images.

### Real-time analysis

The [wheelsims_analysis](https://github.com/LabMOSA/wheelsims_analysis) repository contains Python code that is executed on request by Godot (e.g., biofeedback calculation, data logging from multiple instruments). If enabled in the Godot project, an instance of Python is launched with on game start (main.py), and requests and answers are sent asynchronously (so that calculation time can be long without blocking the main Godot game) between Godot and Python via a local UDP connection.

### Artwork

The [wheelsims_artwork](https://github.com/LabMOSA/wheelsims_artwork) repository contains source Blender files and textures, used to generate the assets contained in the main repository.

## Simulator-specific repositories

### CRIR Simulator Haptics

The [wheelsims_haptics](https://github.com/LabMOSA/wheelsims_haptics) repository contains the Simulink files run by the CRIR Simulator's onboard SpeedGoat computer. It receives force data from external hardware, models the dynamics of a wheelchair-user system, and controls the speed of the rollers using two feedback loops. It also communicates data with the main Godot project using UDP connections:
- Simulink to Godot: current roller speed, used to move the player in the scene;
- Godot to Simulink: mass and rolling resistance of the dynamic model to simulate.

### MiWe Firmware

The [wheelsims_miwe_firmware](https://github.com/LabMOSA/wheelsims_miwe_firmware) repository contains the Arduino code for the MiWe simulator. It communicates the roller speed to the main Godot project using a USB-Serial connection.
