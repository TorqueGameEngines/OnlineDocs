Source Code Tour
*****************

Introduction
=============
This document will explain the source code folders and files that make up Torque 3D's rendering system.

GFX Core
=========
You can find the core GFX files in **engine/gfx**. Some of the source files in this system are meant to be sub-classed based on platform. There are currently 4 main gfxDevice classes:

* GFXDevice
* GFXD3D9Device (inside the D3D9 directory)
* GFXGLDevice (inside the gl directory)
* GFXNullDevice (inside the Null directory)

As you can see, each platform has its own GFXDevice. The same goes for other platform dependent files: gfxShader, gfxCubemap, gfxVertexBuffer, and so on. Some of the other source files are stand-alone. For instance, gfxStructs.h contains classes/structs and functions used by all platforms. This usually involves generic information, such as GFXLightInfo containing light type, position, etc.

DirectX (D3D, D3D9)
====================
Because Torque 3D supports cross-platform compatibility, it is important to keep the GFX layers separate. The D3D folder contains only two files: screenshotD3D.h and screenshotD3D.cpp. Just as the name implies, these two files are used in capturing screens while running a game. (Currently D3D9 only).


You will see the major platform specific classes represented here, such as the GFXdevice, TextureManager, VertexBuffer, etc. The functionality remains the same, but the application and execution are specific to the API. 

OpenGL (gl and ggl)
====================
Much like the D3D sections, the gl folder and its files contain rendering functionality specifically meant to run on a Mac. Once again, the major systems are integrated into the OpenGL layer (StateBlock, GFXDevice, PrimitiveBuffer, etc).


Within the gl directory is another folder: ggl. The source code in this section make up the Torque OpenGL Library. In the code itself, you will find the various OpenGL configurations, bindings, and extension definitions. 

Null
=====
The Null folder contains gfxNullDevice.h and gfxNullDevice.cpp. This device layer is used primarily for dedicated servers, which typically do not require any rendering. Dedicated servers usually just process simulation events and relays that information to the clients. There is no real reason to waste processing power and memory rendering objects that no one will see.

Sim
====
The 3 systems found in this folder are: CubeMapData, gfxStateBlockData, and debugDraw.

**debugDraw** does exactly what it sounds like. Once you enable debugDraw, you can pass it data (Point3Fs and ColorF) which will then render points, cubes, and other polygons. For instance, if you pass in the points that make up a Player's bounding box, you will see a box surrounding that player when running the game.

**CubemapData** is a class exposed to TorqueScript, making the class a ConsoleObject. A Cubemap is a texture that represents a rendering of the surrounding environment. The easiest example to explain would be a Sky cubemap rendered onto a body of water. The cubemap would consist of various sky images taken from different angles.

**GFXStateBlockData** is extremely important. Since GFXStateBlocks are meant to be created in script, a ConsoleObject that can hold StateBlock description was needed. GFXStateBlockData is that ConsoleObject. This covered in more detail in Stateblocks. (TODO - Internal link)

Test
=====
*You can ignore this folder, as it was used during internal testing.*

RenderInstance
================
Another section of engine code that is considered an important part of GFX can be found under renderInstance (engine/renderInstance). The files found in this directory make up the various render managers. We will cover these in the next GFX document. For now, just remember these classes are responsible for controlling the rendering flow of your game. 

Conclusion
============
This guide is another high level walk through of a Torque 3D system. Even though we covered some major files and concepts, you should take the time to read through the code comments left by the engine developers. Some of this will make more since as you read through the remaining GFX documents.
