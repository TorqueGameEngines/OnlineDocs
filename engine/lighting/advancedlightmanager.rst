AdvancedLightManager
====================
**AdvancedLightManager Class Reference**

.. cpp:function:: getLightBinManager() 

	 Will return the lightBinManager for this light manager. 
	
	Syntax::

		getLightBinManager(); 
	
	:return: ``AdvancedLightBinManager *`` The lightBinManager member variable in AdvancedLightManager.

	Examples::
	
		lightmgr->getLightBinManager()
		
.. cpp:function:: isCompatible() 

	 Checks to make sure that the graphics card is compatible with the current pixel shader version that is needed. Currently at least 3.0 is needed.
	
	Syntax::

		isCompatible(); 
	
	:return: No return value.

	Examples::
	
		// Make sure its valid... else fail!
		if ( !lm->isCompatible() )
			return false;
			
.. cpp:function:: activate( SceneGraph *) 

	 In addition to calling its base classes active(SceneGraph*), it will activate the Shadow Manager and create the AdvancedLightBinManager. It will also setup the Render Prepass Manager and register the feature as an AdvancedLightingFeature.
	
	Syntax::

		activate( SceneGraph *sceneManager); 
		
	:param SceneGraph*: The SceneGraph to activate lighting for.
	
	:return: ``SceneGraph *`` The SceneGraph that will be used to create lighting features.

	Examples::
	
		// From the engine function "resetLightManager"
		LIGHTMGR->activate( LIGHTMGR->getSceneManager());
		
.. cpp:function:: deactivate() 

	 Will remove all the objects from the AdvancedLightBinManager and the PrePassRenderBin, then set them to ``NULL``. It will deactivate the Shadow Manager, unregister all the advanced lighting features and then finally send a trigger to let everyone know the LightManager has been deactivated.
	
	Syntax::

		deactivate()  
	
	:return: No return value.

	Examples::
	
		if (mLightManager)
			mLightManager->deactivate();

.. cpp:function:: registerGlobalLight( LightInfo *, SimObject * ) 

	 In addition to calling ``LightManager::registerGlobalLight``, it will add the light to the AdvancedLightBinManager member variable if the AdvancedLightBinManager is created and the light type is a ``LightInfo::Point`` or ``LightInfo::Spot``.
	
	Syntax::

		registerGlobalLight(LightInfo *light, SimObject *obj ) 

	:param type: The light to be registered to mRegisteredLights.
	:param light: Not used.
	
	:return: No return value.

	Examples::
	
		// From inside of Item::registerLights
		lightManager->registerGlobalLight( mLight, this );			

.. cpp:function:: unregisterAllLights() 

	 In addition to calling LightManager::unregisterAllLights, it will clear the AdvancedLightBinManager if it has been created.
	
	Syntax::

		unregisterAllLights() 

	:return: No return value.

	Examples::
	
		// Unregister all the lights in the light manager.
		LIGHTMGR->unregisterAllLights();
		
.. cpp:function:: setLightInfo( ProcessedMaterial *, const Material *, const SceneGraphData &, const SceneState *, U32, GFXShaderConstBuffer * ) 

	 Will check to make sure that the SceneGraphData is not PrePassBin, if it is then it will return out immediately. If it is not, then it will update the constants for the GFXShaderConstBuffer passed in.
	
	Syntax::

		setLightInfo(ProcessedMaterial *pmat, Material *mat, const SceneGraphData &sgData, SceneState *state, U32 pass, GFXShaderConstBuffer *shaderConsts ) 

	:param pmat: Not used.
	:param mat: Not used.
	:param sgData: Will be used to ensure rendering is not being done from the PrePassBin and also to update light constants by a call to ``_update4LightConsts(...)``.
	:param state: While setting information to "shaderConsts" it will be used to obtain the camera's transform.
	:param pass: Not used.
	:param shaderConsts: Will be used to obtain the LightingShaderConstants and to the call to ``_update4LightConsts(...)``. It will also have its "set" function called to set the shader constant for "ViewToLightProj".
	
	:return: No return value.

	Examples::
	
		// From inside of ProcessedShaderMaterial::setSceneInfo
		LIGHTMGR->setLightInfo( this, mMaterial, sgData, state, pass, shaderConsts );
		
.. cpp:function:: setTextureStage( const SceneGraphData &sgData, const U32 currTexFlag, const U32 textureSlot, GFXShaderConstBuffer *shaderConsts, ShaderConstHandles *handles ) 

	 Will assign a Shadowmap if it exists. It will grab the ShadowMap via the LightingShaderContants obtained via the shaderConsts passed in.
	
	Syntax::

		setTextureStage(const SceneGraphData &sgData, const U32 currTexFlag, const U32 textureSlot, GFXShaderConstBuffer *shaderConsts, ShaderConstHandles *handles ) 

	:param sgData: Used to obtain ShadowMapParams.
	:param currTexFlag: Depending on the currTexFlag the texture will be set differently to the GFXDevice.
	:param textureSlot: Not Used.
	:param shaderConsts: Used to obtain the LightingShaderConstants via getLightingShaderConstants(...).
	:param handles: Not used.
	
	:return: No return value.

	Examples::
	
		// From inside of ProcessedCustomMaterial::setTextureStages
		lm->setTextureStage(sgData, currTexFlag, i, shaderConsts, handles )
		
.. cpp:function:: getSphereMesh( U32 &, GFXPrimitiveBuffer *& ) 

	 Will return a vertex buffer handled filled out by a SphereMesh (mSphereGeometry), along with set the variables passed in. If the SphereMesh (mSphereGeometry) is not created by the time this function is called, it will create the sphere mesh (mSphereGeometry) in addition to returning it.
	
	Syntax::

		getSphereMesh(U32 outNumPrimitives, GFXPrimitiveBuffer *&outPrimitives )  

	:param outNumPrimitives: Will be set to the number of polygons for the SphereMesh.
	:param outPrimitives: Will always be set to NULL.
	
	:return: ``GFXVertexBufferHandle<AdvancedLightManager::LightVertex>`` Used for the vertex buffer, typically for a LightBinEntry.

	Examples::
	
		// From inside AdvancedLightBinManager::addLight
		AdvancedLightBinEntry::LightBinEntry lEntry.vertBuffer = mLightManager->
			getSphereMesh( lEntry.numPrims, lEntry.primBuffer );
			
.. cpp:function:: getConeMesh( U32 &, GFXPrimitiveBuffer *& ) 

	 Will return a vertex buffer handled filled out by information for a cone, along with set the variables passed in. If the cone geomtery (mConeGeometry) is not created by the time this function is called, it will create the cone geometry (mConeGeometry) in addition to returning it.
	
	Syntax::

		getConeMesh(U32 outNumPrimitives, GFXPrimitiveBuffer *&outPrimitives )   

	:param outNumPrimitives: Will be set to the number of polygons for the SphereMesh.
	:param outPrimitives: Will always be set to NULL.
	
	:return: ``GFXVertexBufferHandle<AdvancedLightManager::LightVertex>`` Used for the vertex buffer, typically for a LightBinEntry.

	Examples::
	
		// From inside AdvancedLightBinManager::addLight
		AdvancedLightBinEntry::LightBinEntry lEntry.vertBuffer = mLightManager->
			getConeMesh( lEntry.numPrims, lEntry.primBuffer );
			
.. cpp:function:: findShadowMapForObject( SimObject * )  

	 Will take in a SimObject*, then cast it to a ISceneLight*. If the converted variable is valid (meaning you passed in a valid ISceneLight), then it would get the shadow map available for the light.
	
	Syntax::

		findShadowMapForObject(SimObject *object)    

	:param object: The SimObject to be converted to a ISceneLight* to find the ShadowMap.
	
	:return: ``LightShadowMap *`` The found shadow map from the ISceneLight casted "object" variable.

	Examples::
	
		LightShadowMap *lightShadowMap = lm->findShadowMapForObject( object );