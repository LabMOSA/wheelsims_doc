# Developing new terrains in Blender

A terrain is an FBX file that contains the ground and walls, and is generally designed in Blender. Developing a new terrain is always the first step in designing a new playable scene. In this guide, we will develop a very simple terrain that models a road, a widewalk, some grass and a facade.

## Preparing folders

Before creating a new terrain, create this folder in the `wheelsims_artwork` repository:
- `terrain/demo` that will contain the source Blender file for our terrain;
- `terrain/demo/textures` that will contain the jpg/png files used as textures for our terrain.

Remember that all folder and file names must be in `snake_case` (lower case with words separated by underscores) according to the [file name conventions](docs/2%20Software/2%20Developing%20Wheelsims/2_conventions.md).

## Creating the base geometry

Create a basic scene like this one, and save it as `terrain/demo/demo.blend`.

![](developing_new_terrains_blender_base_geometry.png)

This scene has:
- two planes for the grass: one will contain a navigation shape for NPCs and not the other, to prevent NPCs from approaching the building;
- one plane for the road: note that it is lower than the grass planes;
- one mesh for the sidewalk that consists of one horizontal plane bordered by two planes;
- one cube for the building.

## Deforming to account for terrain elevation

To make things a little bit more interesting, we will deform the ground planes and the sidewalk to make a small hill. First add more precision to the meshes so that they can deform: split it in squares of about 2 meter-squared.

*Note that for large scenes, a resolution of 2 meter-squared may be too detailed, and that duch detailed resolutions should be reserved for the few areas with small hills and drops.*

![](deveoping_new_terrains_deform1.png)

Then select all materials, and apply their scale (CTRL+A, Apply Scale). This will prevent issues later when importing the FBX in Godot.

Now select the ground planes (not the building), and add a lattice object to deform those planes. Here we set the resolution of the lattice to 5x5).

![](deveoping_new_terrains_deform2.png)


![](deveoping_new_terrains_deform3.png)


Edit the lattice and raise the middle point with proportional editing in smooth mode to create the desired hill.

![](deveoping_new_terrains_deform4.png)

Set the ground shading to auto-smooth.

![](deveoping_new_terrains_deform5.png)

## Applying temporary materials

Create plain colour temporary materials for now. We will add texture later when we know that everything works well.

![](deveoping_new_terrains_materials.png)

## Exporting to glTF

Once the terrain is completed in Blender, use File → Export → glTF 2.0 (.glb/.gltf), and apply the following options (important):
- In format, select glTF separate (.gltf + .bin + textures). This separates the textures from the mesh information (.bin) which is more git-friendly.
- In Textures, write "textures". This is the subfolder where the textures will be exported.
- Click "Remember Export Settings" to do this once with the current Blender file.
- In Mesh, select "Apply Modifiers", unless you have no modifiers in your current file (which is unlikely since auto-smooth shading is a modifier).

Save the file in the Godot project as `res://src/maps/demo/gltf/demo.gltf`. The terrain will then be imported by Godot.


![](deveoping_new_terrains_export.png)


Now continue to [](3_developing_new_maps.md) to work with this new terrain in Godot.
