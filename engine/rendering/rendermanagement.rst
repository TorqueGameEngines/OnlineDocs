Render Management
******************

Introduction
=============
The purpose of the render manager system is to gather rendering commands submitted from game code and sort them to get proper effects, draw order, and optimal performance from GFX. 

RenderInst
===========
**RenderInst** is a base structure for more task-specific render managers. The current version of RenderInst only contains information on sorting, translucency, and rendering type overrides. 

ObjectRenderInst
=================
**ObjectRenderInst** is a derived from RenderInst. It does not actually contain any information about meshes, materials, transforms, etc. However, it makes use of a very important feature: Delegate callbacks. (RenderDelegate - TODO Internal Link)

MeshRenderInst
===============
Derived from RenderInst, a **MeshRenderInst** object contains the critical data needed for rendering. It is declared directly below ObjectRenderInst. Within this structure is an object's geometry(mesh), lighting information, textures, transforms, and base material.

Some of the most basic classes are used in MeshRenderInst:

* GFXVertexBufferHandleBase and GFXPrimitiveBufferHandle handle the vertex buffer and primitive buffer (respectively)
* World transforms and object-to-world transforms are handled by MatrixF pointers
* LightInfo pointers retain information for primary and secondary lighting
* GFXTextureObject pointers also aid in lighting, as well as texturing the object


RenderBinManager
=================

**RenderBinManager** manages and signals a main list of RenderInst objects.

RenderBinManager contains the variables and functions necessary for adding, processing, sorting, and clearing RenderInst objects. To get a closer look at RenderBinManager, open engine/source/renderInstance/renderBinManager.h and renderBinManager.cpp.

Most of the important management functionality is defined in the class, but you should notice a very important chunk of functionality missing: **rendering code**. RenderBinManager does have a rendering function::

	virtual void render( SceneState *state ) {}

But as you can see, we are not going to be directly using a RenderBinManager for rendering. It's important to know how the class's base functionality works, but we will get to the actual rendering code when we look at RenderBinManager's children.

This class lays the ground work, but the tangible rendering sub-managers derive from RenderBinManager: RenderMeshMgr, RenderObjectMgr, RenderTranslucentMgr, and so on. These are detailed further down in the sub-managers section. 

RenderPassManager
===================

The RenderPassManager could be considered the "top manager" when it comes to the rendering system. The responsibilities of this manager include:

* Declaring and organizing the various RIT: "R"ender "I"nstance "T"ypes

* Allocating a render instance for MeshRenderInst, ObjectRenderInst, and so on

* Adding, sorting, and rendering a list of RenderInst's per bin

* Memory allocation and deallocation for the RenderBinManagers

* Adding, sorting, and managing the various RenderBinManagers. The importance of this task is best shown in code

See the code initializing the rendering managers, initRenderManager.cs::

	// In game/core/scripts/client/renderManager.cs:
	function initRenderManager()
	{
	   // If we already have a script version of
	   // RenderPassManager (DiffuseRenderPassManager)
	   // do not proceed with this function
	   assert( !isObject( DiffuseRenderPassManager ), "initRenderManager() - DiffuseRenderPassManager already initialized!" );
	   
	   // Create a new RenderPassManager
	   new RenderPassManager( DiffuseRenderPassManager );
	
	   // Begin adding sub-managers
	   DiffuseRenderPassManager.addManager( new RenderPassStateBin() { renderOrder = 0.001; stateToken = AL_FormatToken; } );
	     
	   // We really need to fix the sky to render after all the 
	   // meshes... but that causes issues in reflections.
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr() { bintype = "Sky"; renderOrder = 0.1; processAddOrder = 0.1; } );
	   
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr()              { bintype = "Begin"; renderOrder = 0.2; processAddOrder = 0.2; } );
	   // Normal mesh rendering.
	   DiffuseRenderPassManager.addManager( new RenderMeshMgr()                { bintype = "Interior"; renderOrder = 0.3; processAddOrder = 0.3; } );
	   DiffuseRenderPassManager.addManager( new RenderTerrainMgr()             { renderOrder = 0.4; processAddOrder = 0.4; } );
	   DiffuseRenderPassManager.addManager( new RenderMeshMgr()                { bintype = "Mesh"; renderOrder = 0.5; processAddOrder = 0.5; } );
	   DiffuseRenderPassManager.addManager( new RenderImposterMgr()            { renderOrder = 0.56; processAddOrder = 0.56; } );
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr()              { bintype = "Object"; renderOrder = 0.6; processAddOrder = 0.6; } );
	     
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr()              { bintype = "Shadow"; renderOrder = 0.7; processAddOrder = 0.7; } );
	   DiffuseRenderPassManager.addManager( new RenderMeshMgr()                { bintype = "Decal"; renderOrder = 0.8; processAddOrder = 0.8; } );
	   DiffuseRenderPassManager.addManager( new RenderOcclusionMgr()           { bintype = "Occluder"; renderOrder = 0.9; processAddOrder = 0.9; } );
	     
	   // We now render translucent objects that should handle
	   // their own fogging and lighting.
	   
	   // Note that the fog effect is triggered before this bin.
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr(ObjTranslucentBin) { bintype = "ObjectTranslucent"; renderOrder = 1.0; processAddOrder = 1.0; } );
	         
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr()              { bintype = "Water"; renderOrder = 1.2; processAddOrder = 1.2; } );
	   DiffuseRenderPassManager.addManager( new RenderObjectMgr()              { bintype = "Foliage"; renderOrder = 1.3; processAddOrder = 1.3; } );
		DiffuseRenderPassManager.addManager( new RenderParticleMgr()            { renderOrder = 1.35; processAddOrder = 1.35; } );
	   DiffuseRenderPassManager.addManager( new RenderTranslucentMgr()         { renderOrder = 1.4; processAddOrder = 1.4; } );
	   
	   // Note that the GlowPostFx is triggered after this bin.
	   DiffuseRenderPassManager.addManager( new RenderGlowMgr(GlowBin) { renderOrder = 1.5; processAddOrder = 1.5; } );    
	   
	   // Resolve format change token
	   DiffuseRenderPassManager.addManager( new RenderPassStateBin(AL_FormatToken_Pop) { renderOrder = 1.6; stateToken = AL_FormatToken; } );
	}

The premise behind this chunk of code is simple. Calling DiffuseRenderPassManager "the manager of managers" seems appropriate. As the client is being initialized, initRenderManager() is called to create the rendering managers.

Using the .addManager(...) function, the RenderPassManager stores an internal list of RenderBinManagers. We have managers for Sky, Interiors, Lighting, Shadows, and so on. 

Sub-Managers
=============
As mentioned previously, the actual rendering managers are children of RenderBinManager. We are calling them sub-managers, since the RenderPassManager manages and maintains them. Each of these rendering sub-managers contains rendering code unique to its purpose, though multiple instantiations do occur to handle our various renderable Torque objects.


Let's go down a simplified list of these classes and their main purpose:

* **RenderObjectMgr** - This class is used for rendering more than any of the other sub-managers. This manager is responsible for rendering common objects that do not have a standard mesh.
	
	* Sky
	* Shadows
	* Water
	* Foliage
	* Shapebase

* **RenderMeshMgr** - This class is used for rendering mesh based objects such as interiors, TSMesh, and decals.

* **RenderTerrainMgr** - This class is used for rendering the terrain.

* **RenderRefractMgr** - Stock Torque 3D uses only one RenderRefractMgr. The name of the manager describes it well. This manager takes in RenderInst elements and checks to see if they have a refraction custom material. If this check succeeds, the element is maintained by the manager and makes use of the refraction rendering code.

* **RenderImposterMgr** - This is a special render manager for processing single billboard imposters typically generated by the tsLastDetail class.

* **RenderOcclusionMgr** - Used for performing occlusion queries on the scene.

* **RenderTranslucentMgr** - Stock Torque 3D uses only one RenderTranslucentMgr. This manager is a bit more complex than the previous ones described. A RenderInst element must meet a strict set of requirements to be managed by this class. If you look at RenderTranslucentMgr::addElement(...), you can see there are 3 main if(...) statements checking for translucent properties and appropriate render instance type. The actual render function is quite clean, and you can gain more insight about the class by reading through it.

* **RenderGlowMgr** - Just like the previous two managers, there is only one instance of RenderGlowMgr in stock Torque 3D. The name is pretty self-descriptive. This manager is responsible for accepting RenderInst elements that require rendering with a properly set up glow buffer.


Conclusion
============
The purpose of this document is to provide you with a basic understanding of the rendering management system used by Torque 3D. There is still much to be explained in the way of rendering flow, extending the system, and specific examples.

We've covered the basic renderable object instances, base class render managers, specialized rendering manager classes, and touched on some new subjects such as the RenderDelegate. (TODO - Internal Link)