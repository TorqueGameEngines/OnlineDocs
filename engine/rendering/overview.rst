Overview
*********

Introduction
==============
Torque 3D's rendering system is a complex set of modules working together to deliver a next-gen appearance. In addition to many stand-alone rendering systems, such as managers and render instances, a core system is GFX. GFX is an abstract graphics layer designed to reside above graphics APIs such as Direct3D and OpenGL. The system utilizes current and next-gen concepts, such as deferred rendering technology, state blocks, shader buffers, and so on. 

High Level Features
=====================

Torque 3D's rendering features advanced technology, similar to what you might find in DirectX

* GLSL and HLSL shader support
* Vertex and primitive buffers
* Post-processing effects
* Deferred lighting
* Compatibility with Windows, Mac OS X
* State blocks
* Shader constant buffers


Platform Support
==================
GFX wraps around multiple rendering systems, which are handled automatically for you. When working in the engine, you will want to focus on the source code related to your target platform:

* **Windows** - GFX->D3D9 for rendering while input, window management, and general Windows components are handled by platformWin32, windowManager->win32, and a few other filters which will be detailed in the GFX Engine Tour. **Source Code Tour - TODO //Add Internal Link**
* **Mac OSX** - GFX->gl for rendering while platformMac and windowManager->mac handle input, window management, and other Mac components.


Key Concepts
=============
In order to grasp the high level rendering concepts of Torque 3D, you should be familiar with the following:

* **SDK** - A **S**oftware **D**evelopment **K**it is typically a collection of tools and APIs that focus on developing applications for a particular framework/hardware/OS. An example would be the DirectX SDK, which includes all of the APIs and debugging tools used in developing Windows games.
* **API** - An **A**pplication **P**rogramming **I**nterface is a collection of functions, classes, and systems dedicated to supporting a specific feature. An example would be DirectX's Direct3D, which is used for rendering. 
* **DirectX** (http://msdn.microsoft.com/en-us/directx/default.aspx) - A collection of APIs which handle rendering, input, audio, and other forms of media interaction. DirectX is commonly what drives game and video programming on Microsoft's operating systems. Examples of DirectX APIs include Direct3D (D3D) and DirectInput. DirectX developers must use the DirectX SDK to develop a Windows game. The SDK contains all of the DirectX APIs including the runtime libraries and source headers. 
* **OpenGL** (http://www.opengl.org/) - OpenGL stands for Open Graphics Library. This powerful, cross-platform API is used for low-level rendering of 2D and 3D graphics. Supporting OpenGL in Torque 3D is what allows the engine to run on Mac OSX.
* **Shaders** - Shaders are part of the DirectX and OpenGL rendering systems. A shader file contains a set of instructions that get passed to the GPU along with the 3D data it will affect. Both OpenGL and DirectX have their own shader languages, both of which are handled by Torque 3D's GFX. Examples of shaders include motion blur, reflection, bloom, bump mapping, and other advanced rendering effects. Shaders are typically written in a high level shading language based on C programming.
* **GLSL** - OpenGL Shader Language is a high level shading language utilized by OpenGL to create and render shaders in a game.
* **HLSL** (http://msdn.microsoft.com/en-us/library/bb509561%28VS.85%29.aspx) - High Level Shader Language is used by DirectX for creating and displaying shaders in a game. Using HLSL, you can create C like programmable shaders for the Direct3D pipeline.
* **Textures and Materials** - A texture is typically an image file mapped to a polygon or shape, which provides color and detail to the model. Torque 3D materials are used to wrap texture and shader information into a single object.
* **Vertex Buffer** - A vertex buffer is an array of vertex data which can exist in system or video memory. 

Important Links
==================

#. Torque 3D Documentation Page - http://www.garagegames.com/documentation/torque-3d
#. OpenGL Home Page - http://www.opengl.org/
#. DirectX Home Page - http://msdn.microsoft.com/en-us/directx/default.aspx

Conclusion
===========
This article is just a high level description of Torque 3D's rendering system. From here you can proceed however you want. However, it is highly recommended you proceed to the next section (Source Code Tour) if you are new to Torque 3D, GFX, or rendering code in general. 
