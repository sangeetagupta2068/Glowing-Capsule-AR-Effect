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

### 1. Creating the basic scene :
<p align = "justify">
  <ul>
    <li> Let's start by creating a Blank Spark AR Studio project and import any 3D shapes from the AR library. We are using the capsule object. Feel free to pick any object of your choice and add it to the scene.</li>
    <p align = "center">
        <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%201.10.31%20AM.png" width="80%" height="70%">
    </p>
    <li> If you observe, the size of this 3D object is quite small. Let's increase it's scale to 2 x 2 x 1.</li>
    <li> Now, we need to go to Device and in the Render Output Section, within Render pass, we need select Create for "Default pipeline" for the Scene Render Pass patch. This gives us a default structure setup as Camera Texture and Device input objects connected to the Scene Render Pass patch which is inturn connected to the Scene Output. Scene Render pass exists as a patch and essentially allows us to render our object(s) and their children into the Device scene.</li>
    <p align = "center">
        <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%201.21.05%20AM.png" width="80%" height="70%">

<i>Awesome guys! We have now setup our basic scene.</i>
  </ul>  
</p>
 
 ### 2. Implementing the glow effect on the 3D object : 
 <p align = "justify">
    <ul>
      <li>Now, in order to create luminious effect for our object, we need to overlay our actual 3D object over it's blurred version such that it gives a light emitting effect. Let's do this by first copying our Scene Render pass patch in the patch editor and removing all it's connectors. This is what we should ideally have.</li>
       <p align = "center">
        <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%201.39.11%20AM.png" width="80%" height="70%">
      </p>  
      <li> If we drag out 3D object from the scene to the patch editor, it's object get's created. We now need to connect this object as the Scene Object property of our Scene Render pass.</li>
      <li> To create the blurred effect of this object, we need to first browser and import the Blur patch from the AR library and import it into our assets. Post this, we need to add this Blur patch asset as an object by dragging it to the patch editor. </li>
      <li> Now, we need to connect the newly created Scene Render pass's texture to Blur with the Blur amount set as 1. If you connect the Blur patch to Device, you can see a blurred effect of our object is created. </li>
      <p align = "center">
        <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%201.47.43%20AM.png" width="80%" height="70%">
      </p>
      <li> Now, for creating the light emitting effect, we need to overlay our actual object on top of this blurred object. For this, simply create an Add patch and supply the Blur patch output as the first value and our initial Scene Render Pass output as the second value. Connect the output of the Add node to the Scene output. This is what we should ideally have.
      </li>
      <p align = "center">
        <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%201.54.26%20AM.png" width="80%" height="70%">
      </p>
      <li>Let's add a neon green material color to our object. Can you observe the glow better?</li>
      <p align = "center">
         <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%201.59.26%20AM.png" width="30%" height="30%">
      </p>
    </ul> 
 </p> 
 
 ### 3. Adding a shader to the Camera Texture :
 <p align = "justify">
  <ul>
    <li> Now, let's make this effect more realistic by adding a light shader in our camera texture. We can achieve this by adding passing our camera texture and a value color to the Multiply patch. If you try connecting the output of this node to our original Scene Render pass, you will see it gives an error. This is because, when we supply a color value along with our camera texture to the Multiply node, we get a color as an output. However, Scene render pass expects an image as it's background and scene object to create the texture for our scene output. So, now, how do we add this grey shade to our background then ? Enters <b>Shader Render pass</b>!</li>
  <li> Shader Render pass helps us convert our color texture into an image which can be supplied as an input to our original scene render pass. Essentially, what we need to do is supply the output of our Multiply node to the Shader Render pass and the output image of this render pass is passed as the background to our Scene Render pass. You can now see a grey background added to our camera texture.</li>
    <p align = "center">
         <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%202.30.03%20AM.png" width="80%" height="70%">
      </p>
  </ul>
</p> 

### 4. Implementing a trail effect to our 3D object :
<p align = "justify">
  <ul>
    <li> Now it's time to add the final light trail to our glowing capsule object. Let's start by creating a Delay frame object. The Delay frame expects an image as it's first frame which is required to be delayed. So, we need to add a Shadow Render Pass to our final output of the Add node and supply this to the Delay Frame's first frame. Let's add a reciever to display the output of our Delay Frame patch.</li>
    <li>We will now have to add a Shader Render pass to our Reciever object. Let's pass this Reciever output object to our scene output. If you observe, nothing is visible on our screen. This is because the Delay Frame expects an input image frame to render and display our Reciever output. Essentially, we want to see the trail while we move and view our object. How do we achieve this?</li>
    <li>Enters Mix patch! Mix let's us interpolate between our glowing capsule effect and Display Frame Reciever based on the Alpha value supplied. Here, since, we want a slow trailing effect, we set the Alpha as 0.9. Let's connect our Display Frame Reciever object and Add patch output to the Mix patch and let's supply the output of this patch to our Shader Render pass connected to the main output Scene. You will see if we move our capsule object, there is a trail following it. However, when the user moves, there is a trail following the user movement in the background as well. So, how do we get rid of this?</li>
    <p align = "center">
         <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%202.29.41%20AM.png" width="80%" height="70%">
      </p>
    <li>The trick here is to send the Delay Frame output to the blur patch so that it not only removes the trail on user movement but also an gives extra glow to the trailing effect. This is what our final patch editor structure would look like</li>
    <p align = "center">
         <img src = "https://github.com/sangeetagupta2068/Glowing-Capsule-AR-Effect/blob/main/media/Screenshot%202020-10-27%20at%202.29.31%20AM.png" width="80%" height="70%">
      </p>
  </ul>
</p>  

## Conclusion and next steps :
<p align = "justify">
Phew! Finally we are done with the glowing 3D object with a trailing effect. It's now time for us to add a rotating animation to it! I will leave creating the rotating effect upto you. You have access to the sample code if you get stuck. Do let us know what was your experience in creating the full effect. Wondering what you can do next post this effect ? We have got a few ideas :
  <ul>
    <li>Creating a Halo Angel effect</li>
    <li>Creating glowing Devil horns effect</li>
    <li>Creating an effect with fireflies</li>
  </ul>
  
  <i> PS - We would be awaiting to see your effects</i>
</p>

## Created by :
<ul>
  <li>
  <a href = "https://github.com/rbkavin"> Kavin Kumar </a>
  </li>
  <li>
  <a href = "https://github.com/sangeetagupta2068/"> Sangeeta Gupta </a>
  </li>
</ul>  
