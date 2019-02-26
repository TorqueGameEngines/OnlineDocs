Using the LightManager Class
******************************

Introduction
=============
The LightManager is one of the most comprehensive classes in the lighting system. LightManager is defined as a singleton and provides the user with the ability to register global lights, compute static lighting, register special types of lights and return the active LightManager. The active LightManager can be accessed at any time via the static function "getActiveLM", or with the #define "LIGHTMGR". Even though it has a wealth of functionality, on its own it can not operate and is the base class to BasicLightManager and AdvancedLightManager. It contains four key functions that need to be overridden for its subclasses to be initialized::

	bool isCompatible() const

Should return true if this light manager is compatible with the current platform and GFX device::

	void setLightInfo( ProcessedMaterial *pmat, const Material *mat, const SceneGraphData &sgData, 
    	const SceneState *state, U32 pass, GFXShaderConstBuffer *shaderConsts )

Sets shader constants / textures for LightInfo's::

	void setTextureStage( const SceneGraphData &sgData, const U32 currTexFlag, const U32 textureSlot, 
    	GFXShaderConstBuffer *shaderConsts, ShaderConstHandles *handles )

Allows he ability to set textures during the Material::setTextureStage call, return true if it has done work::

	void _addLightInfoEx( LightInfo *lightInfo )

Attaches any LightInfoEx data for the light manager to the light info object. 

Example Uses
=============
The Sun class will need to have a LightInfo object created for it. As a result, in its constructor it will create a LightInfo object by calling the static function createLightInfo(LightInfo *) to allocate a new lightInfo object for its use. Inside of the LightManager::createLightInfo(LightInfo *) function the allocated LightInfo will then be added to all of the LightManager's currently allocated light objects by traversing the LightManagerMap returned by the member function _getLightManagers(). Finally, the function will return the pointer to the allocated LightInfo object that is created.

After the Sun class creates the light info via "LightManager::createLightInfo()" the last thing it will do is set the type of light that it is (with LightInfo::setType). It sets the type to "LightInfo::Vector", or commonly referred to as "directional".

Other examples of classes using createLightInfo are the following. If the type of light is not specified after the LightInfo is created, it is "vector" by default.

* class Projectile
Sets the type to LightInfo::Point

* class Explosion
Does not set a LightInfo after it is created in the constructor, so by default it users Point::Vector. However, later in the "Explosion::onAdd" function it will set the type to a LightInfo::Point if the Explosion's internal information calls for it.

* class ScatterSky
Will set the type to LightInfo::Vector

Compatibility
==============
As mentioned in the section above, the LightManager contains the pure virtual function "bool isCompatible()", which is basically self explanatory. If the subclass detects that the graphics card does not meet the requirements that it needs, it will return false. This compatibility function will be called when a light manager is assigned to the SceneGraph. When the isCompatible function is called via "bool SceneGraph::_setLightManager" and it detects that the function did not return true, it will not assign the LightManager to the SceneGraph.

Activating and Deactivating the LightManager
=============================================
The LightManager will provide the function "activate" that can be overridden by its subclasses, however, the subclasses should call the LightManager::activate function from any override that is written. The activate function will ensure that the SceneManager passed in is valid, the light manager currently is not active and that no other light manager is active.

Using the Active LightManager
==============================
The active LightManager is available throughout the code base via the static function "LightManager *getActiveLM()", or the most commonly used #define "LIGHTMGR". The LIGHTMGR definition is used throughout the code base to utilize the fact that the LightManager is defined as a singleton.

**Example Uses**::

	WaterBlock::setupVertexBlock(U32, U32, U32)

WaterBlock uses LIGHTMGR to retrive the Sun light and obtain the direction it is pointing at::

	CloudLayer::renderObject(ObjectRenderInst *, SceneState *, BaseMatInstance *)

CloudLayer uses LIGHTMGR during rendering to help obtain the ambient color of the sun::

	GuiObjectView::renderWorld(const RectI&)

GuiObjectWorld uses LIGHTMGR to unregister all of the lights via "LIGHTMGR->unregisterAllLights()". 

AdvancedLightManager
=====================
The AdvancedLightManager is a singleton, meaning that there is always an instance available to grab and that the class is created at the runtimes initialization. In addition to overriding the pure virtual functions from its base class, LightMananger, it will override the activate and deactivate functions. It will also overrides the way global lights are registered and unregistered. As previously mentioned in the Overview section, the AdvancedLightManager requires the graphics card to support shader model 3.0. Additional functionality over the base LightManager is the ability to look for a LightShadowMap per SimObject (if the object can cast to an ISceneLight properly).

BasicLightManager
==================
The BasicLightManager at its base is like the AdvancedLightManager, meaning that it is a singleton, that there is always an instance available, and that the object is created at the runtime's initialization. In addition to overriding the pure virtual functions from its base class, LightMananger, it will override the activate and deactivate functions. It will also create the static method "getShadowFilterDistance" to help filter out shadows. For an example of this, take a look at the function "ProjectedShadow::_renderToTexture". 
