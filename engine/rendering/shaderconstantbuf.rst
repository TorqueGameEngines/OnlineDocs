Shader Constant Buffers
************************

Concept
========
Much like state blocks, shader constant buffers help reduce the amount of rendering code you have to write. This concept is quite similar to DirectX 10's version of constant buffers, which share a similar purpose:


Quoted concepts from DirectX HLSL MSDN::

	A constant buffer, or shader constant buffer, is a 
	buffer that contains shader constants.
	
	Conceptually, it looks just like a 
	single-element vertex buffer. 
	
	A constant buffer is a specialized buffer resource 
	that is accessed like a buffer. 
	
	A buffer resource is designed to minimize the 
	overhead of setting shader constants.


Technical Description
========================
A shader constant buffer is just a block of memory (or an object) that contains the constants that a shader needs to have bound. Specifically, they buffer a collection of string/value pairs that are sent to a shader. They are allocated by the shader itself because the shader may have information about layout that no other part of the system will know about.


You can look up handles by shader constant name. This removes the need for a static shader constant-to-slot mapping and also allows us to do some CPU side optimizations. Under the hood, the string/value pair is mapped to a block of memory that can be handed to a shader with one call. 

Source Code
============
We are going to take a light tour of the engine code that makes up the GFXShaderConstBuffer system. Let's start by opening *engine/source/gfx/gfxShader.h*. Toward the top of this header, you will see a struct and two base classes that make up this system::

	/// Instances of this struct are returned GFXShaderConstBuffer
	struct GFXShaderConstDesc {...};
	
	
	/// This is an opaque handle used by GFXShaderConstBuffer 
	/// clients to set individual shader constants.
	/// Derived classes can put whatever info they need into here, 
	/// these handles are owned by the shader constant buffer
	/// (or shader).  Client code should not free these.
	class GFXShaderConstHandle {...};
	
	
	/// GFXShaderConstBuffer is a collection of 
	/// string/value pairs that are sent to a shader.
	/// Under the hood, the string value pair is 
	/// mapped to a block of memory that can
	/// be blasted to a shader with one call (ideally)
	class GFXShaderConstBuffer {...}

It should be obvious by the amount of pure virtual function declarations that GFXShaderConstHandle and GFXShaderConstBuffer are meant to have children. Both GFXD3D9 and GFXGL will get their own versions of shader constant buffers. In this file, there is not much you can learn from GFXShaderConstHandle. However, you might want to scan GFXShaderConstBuffer.

It is derived from StrongRefBase and GFXResource. Being a StrongRefBase object, the stateblock will exist as long as the reference exists. When all of the strong references to the stateblock go away, it is permanently deleted. It is treated as a GFXResource since our GFX system needs to track its resources owned by a particular device.

The virtual function declarations should give you insight on how we are setting up the future child functionality. We have almost twenty overloaded functions named **set(...)**. Each one takes in a GFXShaderConstHandle* and a constant. The handles contains the name of the constant, which should be a name contained in the array returned in getShaderConstDesc. 

It is very important that you remember what GFXShaderConstBufferRef is:

In engine/source/gfx/gfxShader.h::

	typedef StrongRefPtr<GFXShaderConstBuffer> GFXShaderConstBufferRef;

GFXShaderConstBufferRef is like a pointer (reference) to GFXShaderConstBuffer, with a few key differences. A few paragraphs back I mentioned GFX tracking its resources and references, and this is one of the ways it does so. This is a **referenced counted**, object template pointer class (quite descriptive!). Heavy emphasis on the **referenced counted**. 

If you open *engine/source/gfx/gl/gfxGLShader.h*, you can see how we have set up our OpenGL version of a constant shader buffer.

**We have our child class declaration**::

	class GFXGLShaderConstBuffer: public GFXShaderConstBuffer{...}

**The GL version contains an activation function**::

	/// Called by GFXGLDevice to activate this buffer.
	void activate();

**The class even keeps track of the shader that creates the buffer**::

	WeakRefPtr<GFXGLShader> mShader;

	/// Return the shader that created this buffer
	virtual GFXShader* getShader() { return mShader; }

Of course, the multiple virtual void set(...) functions get defined as well, but in the gfxGLShader.cpp file. The base relationship you should remember is a GFX shader creates and uses a shader constant buffer, while the constant buffer keeps track of its owner and sets the actual constants. 

Engine Example
================
As for an engine example, I'll start with a generic chunk of code:

**We will set up our constant buffer and handle once**::

	// Setup code
	GFXShaderConstBufferRef myBuff = shader->allocConstBuffer();
	GFXShaderConstHandle* myHandle = shader->getShaderConstHandle("$diffuseColor");

**Now you can set the constant buffer**::

	// Render code
	myBuff->set(myHandle, myConst);
	GFX->setShaderConstBuffer(myBuff);

Now that you see the basic code concept, let's examine an existing constant buffer in the engine. The CloudLayer class handles its shader constant buffer internally. Open **engine/source/environment/cloudLayer.cpp**. Scroll down until you see the following function::

	bool CloudLayer::onAdd(){...}

Further into the function, around line 92, you can see where the internal GFXShaderConstBufferRef (mShaderConsts) is allocated::

	// Create ShaderConstBuffer and Handles
	mShaderConsts = mShader->allocConstBuffer();

The GFXShaderConstHandle pointers are internal members belonging to the CloudLayer class::

**In engine/source/environment/cloudLayer.h**::

	GFXShaderConstHandle *mModelViewProjSC; 
	GFXShaderConstHandle *mAmbientColorSC;
	GFXShaderConstHandle *mSunColorSC;
	GFXShaderConstHandle *mSunVecSC;
	GFXShaderConstHandle *mTexOffsetSC[3];
	GFXShaderConstHandle *mTexScaleSC;
	GFXShaderConstHandle *mBaseColorSC;    
	GFXShaderConstHandle *mCoverageSC;  
	GFXShaderConstHandle *mEyePosWorldSC;


Back in the cloudLayer.cpp, these handles are set after the buffer has been allocated::

	mModelViewProjSC = mShader->getShaderConstHandle( "$modelView" );
	mEyePosWorldSC = mShader->getShaderConstHandle( "$eyePosWorld" );
	mSunVecSC = mShader->getShaderConstHandle( "$sunVec" );
	mTexOffsetSC[0] = mShader->getShaderConstHandle( "$texOffset0" );
	mTexOffsetSC[1] = mShader->getShaderConstHandle( "$texOffset1" );
	mTexOffsetSC[2] = mShader->getShaderConstHandle( "$texOffset2" );
	mTexScaleSC = mShader->getShaderConstHandle( "$texScale" );
	mAmbientColorSC = mShader->getShaderConstHandle( "$ambientColor" );
	mSunColorSC = mShader->getShaderConstHandle( "$sunColor" );
	mCoverageSC = mShader->getShaderConstHandle( "$cloudCoverage" );
	mBaseColorSC = mShader->getShaderConstHandle( "$cloudBaseColor" );


The actual setting of the shader data, constant buffer, and stateblock does not happen until further down in the source file. If you scroll down to around line 264, you will find the rendering function for CloudLayer::

	void CloudLayer::renderObject( ObjectRenderInst *ri, SceneState *state, BaseMatInstance *mi ){...}

On line 276, GFX takes over and performs the "set" code::

	GFX->setShader( mShader );
	
	// HERE WE SET THE SHADER CONSTANT BUFFER
	GFX->setShaderConstBuffer( mShaderConsts );
	
	GFX->setStateBlock( mStateblock );


Script Example
===============
Using shader constant buffers in TorqueScript is a little different than in the engine code. At this time, most game developers know about the SSAO (Screen Space Ambient Occlusion) rendering technique. Torque 3D has a SSAO solution, which is defined in TorqueScript.

SSAO is a PostEffect, so it must be defined as such. Locate and open **Examples/FPS Example/game/core/scripts/client/postFx/ssao.cs**. The effect is declared using the following code (reduced to just show the declaration):: 

	singleton PostEffect( SSAOPostFx ){...};

In the CloudLayer example, I mentioned the class contained internal GFXShaderConstHandle pointers as member variables. In TorqueScript, SSAO uses scoped global variables::

	// The small radius SSAO settings.
	$SSAOPostFx::sRadius = 0.1;
	$SSAOPostFx::sStrength = 6.0;
	$SSAOPostFx::sDepthMin = 0.1;
	$SSAOPostFx::sDepthMax = 1.0;
	$SSAOPostFx::sDepthPow = 1.0;
	$SSAOPostFx::sNormalTol = 0.0;
	$SSAOPostFx::sNormalPow = 1.0;

	// The large radius SSAO settings.
	$SSAOPostFx::lRadius = 1.0;
	$SSAOPostFx::lStrength = 10.0;
	$SSAOPostFx::lDepthMin = 0.2;
	$SSAOPostFx::lDepthMax = 2.0;
	$SSAOPostFx::lDepthPow = 0.2;
	$SSAOPostFx::lNormalTol = -0.5;
	$SSAOPostFx::lNormalPow = 2.0;

These variables are used when setting the buffer. As a script object, SSAOPostFx can have member functions. An important function to define for PostEffect objects is **setShaderConsts(%this)**. If a PostEffect object, such as SSAOPostFx, has this function defined, it will be called by the engine automatically.

If you scroll down to the function, you can see how it sets the shader constant buffer::

	function SSAOPostFx::setShaderConsts(%this )
	{      
	  %this.setShaderConst( "$overallStrength", $SSAOPostFx::overallStrength );
	
	   // Abbreviate is s-small l-large.   
	   
	  %this.setShaderConst( "$sRadius",      $SSAOPostFx::sRadius );
	  %this.setShaderConst( "$sStrength",    $SSAOPostFx::sStrength );
	  %this.setShaderConst( "$sDepthMin",    $SSAOPostFx::sDepthMin );
	  %this.setShaderConst( "$sDepthMax",    $SSAOPostFx::sDepthMax );
	  %this.setShaderConst( "$sDepthPow",    $SSAOPostFx::sDepthPow );
	  %this.setShaderConst( "$sNormalTol",   $SSAOPostFx::sNormalTol );
	  %this.setShaderConst( "$sNormalPow",   $SSAOPostFx::sNormalPow );
	   
	  %this.setShaderConst( "$lRadius",      $SSAOPostFx::lRadius );
	  %this.setShaderConst( "$lStrength",    $SSAOPostFx::lStrength );
	  %this.setShaderConst( "$lDepthMin",    $SSAOPostFx::lDepthMin );
	  %this.setShaderConst( "$lDepthMax",    $SSAOPostFx::lDepthMax );
	  %this.setShaderConst( "$lDepthPow",    $SSAOPostFx::lDepthPow );
	  %this.setShaderConst( "$lNormalTol",   $SSAOPostFx::lNormalTol );
	  %this.setShaderConst( "$lNormalPow",   $SSAOPostFx::lNormalPow );
	   
	  %blur =%this->blurY;
	  %blur.setShaderConst( "$blurDepthTol", $SSAOPostFx::blurDepthTol );
	  %blur.setShaderConst( "$blurNormalTol", $SSAOPostFx::blurNormalTol );   
	   
	  %blur =%this->blurX;
	  %blur.setShaderConst( "$blurDepthTol", $SSAOPostFx::blurDepthTol );
	  %blur.setShaderConst( "$blurNormalTol", $SSAOPostFx::blurNormalTol );   
	   
	  %blur =%this->blurY2;
	  %blur.setShaderConst( "$blurDepthTol", $SSAOPostFx::blurDepthTol );
	  %blur.setShaderConst( "$blurNormalTol", $SSAOPostFx::blurNormalTol );
	      
	  %blur =%this->blurX2;
	  %blur.setShaderConst( "$blurDepthTol", $SSAOPostFx::blurDepthTol );
	  %blur.setShaderConst( "$blurNormalTol", $SSAOPostFx::blurNormalTol );         
	}


Conclusion
===========
The intent of this document was to provide you with a strong introduction to GFX shader constant buffers. There are various examples scattered throughout the code, so you might want to spend some more time browsing through the code and comments.

Should you decide to create your own custom classes with renderable objects, remember to check this document again and see how you can use constant buffers in your code. The optimization is well worth the learning curve. 