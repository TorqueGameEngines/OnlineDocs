RenderDelegate
***************

Concept
========
The concept and functionality behind RenderDelgate gives you, the developer, a lot of flexibility when you are creating your own rendering objects. RenderDelgates are based on the system sending a signal, which is caught by an object's RenderDelegate. The RenderDelgate itself calls an object's render function.

Let's take a look at a few simple examples. 

SkyBox Example
================
The SkyBox object is a great example of a custom object that requires rendering. The class is derived from SceneObject, which does not have a rendering function. Open **engine/source/environment/skyBox.h**. If you scroll through the SkyBox class, you will find the declaration of its RenderDelegate::

	/// Our render delegate.
	void _renderObject( ObjectRenderInst *ri, SceneState *state, BaseMatInstance *mi );


Open skyBox.cpp (same directory), then locate the SkyBox::prepRenderImage(...) function. At the bottom of the function, Sky's RenderDelegate is bound. In the following code, read each line's comment to understand what is happening::

	// Create a render instance by asking the RenderPassManager for one
	ObjectRenderInst *ri = state->getRenderPass()->allocInst<ObjectRenderInst>();
	
	// Bind the SkyBox's rendering function to the renderDelegate
	ri->renderDelegate.bind( this, &SkyBox::_renderObject );
	
	// Set the Render Instance Type (RIT)
	ri->type = RenderPassManager::RIT_Sky;
	
	// Set the sorting keys
	ri->defaultKey = 10;
	ri->defaultKey2 = 0;
	
	// Add the render instance to the manager
	state->getRenderPass()->addInst( ri );


When binding, we are passing in the SkyBox class (this), and its rendering function. Let's say the rendering function had a different name, such as _renderSky::

	ri->renderDelegate.bind( this, &SkyBox::_renderSky);

What we are doing is preparing the SkyBox class to receive a render signal and act on it. One of our manager's (which we will discuss in a minute), will parse through all of its contained objects. When it comes across SkyBox, it will send a render signal to the class. It doesn't care about the name of the rendering function, it just tells the object to render with certain information::

	void SkyBox::_renderObject( ObjectRenderInst *ri, SceneState *state, BaseMatInstance *mi )
	{
	   ...
	
	   GFXTransformSaver saver;  
	   GFX->setVertexBuffer( mVB );         
	      
	   MatrixF worldMat = MatrixF::Identity;
	   worldMat.setPosition( state->getCameraPosition() );
	
	   SceneData sgData;
	   sgData.init( state );
	   sgData.objTrans = &worldMat;
	   
	   ...

RenderObjectExample
=====================
No doubt, if you are reading through these engine docs you are most likely a programmer. Regardless of your experience, diving head first into Torque 3D's source code can be overwhelming. If you need a very simple RenderDelegate example, you do not have to dig through the entire Player->ShapeBase->etc hierarchy.

Instead, an example class was written specifically for demonstrating a basic RenderDelegate: **RenderObjectExample**. The source files, renderObjectExample.h and .cpp, are found in **engine/source/T3D/examples**. Every line has been heavily commented to explain the purpose of the class.

RenderObjectExample has even been exposed to script and the World Editor. You can add a RenderObjectExample to your scene while debugging the engine, and go through each line of rendering code step by step. 

RenderDelegate vs Other Render Methods
========================================

A render object (using a RenderDelegate) handles its own rendering by submitting itself as an ObjectRenderInst along with a delegate for its render() function. However, the preferred rendering method in the engine is to submit a MeshRenderInst along with a Material, vertex buffer, primitive buffer, and transform and let the RenderMeshMgr handle the actual rendering.

With that in mind, you may be wondering why you should ever use a RenderDelegate when some of the most important classes do not use it: Player, Item, ShapeBase, etc. While writing the actual rendering code can be complex, deciding on which method to use is simple.

When you have access to an object's 3D geometry (mesh) and material (textures and texture properties), you might as well make use of the mesh and shape rendering systems. This includes anything using COLLADA and .DTS.

If your new object does not use 3D geometry, you should look into using the RenderDelegate system. More importantly, integration of 3rd party technologies that handle their own rendering, such as SpeedTree or Scaleform, should definitely use RenderDelegates. 

* SpeedTree - http://www.speedtree.com/
* Scaleform - http://web.archive.org/web/20111026114129/http://www.scaleform.com/

Conclusion
============
This goal of this document was to provide you with an introduction and specific examples of the RenderDelegate system. Should you decide to create your own custom classes which require object rendering, please refer back to this doc.

Remember, if your new object has a 3D mesh and makes use of the material system, you are encouraged to follow the example set by RenderMeshExample and RenderObjectExample. If you are implementing a very custom object, or a are integrating a 3rd party product with its own rendering, using a RenderDelegate will be much easier. 