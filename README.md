# Normal Editing Workflow
## Step 1: Download the Blend File
The blend file contains the nodes required for this workflow as well as a simple example mesh. You can use the asset browser or append the node groups into your desired file. 

## Step 2: Prerequisites
The face must have a UV unwrapped that is symmetrical such that the u coordinate can be inverted to get the corresponding mirrored side. Such a UV map looks like this: 

![image](https://user-images.githubusercontent.com/26509702/219269633-fba9676d-19b4-4dab-a816-5940b7a07839.png)

An easy way to achieve this result is through the mirror modifier. The rest of this tutorial will assume that in your setup, your character is in a rest pose, the +z axis is up, the character is looking in the direction of the -y axis, and that every point on the character's right side has a positive x value. Whenever I mention a light source, assume it is a sun lamp. 

## Step 3: Create Guidelines
This workflow requires two textures to define the normals of the face: an azimuth texture and an elevation texture. To make the creation of these textures easier, use blender's texture paint mode to create a guideline texture that has iso-asimuthal and iso-elevation contours. Below is an example of what it should look like:

![image](https://user-images.githubusercontent.com/26509702/219268297-22699331-af40-4398-ad23-3c1276c9e959.png)

The red lines are guide lines for forming the guide lines. The green lines are the shadow lines that occur when the light direction is parallel to the horizontal plane and is free to move on the axis perpendicular to the horzontal plane (the z axis in most setups). The blue lines are shadow lines that occur when the light direction ray is contained in the plane of symmetry between the left and right side of the face (yz plane in most setups). The light is free to rotate on the on the axis perpendicular to this plane (x axis in most setups). Once we have defined our shadow contour lines, we can create the azimuth and elevation maps.

## Step 4: Creating the Maps
To create the maps, we will use something called [sdf_tool](https://drive.google.com/file/d/1lvzZLBC8uet1cokQPCJkV5x7S3OnBY4X/view), which was created by 橘子猫. I was unable to find any accounts they have online. Unfortunately, this tool only works on windows. Open the guideline image in your image editing app of choice. The following example will be shown in Krita. We will start with the azimuthal map. On a new layer, we will select and fill with pure white the side of the face that faces the positive x axis. We will name this layer "a1".

![image](https://user-images.githubusercontent.com/26509702/219270384-b1296c22-f5f9-43c3-ba77-96a5e3858d95.png)


Then, we will create a new layer called "b1" and block out a new area. Imagine we are rotating the light source so that it aligns closer to the front of the face. We will block out the areas that face the light source now AND the area that was blocked out in the previous layer.

![image](https://user-images.githubusercontent.com/26509702/219271149-fa138196-96a3-4d25-89c7-861bd334772b.png)

Here we can see that I also chose to highlight the left side of the nose. It's useful to store the nose as its own hidden layer so it can be copied into other light blocking layers. Also note that each light block creeps into the next azimuthal contour line. 

Repeat the process until you reach the halfway point of the face.

![image](https://user-images.githubusercontent.com/26509702/219271355-743f3787-2009-42e3-a1e6-a36a8be45948.png)


Then save each layer, except for the guideline layer as a separate image in `sdf_tool/images`. They should be named "a", "b", "c", etc. Then, edit the `run.bat` and `run.py` files to only include the files that you have made. You may have to add or remove file names. Then, you can run the run.bat file. The result should be an image like this:

![image](https://user-images.githubusercontent.com/26509702/219271725-07ea73ee-54df-4b9a-878e-d86441d59846.png)

Repeat for the elevation angles:

![image](https://user-images.githubusercontent.com/26509702/219271826-54a6770f-277f-4027-9ffe-d9a9e87898ee.png)


In my experience, it's best the keep the number of contours relatively small for elevation and to create large patches of constant elevation. 

## Step 5: Assembling the Nodes
As you could probably tell, the UV coordinates will be mirrored from one side to another. You node setup should look like this:

![image](https://user-images.githubusercontent.com/26509702/219272393-0018db21-7ad4-4f56-bb77-abc386301df0.png)


There is only one parameter that you should tweak, the `Z` parameter on the `azimuthToXY` node. This determines the default elevation of the normal outputted by the node. A value of 0 is perfectly horizonal. A value of .25 points the elevation slightly upward. The color in the RGB node is the up vector (BCBCFF).

## Step 6: Result
Here's what everything looks like put together:


![image](https://user-images.githubusercontent.com/26509702/219272795-a391e54a-10fe-4738-9090-45ad4deb76ef.png)



