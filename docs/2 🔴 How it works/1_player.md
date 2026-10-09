# 🔴 Player

The player represents the user in space.

It is only partly driven by the Godot's physics engine:
- Its vertical position and lateral/anterior-posterior rotation are driven by physics. More precisely, the player is affected by gravity, and it has four colliders that represent the wheels, so that it matches the ground level when the ground is not flat.
- Its position and orientation on the ground plane are **not** driven by physics. This is because the whole chain (force measurement → transfer to Godot → physic simulation → player movement) would be too slow and the user would feel substantial lag. Instead, the simulator hardware sends the linear and angular speeds directly to the player, which simply translates the player on the ground plane, and rotates around the vertical axis.

The player is accessible by any module using the autoload variable `Globals.player`. Each time a scene is instantiated, `Globals.player` points to this new scene's player object. Therefore, any module can move the player, or obtain its position and orientation.
