# THREE.js-PathTracing-Renderer
Real-time PathTracing with global illumination and progressive rendering, all on top of the Three.js WebGL framework.

<h2>LIVE DEMOS</h2>

* [Geometry Showcase Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_GeometryShowcase.html) demonstrating some primitive shapes for ray tracing.

* [Cornell Box Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_CornellBox_DirectLighting.html) which renders the famous Cornell Box, but at ~60 fps!

For comparison, here is a real photograph of the original Cornell Box vs. a rendering with the three.js PathTracer:

![](readme-Images/measured.jpg) ![](readme-Images/CornellBox-Render0.png)

* [Physical Sky Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_SkyModel.html) which models Earth's atmospheric scattering and time of day.

* [Quadric Geometry Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_QuadricGeometryShowcase.html) showing different quadric (mathematical) shapes (Warning: this may take 7-10 seconds to load/compile!)

<h3>Constructive Solid Geometry(CSG) Museum Demos</h3>

The following demos showcase different techniques in Constructive Solid Geometry - taking one 3D shape and either adding, removing, or overlapping a second shape. (Warning: these demos may take 10 seconds to load/compile!) <br>
All 4 demos feature a large dark glass sculpture in the center of the room, which shows Ellipsoid vs. Sphere CSG. <br>
Along the back wall, a study in Box vs. Sphere CSG: [CSG_Museum Demo #1](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_CSG_Museum_1.html) <br>
Along the right wall, a glass-encased monolith, and a study in Sphere vs. Cylinder CSG: [CSG_Museum Demo #2](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_CSG_Museum_2.html) <br>
Along the wall behind the camera, a study in Ellipsoid vs. Sphere CSG: [CSG_Museum Demo #3](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_CSG_Museum_3.html) <br>
Along the left wall, a study in Box vs. Cone CSG: [CSG_Museum Demo #4](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_CSG_Museum_4.html) <br>

Important note! - There is a hidden Easter Egg in one of the 4 Museum demo rooms.  Happy hunting!

<h3>Materials Demos</h3>

These demos showcase different materials possibilities: <br>
Refractive (glass/water) and ClearCoat (billiard ball/car paint) materials: [Materials Demo #1](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_MaterialsShowcase_1.html) <br>
Volumetric (smoke/fog/gas) and Metallic (aluminum mirror) materials: [Materials Demo #2](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_MaterialsShowcase_2.html) <br>
Diffuse (matte wall paint/chalk) and Translucent (skin/balloons,etc.) materials: [Materials Demo #3](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_MaterialsShowcase_3.html) <br>
Metallic (Gold) and shiny SubSurface scattering (polished Jade/wax candles) materials: [Materials Demo #4](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_MaterialsShowcase_4.html) <br>

![](readme-Images/threejsPathTracing.png)

<br>
<h2>FEATURES</h2>

* Real-time interactive Path Tracing in your Chrome browser - even on your smartphone! ( What?! )
* First-Person camera navigation through the 3D scene.
* When camera is still, switches to progressive rendering mode and converges on a photo-realistic result!
* The accumulated render image will converge at around 1,000-2,000 samples (lower for simple scenes, higher for complex scenes).
* Direct lighting now makes images render/converge almost instantly!
* Support for: Spheres, Planes, Discs, Quads, Triangles, and quadrics such as Cylinders, Cones, Ellipsoids, Paraboloids, Hyperboloids, Capsules, and Rings/Torii.
* Constructive Solid Geometry(CSG) allows you to combine 2 shapes using operations like addition, subtraction, and overlap.
* Basic support for loading models in .obj format (triangle and quad faces are supported, but no higher-order polys like pentagon, hexagon, etc.)
* Current material options: Metallic (mirrors, gold, etc.), Refractive (glass, water, etc.), Diffuse(matte, chalk, etc), ClearCoat(cars, plastic, billiard balls, etc.), Translucent (skin, leaves, etc.), Subsurface w/ shiny coat (jelly beans, cherries, white glue, polished Jade, etc.), Volumetric (smoke, dust, fog, etc.)
* Diffuse/Matte objects use Monte Carlo integration (a random process, hence the visual noise) to sample the unit-hemisphere oriented around the normal of the ray-object hitpoint and collects any light that is being received.  This is the key-difference between path tracing and simple old-fashioned ray tracing.  This is what produces realistic global illumination effects such as color bleeding/sharing between diffuse objects and refractive caustics from specular/glass/water objects.
* Camera has Depth of Field with real-time adjustable Focal Distance and Aperture Size settings for a still-photography or cinematic look.
* SuperSampling gives beautiful, clean Anti-Aliasing (no jagged edges!)
* Users will be able to use easy, familiar commands from the Three.js library, but under-the-hood the Three.js Renderer will use this path tracing engine to render the final output to the screen.

<h3>Experimental Works in Progress (W.I.P.)</h3>

The following demos show what I have been experimenting with most recently.  They might not work 100% and might have small visual artifacts that I am trying to fix.  I just wanted to share some more possible areas in the world of path tracing! :-) <br>

This Demo renders objects inside a volume of gas/dust/fog/clouds(etc.).  Notice the cool volumetric caustics from the glass sphere on the left!: <br>

* [Volumetric Rendering Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_VolumetricRendering.html) <br>

This Demo deliberately creates a very hard scene to render because the light source is almost 100% blocked.  Normal naive path tracing will be very dark and noisy because the rays from the camera can't find the light source unless they are very lucky: <br>

* [Naive Path Tracing Hidden-Light comparison Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_CompareUni-Directional.html) <br>

Enter Bi-Directional Path Tracing to the rescue!  Not only do we trace rays from the camera, we trace rays from the light source as well, and then at the last moment, connect them.  The result is still a little noisy, but much better (we can actually see something!)<br>

* [Bi-Directional Path Tracing Hidden-Light comparison Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_Bi-Directional_PathTracer.html) <br>

Rendering spheres, boxes and mathematical shapes is nice, but most modern graphics models are built out of triangles.  The following demo uses an .obj loader to load a model in .obj format (list of triangles) from disk and then places it in a scene to be path traced.  As of now, it runs too slow for my taste.  It still needs a BVH acceleration structure to speed things up greatly (I am currently investigating different approaches on the GPU). I am showing this because I wanted to demonstrate the ability of the three.js PathTracing renderer to load and render a model in one of the most popular model formats ever: <br>

* [.OBJ Model Loading Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_OBJModel_Loader.html)<br>

Some pretty interesting shapes can be obtained by deforming objects and/or warping the ray space (position and direction).  This demo applies a twist warp to the spheres and mirror box and randomizes the object space of the top purple sphere, creating an acceptable representation of a cloud (for free - no extra processing time for volumetrics!)
* [Ray/Object Warping Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/ThreeJS_PathTracing_Renderer_RayWarping.html)<br>

<h2>Updates</h2>

* April 11th, 2017: 4 new CSG_Museum demos!  Constructive Solid Geometry(CSG) allows the creation of interesting, complex shapes by combining 2 basic 3D shapes (like Box and Sphere).  Operations include Plus (fuse the 2 shapes together into 1 shape), Minus (remove a negative chunk out of the first shape with the second shape), and Overlap (only render the volume where the two shapes overlap or intersect).  I'm pretty happy with how these operations turned out, although I'm reaching the compilation limit on my humble laptop integrated graphics card.  This is why the demos are split into 4 different showcases.  Trying to stuff ALL the artwork into one room was crashing my browser at shader-compilation time.  Interestingly enough, my Samsung S7 has no problem and achieves 30-60 fps.  Ray/Path tracers eat math shapes (Spheres, boxes, etc.) for breakfast which is why I went down this CSG path temporarily.  I'm still actively working on the BVH so we can start having regular triangular models at 30-60 fps. It's the most complicated piece thus far.  Soon! 
* March 29th, 2017: New Ray-Warping exprimental W.I.P. demo!  Also, I am actively working on the GPU BVH Acceleration structure to speed up triangle model rendering.  There are not many easy-to-understand BVH resources on the internet, so I'm putting all the pieces together by myself one step at a time.  So far I have the BVH builder working.  Now I'm writing the GPU ray-BVH intersection code which has to quickly grab the BVH off of GPU texture memory.  Hard to debug with Javascript/Browser, as I don't have much printout options from what's happening on the GPU.  As soon as I have something decent, I'll share it to this repo!  :) <br>
* March 22nd, 2017: Added 2 buttons to mobile controls (tablet and smartphone), for a total of 6 buttons.  With the addition of these buttons, now all the physical camera properties can be changed in real time just like the desktop version could.  Horizontal pinching controls the field of view (FOV), Vertical pinching controls the camera aperture size, and the 2 new buttons are used to move the focus distance (focal point) farther from the camera or closer to the camera. <br>
* March 3rd, 2017: Complete overhaul of mobile joystick controls.  Now the controls on Cell Phones and Tablets have a smooth, fluid response.  Also I changed the look of the buttons to directional, which makes more sense in this fly-cam setting.  However, I left the vintage joystick arcade-style circular buttons code intact, but commented out, so if you want a character jump-action button, etc., you can just mix and match the button shapes to your liking! :-) <br>

<h2>TODO</h2>

* Instead of scene description hard-coded in the path tracing shader, let the scene be defined using the Three.js library
* Allow variable triangle counts in fragment shader due to varying .obj file model complexity.
* Consider splitting up triangle list DataTexture into multiple textures for higher-poly-count models.  Current texture width/size limit is 4096 for Android (that's 4096 / 3 vertices per triangle / 3 floating-point coordinates per vertex = 455 possible triangles.  Need to increase this limit to 100,000 (or more) possible triangles somehow.  Maybe data going in the texture's v direction in addition to the u direction?
* Implement AABB BVH (bounding volume hierarchy) for object/primitive culling, especially to speed up .obj model rendering.
* Dynamic Scene description/BVH updating and streaming into the GPU path tracer via Data Texture.
* Until a decent BVH is implemented, triangle models are not included in the GitHub repo demo (although they load and render perfectly, the frame rate is still too low, especially with models of 100 or more triangles). <br>

<h2>ABOUT</h2>

* This began as a port of Kevin Beason's brilliant 'smallPT' ("small PathTracer") over to the Three.js WebGL framework.  http://www.kevinbeason.com/smallpt/  Kevin's original 'smallPT' only supports spheres of various sizes and is meant to render offline, saving the image to a PPM text file (not real-time). I have so far added features such as real-time progressive rendering on any device with a Chrome browser, FirstPerson Camera controls with Depth of Field, more Ray-Primitive object intersection support (such as planes, triangles, and quadrics), and support for more materials like ClearCoat and SubSurface. <br>

This project is in the alpha stage.  More examples, features, and content to come...
