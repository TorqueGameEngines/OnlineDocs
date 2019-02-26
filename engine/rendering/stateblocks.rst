Stateblocks
************

Concept
========
The purpose of GFXStateblocks is quite simple: an entire rendering state is contained in one object, and you are able to set the rendering state with one call. If you've written rendering code before, you may have written code similar to this before::

	// Enable Blending
	glEnable (GL_BLEND);
	
	// Set The Blend Mode		
	glBlendFunc (GL_SRC_ALPHA ,GL_ONE_MINUS_SRC_ALPHA)


What if you need to setup that kind of rendering state more than just once? GFXStateblocks allow you to wrap that up into the following::

	GFX->setStateBlock(myState);


There's a little more tech and setup involved, but the above example should be enough to encourage you to read on and use this concept in your own project. 

Technical Description
========================
Using GFXStateblocks allows you to pre-generate your rendering states, which is going to save you time, cleanup your code, apply modern rendering techniques, and give you more control over your game's rendering from the engine **as well as script**. When combined with CustomMaterials, the material definitions in script need less custom engine support.

Stateblocks are created by filling out a GFXStateBlockDesc structure and calling GFX->createStateBlock on it. This returns a GFXStateBlockRef, which is a reference-counted GFXStateBlock. This is essentially a GFXResource, just like a texture. Then you use a stateblock by calling GFX->setStateBlock and passing the state block in.

Using a stateblock fully defines a render state, which completely does away with all concepts canonical. This is actually a good thing as this will reduce bugs introduced because a state was not properly cleaned up before exiting. 

Source Code
=============
It might help if we tour the engine code, so you can get some concrete code samples in front of your eyes. Start by opening **gfxStateBlock.h** and **gfxStateBlock.cpp**, both of which are found in engine/source/gfx. Let's browse the header (.h) first. All four major declarations are important here::

	struct GFXSamplerStateDesc {...};
	
	struct GFXStateBlockDesc {...};
	
	class GFXStateBlock {...};
	
	typedef StrongRefPtr<GFXStateBlock> GFXStateBlockRef;


GFXSamplerStateDesc
====================
The GFXSamplerStateDesc struct contains variables and methods to identify the texture object used for each texture lookup. You'll find texture arguments for color, alpha, min/mag/mip filter, and address modes. A solid example of how this structure is used can be found in the gfxD3D9StateBlock::activate(...) function.

Inside this method, a GFXSamplerStateDesc variable (ssd) is set to one of the stateblocks internal samplers. The function performs a check to see how OpenGL handles the GL_TEXTURE_2D variable:

Abbreviated code from GFXGLStateBlock::activate(...), found in engine/source/gfx/gl/gfxGLStateBlock.cpp ::

	const GFXSamplerStateDesc ssd = mDesc.samplers[i];
	
	switch (ssd.textureColorOp)
	{
	case GFXTOPDisable:
	   if(!tex)
	      break;
	   glDisable(GL_TEXTURE_2D);
	   updateTexParam = false;
	   break;
	}


GFXStateBlockDesc
===================
**GFXStateBlockDesc** defines a render state, which is then used to create a GFXStateBlock instance. If you look through the structure, you will read through some common render state ops and references: blending (source/destination/operation), depth buffer (z buffer enable/bias/definition), color writes (write red/blue/green/alpha), and so on.

A nifty concept applied through GFXStateBlockDescr is the combining state block descriptions. This is done so through the::addDesc(...) function::

	/// Adds data from desc to this description, uses *defined
	parameters in desc to figure out what blocks of 
	state to actually copy from desc.
	void addDesc(const GFXStateBlockDesc& desc);


GFXStateBlock
===============
The base GFXStateBlock class looks very bare. It is derived from StrongRefBase and GFXResource. Being a StrongRefBase object, the stateblock will exist as long as the reference exists. When all of the strong references to the stateblock go away, it is permanently deleted. It is treated as a GFXResource since our GFX system needs to track its resources owned by a particular device.


There are only 4 functions in this base class, and they are all virtual. This is due to the fact that we have multiple graphical APIs to support, which means we are going to have GFXStateBlocks for DirectX and OpenGL:

* GFXD3D9StateBlock
* GFXGLStateBlock

Of course, we have our null device stateblock (GFXNullStateBlock), but you will not actually need to use that for any rendering. The other GFX devices will have their own implementation of stateblocks. In fact, let's take a look at the GL implementation. Open engine/source/gfx/gl/gfxGLStateBlock.h. The class we are looking at is **GFXGLStateBlock**.

Within this function we have a working interface (constructor and destructor), a function called by OpenGL to activate the stateblock (::activate), and a tangible GFXStateBlockDesc member variable (mDesc). The activate function definition can be found in **gfxGLStateBlock.cpp** ::

	GFXGLStateBlock::activate(const GFXGLStateBlock* oldState)
	{
	   // Internal code not shown
	}

It is heavily commented and has a very important warning at the beginning. It is highly recommended you read through the comments and code to get a better understanding of how the stateblock is set up. 

GFXStateBlockData
===================
Two very important classes we need to take a look at is the GFXStateBlockData class and GFXSamplerStateData class, found in engine/source/gfx/sim/gfxStateBlockData.h/.cpp. The class definitions and their comments are quite descriptive::

	/// Allows definition of render state via script, 
	basically wraps a GFXStateBlockDesc
	class GFXStateBlockData: public SimObject
	
	/// Allows definition of sampler state via script, 
	basically wraps a GFXSamplerStateDesc
	class GFXSamplerStateData: public SimObject


As you read, these classes allow us to create GFXStateBlock and GFXSamplerState descriptions in TorqueScript. This means you are able to utilize a lot more custom shader and rendering work without being as reliant on custom engine code. You should definitely look through the::initPersistFields() functions for each class. You will notice the various references and ops that make up a render state are exposed. 

Engine Example
================
We are going to use a very simple engine example for showing how GFXStateBlocks are created and used. Start by opening *engine/source/interior/interior.h/.cpp*. When we use debug rendering, we are able to see certain aspects of an interior that are normally invisible to a player. One such aspect would be the rendering of portals.

In the Interior class, we have defined multiple stateblock references. Let's look at one that affects our portal rendering::

	GFXStateBlockRef mInteriorDebugPortalSB;

Ok! We have our stateblock reference, but it still needs some information. Go into Interior.cpp, and scroll down to the prepForRendering function around line 343::

	bool Interior::prepForRendering(const char* path)
	{
	     // Previous and remaining code not shown
	
	     mInteriorDebugPortalSB = GFX->createStateBlock(sh);
	
	}

This line of code shows we have initialized our stateblock reference, but what device does so? We haven't seen any OpenGL or DirectX code anywhere, so how can we know if we are using a GFXGLStateBlock or not? This is where GFX takes control. **GFX->createStateBlock(...)** takes in a fully initialized GFXStateBlockDesc reference. 

GFX then proceeds to set up the hash value and search for existing stateblocks. If the stateblock we need does not exist, it calls **createStateBlockInternal**. This function drills into our platform's device, so we have a GFXGLDevice::createStateBlockInternal and a GFXD3D9Device::createStateBlockInternal.

When creating a GFXStateBlock in script, quite a few things happen for you automatically. However, when you are in the engine there are a few "Gotchas" you have to remember. **When you create a GFXStateBlock in the engine, you must call setStateBlock before you use it!**


**Called in Interior::debugRenderPortals()**::

	GFX->setStateBlock(mInteriorDebugPortalSB);


A simple, more generic engine example would be this::

  // Setup code, done once
  GFXStateBlockDesc desc;
  desc.setBlend(true, GFXSrcAlpha, GFXInvSrcAlpha);
  GFXStateBlockRef myState = GFX->createStateBlock(desc);

  // Render time code
  GFX->setStateBlock(myState);

Script Example
================
Earlier, I mentioned using shader data and GFXStateBlocks together in script. We have provided you with a couple of examples. Open Examples/FPS Example/game/core/scripts/client/postFX.cs. This file contains multiple GFXStateBlockData and ShaderData definitions. First, we focus on the default stateblock::

	singleton GFXStateBlockData( PFX_DefaultStateBlock )
	{
	   zDefined = true;
	   zEnable = false;
	   zWriteEnable = false;
	      
	   samplersDefined = true;
	   samplerStates[0] = SamplerClampLinear;
	};


The above code demonstrates how to declare a GFXStateBlock in TorqueScript using the exposed Console Object, **GFXStateBlockData**. In this example, we define depth sorting and handle linear clamping. We can then use this stateblock in a PostEffect definition::

	singleton PostEffect( BL_ShadowFilterPostFx )
	{
	   requirements = "";
	
	   shader = BL_ShadowFilterShader;
	   stateBlock = PFX_DefaultStateBlock;
	   targetClear = "PFXTargetClear_OnDraw";
	   targetClearColor = "0 0 0 0";
	   texture[0] = "$inTex";
	   target = "$outTex";   
	};


A GFXStateBlockData definition can also be used in the creation of a separate stateblock, as shown below::

	singleton GFXStateBlockData( LightRayStateBlock: PFX_DefaultStateBlock )
	{
	   samplersDefined = true;
	   samplerStates[0] = SamplerClampLinear;
	   samplerStates[1] = SamplerClampLinear;     
	};

Essentially, we wanted the exact same rendering state for our two post processing effects. Instead of having to modify our engine code (twice), we can define our stateblock in script (once) and use it multiple times. 

Conclusion
============
There is a lot to learn about GFXStateBlocks. The intent of this article was to give you a strong introduction on the purpose, engine structure, and examples of how to use this new system. As you develop new shaders, look for ways you can save yourself time and headaches by using GFXStateBlocks. 