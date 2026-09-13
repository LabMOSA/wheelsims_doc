# Developing new static objects

In this guide, we will create a static object that is an orange cone, that can then be added to any new scene.

## Designing the object in Blender

Creating static objects is very similar to [creating terrains](docs/2%20Software/3%20Developing%20new%20static%20scenes/2_developing_new_terrains.md).

First create these folders in the `wheelsims_artwork` repository:
- `objects/sports` that will contain the source Blender files for sport-related objects such as our cone;
- `objects/sports/textures` that will contain the jpg/png files used as textures (we don't have a texture for our cone, but other objects may have)

and these folders in the `wheelsims` repository:
- `src/objects/sports/gltf` that will contain the exported sport-related objects.

Remember that all folder and file names must be in `snake_case` (lower case with words separated by underscores) according to the [file name conventions](docs/2%20Software/2%20Developing%20Wheelsims/2_conventions.md).

In Blender, create a similar object and save it as `objects/sports/cone.blend`. All units are in meters. For optimization, try to limit the number of polygons in an object.

![](docs/2%20Software/3%20Developing%20new%20static%20scenes/developing_new_static_objects_blender.png)

If textures are needed, put them in the `objects/sports/textures` subfolder and use them in your Blender materials.

## Exporting to glTF

Export the same way you exported a terrain in [2_developing_new_terrains](docs/2%20Software/3%20Developing%20new%20static%20scenes/2_developing_new_terrains.md), but this time in folder `src://src/objects/sports/gltf/cone.gltf`. Godot will import it.

## Creating the object scene in Godot

Although we could use the glTF file we just created directly in any scene, we will add an additional layer between the terrain scene (.tscn) used everywhere, and its source geometry (.gltf). This will allow us to add required collision shape to the object.

In Godot, create a new 3D scece, and drag and drop the `cone.gltf` file onto the root Node3D. Rename the root node to "Cone", then save it in `wheelsims/objects/sports/cone.tscn`.

## Adding a collision shape

If we don't add a collision shape, the player would pass through it instead of colliding with it.

In the [terrain tutorial](docs/2%20Software/3%20Developing%20new%20static%20scenes/2_developing_new_terrains.md), we created trimesh collision shapes using the mesh geometry, which is the best option for complex shapes such as unlevel grounds and walls. However, trimesh collision shapes have a high computational cost and should be avoided for simple objects. A better option is to use primitive shapes such as spheres, cubes and cylinders.

Here, we will create a cylinder around the shape.

Begin by adding a StaticBody3D to the cone:

![](docs/2%20Software/3%20Developing%20new%20static%20scenes/developing_new_static_objects_static_body_3d.png)

Then add the required CollisionShape3D to the StaticBody3D:

![](docs/2%20Software/3%20Developing%20new%20static%20scenes/developing_new_static_objects_collision_shape_3d.png)

And then, in the inspector with the CollisionShape3D selected, select a new CylinderShape3D as the shape:

![](docs/2%20Software/3%20Developing%20new%20static%20scenes/developing_new_static_objects_collision_shape_3d_primitive.png)

Match the cylinder to the cone shape using the three red control points.

![](docs/2%20Software/3%20Developing%20new%20static%20scenes/developing_new_static_objects_match_cone.png)


## Adding a navigation obstacle

Although the cone currently has a collision shape, this only applies to the player: NPCs can still pass through it.

Add a NavigationObstacle3D to the cone, and give it an appropriate radius. Now the NPCs will avoid the cone.

![](docs/2%20Software/3%20Developing%20new%20static%20scenes/developing_new_static_objects_final_godot.png)

Save the `cone.tscn` file. From now on, you can drag this `cone.tscn` file into any scene.
