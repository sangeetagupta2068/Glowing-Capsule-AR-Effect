# Glowing-Capsule-AR-Effect

### Creating the basic scene : 
 - Create a Blank Spark AR Studio project -> Import 3D capsule object from the AR library (AR library -> 3D objects -> 3D shapes) -> add asset to the scene -> set scale to 2 x 2 x 1
 - Select Device -> In Render output -> Render pass -> Create Default pipeline
 - This gives us a default structure setup as camera texture and device as input objects connected to the scene render pass which is inturn connected to the scene output. While camera texture helps us capture the live video when someone interacts with our effect is connected to the background property of Scene Render pass, the Device is connected to the scene object which inturn gives us a texture rendered in the screen output.
 - Now, it's possible to have multiple Scene render pass connected to multiple objects for one scene. 
 
 
 ### Creating the glow effect : 
 - In order to create luminious effect for our object, we need to overlay our actual capsule object over it's blurred version such that it gives a light emitting effect. Let's do this by creating a patch. 
 - First, let us create a copy of the Scene Render pass in the patch editor. If we drag our capsule from the scene to the patch editor, it's object is created. Let us add this object as the scene object property of our Scene Render pass. We want to create a blurred effect of this object. For this, browser and import the Blur patch from the AR library and import it into assets. Add this Blur asset as an object by dragging it to the patch editor. Connect the newly created Scene render pass's texture to Blur with the Blur amount set as 1. Now, if you connect the Blur patch to Device, you can see a blurred effect of our capsule object is created. 
 - Now, for creating the light emitting effect, we need to overlay our actual capsule object on top of this blurred object. For this, simply create an Add node and supply the Blur patch output as the first value and our initial Scene Render Pass output as the second value. Connect the output of the Add node to the Scene output.
 - Let's add a neon green material color to our capsule object. Can you observe the glow on our capsule ? 
 
 ### Adding a background shader : 
 - Now, let's make this effect more realistic by adding a light shader in our camera texture. We can achieve this by adding passing our camera texture and a value color to the Multiply node. If you try connecting the output of this node to our original Scene Render pass, you will see it gives an error. This is because, when we supply a color value along with our camera texture to the Multiply node, we get a color as an output. However, Scene render pass expects an image as it's background and scene object to create the texture for our scene output. So, now, how do we add this grey shade to our background then ? Enters Shader Render pass. Shader Render pass helps us convert our color texture into an image which can be supplied as an input to our original scene render pass. 
 
 ### Adding the trail to our capsule : 
- We are almost done with our glowing capsule effect. Now it's time to add the final light trail to our glowing capsule object. 
