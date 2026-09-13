# Obstacle Race (in progress)

## Parameters of an obstacle race
### Race data
The obstacle race is organized with different race levels. Every race level has parameters defined in a race_data object: 

![243](obstacle_race_race_data.png)
*Screenshot of the inspector of obstacle_race_generator node*

*Every length is in meters*

A race is composed of challenges. A challenge is a sequence of different objects. A challenge is defined by the spacing between its objects and the size of those objects. Objects can be either walls or obstacles. This is why there are separate parameters for obstacles and walls.

**For obstacles:**

- Size → **Obstacle Size Range**
- Space between obstacles → **Opening Size Range**

**For walls:**

- Size → **Wall Size Range**
- Space between walls → **Opening Size Range**

The range corresponds to the minimum and maximum lengths.

You can control the proportion of walls and obstacles using the **Obstacle Opening Probability** parameter (1 for obstacle, 0 for opening).

Walls can be transparent or opaque (e.g., a brick wall or a fence). You can control this proportion using the **Transparent/Opaque Wall Probability** parameter (1 for transparent, 0 for opaque).

These parameters can be edited in the inspector of the **obstacle_race_generator** node.

###  Objects

In the same node (obstacle_race_generator), you need to fill the object fields to generate the objects. They are 3 lists:

![302](obstacle_race_objects_inspector.png)

- ***Obstacle Infos***
- ***Transparent Wall Infos***
- ***Opaque Wall Infos***

These are resource objects called ObjectInfo. They are not the scenes of the objects directly. They contain different fields:

![324](obstacle_race_object_info_inspector.png)


- _**Scene**_: References the scene required to instantiate the object.
- _**Sizes**_: A dictionary containing the object sizes along each axis, depending on the object’s rotation.
- _**Local Scale**_: The object size using the default rotation defined in the scene.

The sizes are needed to calculate dimensions without instantiating every object:

- the depth of the challenge (i.e., the greatest X value among the obstacles in the challenge)
- the object size (i.e., the Z value)

To obtain this object information, the data must be baked before running the main scene.

---
## How to bake objects

A tool script named **object_size_baker.gd** is used to create the **ObjectInfo** resources from the scenes.

### First step

All scenes you want to bake must be located in the same folder.

Then, reference this folder path in **baked_config_res.tres**.  
This resource is located in:

`games/races/obstacle_race/generator/baker`

Next, create a destination folder for the **ObjectInfo** resources and reference its path in **baked_config_res.tres**.

### Second step

Run the baker script **object_size_baker.gd**, located in:

`games/races/obstacle_race/generator/baker`

**How to run it:**  
Open the script and press **Ctrl + Shift + X**, or right-click the file and select **Execute**.

If the process succeeds, a message will appear in the console listing the created **ObjectInfo** files and their paths.

### Third step

The **ObjectInfo** resources are now created. You must assign them in the inspector of the **obstacle_race_generator** node.
