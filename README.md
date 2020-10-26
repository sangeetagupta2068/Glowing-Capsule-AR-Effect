# Learn to Build a Glowing Neon AR effect
<p align="justify">
In this tutorial, we attempt to help all aspiring Spark AR creators understand the basics of Render passes and build a basic glowing AR effect which creates a light trail whenever the glowing object is moved. Before we start talking about the pre-requistes or the step by step tutorial for building this filter, let's see how this filter actually looks like!
</p>
<p align = "center">
  <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/REFERENCE1.png" width="30%" height="30%">
</p>

## Pre-requisites
<p align="justify">
Now, are you excited to build this filter? Well, before moving ahead, let's see what are the check pointers you would be needing to create this tutorial. 
  <ul>
   <li> Spark AR Studio version 92 or later </li>
   <li> Familiarity with the basic concepts of creating AR effects using Spark AR </li>
   <li> You are as eager to implement this filter as much as we are to walk you through this! </li>
  </ul>
</p>

## Inspiration
<p align = "justify">
Now that we discussed the check pointers, we wanted you to understand what was the motive behind creating this tutorial. Technology has always been about creating magic with logic for us and Augmented Reality has just opened doors for us as technologies to implement our imaginary friends and objects into the real world. We strongly feel as newbies into this world of creating AR effects to express yourself, understanding the application of Render passes using this tutorial will give you new feathers to create filters with realistic glowing, trail and shader effects, thus giving you a new opportunity to go more creative with your Spark AR filters and engage your audience in this lockdown! 
</p>

## Creating the Effect
<p align = "justify">
 Now, let's get started by first creating mini milestones for creating our effect. Our milestones for this project are : 
  <ol>
   <li>Create the basic scene</li>
   <li>Implement the glow effect on the 3D object</li>
   <li>Add a shader to the Camera Texture</li>
   <li>Implement a trail effect to our 3D object</li>
  </ol>
</p>

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
 - Now, let's make this effect more realistic by adding a light shader in our camera texture. We can achieve this by adding passing our camera texture and a value color to the Multiply node. If you try connecting the output of this node to our original Scene Render pass, you will see it gives an error. This is because, when we supply a color value along with our camera texture to the Multiply node, we get a color as an output. However, Scene render pass expects an image as it's background and scene object to create the texture for our scene output. So, now, how do we add this grey shade to our background then ? Enters Shader Render pass. Shader Render pass helps us convert our color texture into an image which can be supplied as an input to our original scene render pass. Essentially, what we need to do is supply the output of our Multiply node to the Shader Render pass and the output image of this render pass is passed as the background to our Scene Render pass. You can now see a grey background added to our camera texture.
 
 ### Adding the trail to our capsule : 
- Now it's time to add the final light trail to our glowing capsule object. Let's start by creating a Delay frame object. The Delay frame expects an image as it's first frame which is required to be delayed. So, we need to add a Shadow Render Pass to our final output of the Add node and supply this to the Delay Frame's first frame. Let's add a reciever to display the output of our Delay Frame patch. We will now have to add a Shader Render pass to our Reciever object. Let's pass this Reciever output object to our scene output. If you observe, nothing is visible on our screen. This is because the Delay Frame expects an input image frame to render and display our Reciever output. Essentially, we want to see the trail while we move and view our object. How do we achieve this? 
- Here comes the Mix patch. Mix let's us interpolate between our glowing capsule effect and Display Frame Reciever based on the Alpha value supplied. Let's connect our Display Frame Reciever object and Add patch output to the Mix patch and let's supply the output of this patch to our Shader Render pass connected to the main output Scene. You will see if we move our capsule object, there is a trail following it. However, when the user moves, there is a trail following the user movement in the background as well. So, how do we get rid of this?

### Adding trail only to the capsule :
so insted of making the trail in the last we are going to make it before sending it to the blur patch so it has anoter advantage as we use add patch that gives extra glow to the trail patch . so we send the trail to blur and the add it like we did before with the blur . So now the blur will be also happen to the trail of the capsule. 

### Moving the capsule  :
now we have done the basic mateiral for the glow we can now animate how ever we want . We can make it move it or rotate . This method can be applied to any object and any type of mateiral . Each material will give differnt output. Based on the needes we can change the parametars of the materials. 

## Created by : 
* <a href = "https://github.com/rbkavin"> Kavin Kumar </a>
* <a href = "https://github.com/sangeetagupta2068/"> Sangeeta Gupta </a>
