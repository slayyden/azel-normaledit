# Normal Editing Workflow
## Step 1: Download the Blend File
The blend file contains the nodes required for this workflow as well as a simple example mesh. You can use the asset browser or append the node groups into your desired file. 

## Step 2: Create Guidelines
This workflow requires two textures to define the normals of the face: an azimuth texture and an elevation texture. To make the creation of these textures easier, use blender's texture paint mode to create a guideline texture that has iso-asimuthal and iso-elevation contours. Below is an example of what it should look like:
![image](https://user-images.githubusercontent.com/26509702/219268297-22699331-af40-4398-ad23-3c1276c9e959.png)
The red lines are guide lines for forming the guide lines. The green lines are the shadow lines that occur when the light direction is parallel to the horizontal plane and is free to move on the axis perpendicular to the horzontal plane (the z axis in most setups). The blue lines are shadow lines that occur when the light direction ray is contained in the plane of symmetry between the left and right side of the face (yz plane in most setups). The light is free to rotate on the on the axis perpendicular to this plane (x axis in most setups). Once we have defined our shadow contour lines, we can create the azimuth and elevation maps.

## Step 3: Creating the Maps
To create the maps, we will use something called [sdf_tool]([url](https://drive.google.com/file/d/1lvzZLBC8uet1cokQPCJkV5x7S3OnBY4X/view)), which was created by 橘子猫. Open the guideline image in your image editing app of choice. The following example will be shown in Krita. 
