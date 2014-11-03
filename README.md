-------------------------------------------------------------------------------
CIS565: Project 5: WebGL
-------------------------------------------------------------------------------

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/all.PNG)


The purpose of this project was to get used to GLSL vertex and fragment shading.

-------------------------------------------------------------------------------
PART 1 
-------------------------------------------------------------------------------

For this part of the assignment I created a dynamics wave animation that runs 
entirely on the GPU. 

The first animation is a simple sin-wave based vertex shader.

For my second animation I played with trigonometric functions and numbers
until I saw something that was interesting. My animation is a cosine function that 
takes in the values of the positions and multiplies them by some constants. 
I added sliders so the user is able to see the effect of changing the amplitude and the frequency of the function. 

I alse added color pickers to the vertices to allow for more interactivity. The user 
can change the color of the minimum and maximum points

-------------------------------------------------------------------------------
PART 2 
-------------------------------------------------------------------------------
For part 2 I implemented a GLSL fragment shader to render an interactive globe. The features 
that I have implemented are: 

* Night-time lights on the dark side of the globe
* Specular mapping
* Moving clouds
* Bump mapped terrain
* Rim lighting to simulate atmosphere
* Procedural water rendering and animation using noise 

-------------------------------------------------------------------------------
PART 2 WALKTHROUGH:
-------------------------------------------------------------------------------
This is what I started with: 

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/first.PNG)


**Night Lights**

The first step was to map a nighttime texture to the points that correspond to the 
dark side of the globe, that is, where diffuse lighting is zero. 
To do so I used linear interpolation between the two textures to achieve a gradient 
across both sides of the Earth. I also used a gamma correction to make the night lights stand out.

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/second.PNG)


**Specular Map** 

The part of the globe that corresponds to landmasses should not receive any specular lighting.
To find such points, I used a texture where the landmass is colored black and the water is colored white.
For landmass, the specular component was ignored, and it was only applied to the parts that correspond to water. 
The picture below shows the effect of applying specular lighting to land. 

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/spec.PNG)

**Clouds**

To determine the color of the clouds I used two textures: one gives the color of the clouds
 while the other one gives the transparency. During the day, the clouds receive diffuse lighting. 
To animate the clouds I  offset the component of the textures by a certain amount. 

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/fifth.PNG)

**Bump Mapping**

To achieve bump mapping I used another texture where the luminance corresponds to the 
height of each fragment. I read a texel and two of its neighbors (the right one and the top one) 
and created a perturbed normal in tangent space. This was then transform into eye coordinates and 
used for diffuse lighting instead of the original normal. 

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/fifth.PNG)

**Rim Lighting**

Rim lighting is the effect that makes the globe look as if it has an atmospheric layer.
To create this effect, I calculated the dot product of the normal and the position and used it as a 
threshold to add a color to our original color. 

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/seven.PNG)

**Procedural water rendering and animation using noise**

To animate the oceans I used Perlin noise. However, to achieve a more or less realistic effect 
you really need to play with the values and I haven't found any that make the ocean look realistic.
The following picture shows this effect. 

![alt tag](https://github.com/paula18/Project5-WebGL/blob/master/water.PNG)

-------------------------------------------------------------------------------
PERFORMANCE EVALUATION
-------------------------------------------------------------------------------
For my performance evaluation I measured the time is takes to render each feature. 
However, I did not see any difference; all take about 0.001s to render. I was going to measure the render
time having a skybox, but I wasn’t able to finish it. I will added when it is done.

-------------------------------------------------------------------------------
TODO
-------------------------------------------------------------------------------
I would like to finish the skybox implementation and create cloud shadows via ray tracing. 

-------------------------------------------------------------------------------
THIRD PARTY CODE POLICY
-------------------------------------------------------------------------------
My Perlin noise function is obtained at https://github.com/ashima/webgl-noise
 
