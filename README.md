# TorchSample

Unreal Engine + Blender files for a simple (and complex) torch. Tryouts for materials and particle systems including Niagara.

![[doc/cover.jpg.png]]

## Inspiration
![https://i.all3dp.com/workers/images/fit=cover,w=1000,gravity=0.5x0.5,format=auto/wp-content/uploads/2021/10/26120703/some-low-poly-props-that-look-charming-and-cohesiv-toby-leung-210304_download.jpg](https://i.all3dp.com/workers/images/fit=cover,w=1000,gravity=0.5x0.5,format=auto/wp-content/uploads/2021/10/26120703/some-low-poly-props-that-look-charming-and-cohesiv-toby-leung-210304_download.jpg)
_Low poly design example_

## 3D Model
Trying to recreate a low poly torch I came up with a 5 to 6 edged torch shape. However unsure of its natural properties I wanted it to be somewhat rugged so at least it'd be recognizable as wood. I went experimenting with how materials could help in presenting the torch's looks, I fell down a rabbit hole that is material design. 

### Wood
First I tried making a wood design myself using blender's shader editor. Combining two wave textures over two different angles resulted in what somewhat resembled the rings of wood in an unnatural way. 
| | |
|-|-|
|![[doc/blender_wood_1.png]]|![[doc/blender_wood_1_nodes.png]]|

After watching a tutorial, using the base of a noise and musgrave texture and mixing those with gradients (colorramp) nodes, I got an actual wooden look to the torch. 

| | |
|-|-|
|![[doc/blender_wood_2.png]]|![[doc/blender_wood_2_nodes.png]]|

However, this look was too detailed for a low poly design and I decided to simplify it using only the two base textures and the gradient, effectively eliminating the roughness of the wood, resulting in a fairly good looking wood texture.

| | |
|-|-|
|![[doc/blender_wood_3.png]]|![[doc/blender_wood_3_nodes.png]]|

### Metal
For the iron I came about the same way, first fiddling around, then following a tutorial and finally using what I learned in the tutorial to make a simplified version.

I started with a principled BDSF node, adjusting base color, specular color, roughness and metallic sliders to create a somewhat metal-looking material.
![[doc/blender_iron_1.png]]

The post-tutorial material was so heavy, the blender application lagged.
| | |
|-|-|
| ![[doc/blender_iron_2.png]] | ![[doc/blender_iron_2_nodes_2.png]] |

However I learnt from both iron and wood I could use a noise texture to simulate the specks in the metal parts. Making it low detailed and somewhat smudged, the following material emerged.
| | |
|-|-|
| ![[doc/blender_iron_3.png]]| ![[doc/blender_iron_1_nodes.png]] |

### Reflecting
Both outcome materials are significantly different from my original inspiration, and I wouldn't use them under any circumstances in a low poly design environment. Ironically, the initial shader for the iron looks the most low poly design out of any materials. 

## Niagara particle system
I had never used the niagara particle system before, although I am a little familiar with Unity particle system. I decided my torch needed fire and went fiddling around in both Blender and Unreal Engine. However, since I only use blender for 3D modeling and shading, I quickly moved to Unreal Engine as I wanted to figure out how particle systems work.

Starting with a blank game and level, I added a new niagara system from existing emitter "Fountain". Next, in the Particle Spawn cycle, I tuned down velocity and lifetime, broadened the cone angle and set the mass to 0 to avoid gravity pulling the particles down.
| | |
|-|-|
|![[doc/niagara_1.png]]|![[doc/niagara_spawn.png]]|

Next was the color design. The color of animated fire usually goes from a bone-y white to orange to bright red. In the Particle Update cycle, I added a new Color module and compiled an array of five colors that the particles would change to throughout their lifetime (the older the particle, the brighter the red shade). 

Also, I added a Scale Sprite Size module to make the particles grow bigger and smaller throughout their lifetime according to a curve. This resulted in a somewhat similar effect to fire.

| | |
|-|-|
|![[doc/niagara_2.png]]| ![[doc/niagara_update.png]]|
