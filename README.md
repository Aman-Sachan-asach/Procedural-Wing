# [HW1: Noise](https://github.com/CIS700-Procedural-Graphics/Project1-Noise)

## Project Description

### Overall description

The project goes about creating the wing of a bird, albeit perhaps not the most detailed model.
Various GUI controls were added to give the project more life.

GUI controls let you:

1. Change the colors of the feathers of the wing

2. Change the strength and direction of wind, which is seen as a small perturbarance 

3. Change the persistence of the octaves of Noise

4. Change the number of octaves of Noise

5. Change the field of view of the camera

6. Change the aspect ratio of the camera

The UVs are updated constantly to make the surface of the sphere seem animated.

### Things Done:

#### main.js description

1. Created a Icosahedron geometry, which when sub-dived approximates a sphere really well.

2. Using this approximated sphere and a custom material 'color_Material', I created a sphere mesh, that was added to the scene.

3. The color_Material contains multiple uniforms (including multiple textures that will be used with different image samplers), that will be passed too the shader to control various aspects. Some of these uniforms were also added to the GUI to increase interactivity.
   'color_Material' also holds the creates its own fragment and vertex shaders (all Materials in nodejs do).

4. All the GUI parameters and uniforms used by the shader are updated to create a dynamic looking scene in 'function onUpdate(framework)'

#### Shaders

##### Vertex Shader

1. The Vertex shader deals with the actual Noise function, using which we deform the position, of that vertex along it's surface normal.

2. The noise function is a multi-octave noise function, that utilizes a simple hash function to map a 3D point to some unique noise value.
The noise function also makes use of a cosine interpolation and smoothing stage to give a less jittery and smooth noise output.

3. The noise output is just a float value that scales the normal of that vertex and adds this scaled normal to the vertex position.

##### Fragment Shader

1. The fragment shader utilizes a flag to determine which image sampler, if any, is to be used to create a colorful deformed sphere at every timestep.
