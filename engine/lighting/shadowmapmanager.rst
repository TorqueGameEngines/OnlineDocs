ShadowMapManager
*****************

**ShadowMapManager Class Reference**

.. cpp:function:: activate()

	Called when the ShadowMapManager should become active. If the ShadowMapManager is unable to retrieve a SceneManager through the internal method getSceneManager then it will return a console error saying it was unable to active the ShadowMapManager and return out of the function. If it is able to retrieve the SceneManager then it will notify the SceneManager of its onPreRender function and turn its self active.
	
	Syntax::

		activate()
	
	:return: no return value.

	Examples::
	
		// Called from within the AdvancedLightManager::activate, SHADOWMGR is a #define
		// of the ShadowMapManager::instance() function.
		SHADOWMGR->activate();

.. cpp:function:: deactivate()

	Called when the ShadowMapManager should be decactivated. The ShadowMapManager will notify the SceneManger to remove its onPreRender function from the pre-render signal, clean up the shadow texture memory and makes its self no longer active.
	
	Syntax::

		deactivate()
	
	:return: no return value.

	Examples::
	
		// Called from within the AdvancedLightManager::deactivate, SHADOWMGR is a #define
		// of the ShadowMapManager::instance() function.
		SHADOWMGR->deactivate();
		
.. cpp:function:: setLightShadowMapForLight( LightInfo * ) 

	Looks up the shadow map for the light then sets it.
	
	Syntax::

		setLightShadowMapForLight(LightInfo *light ) 
		
	:param light: Will use this variable to look up the potential ShadowMapParams.
	
	:return: no return value.

	Examples::
	
		// Set light holds the active shadow map.       
		mShadowManager->setLightShadowMapForLight( sunLight );
		
.. cpp:function:: setLightShadowMap( LightShadowMap *)  

	Sets the current shadowmap (used in setLightInfo/setTextureStage calls).
	
	Syntax::

		setLightShadowMap(LightShadowMap *lm )
		
	:param lm: The current shadow map that will be assigned to the classes internal "LightShadowMap *mCurrentShadowMap" variable.
	
	:return: no return value.

	Examples::
	
		// While traversing the shadow maps in "ShadowMapPass::render".
		LightShadowMap *lsm = shadowMaps[i];
		mShadowManager->setLightShadowMap( lsm );