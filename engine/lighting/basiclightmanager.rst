BasicLightManager
******************

**BasicLightManager Class Reference**


.. cpp:function:: isCompatible()

	Checks to make sure that the graphics card is compatible with the current pixel shader version that is needed. Currently at least 1.0 is needed.
	
	Syntax::

		isCompatible()
	
	:return: no return value.

	Examples::
	
		// Make sure its valid... else fail!
		if ( !lm->isCompatible() )
    		return false;
			
.. cpp:function:: activate( SceneGraph *) 

	In addition to calling its base classes ``active(SceneGraph*)``, it will also set the Scenegraph to enable post effect fog and tell the material manager not to use prepass.
	
	Syntax::

		activate( SceneGraph *sceneManager); // SceneGraph* The SceneGraph to activate.
	
	:return: SceneGraph* The activated SceneGraph object.

.. cpp:function:: deactivate()

	Will remove all the objects from the AdvancedLightBinManager and the PrePassRenderBin, then set them to ``NULL``. It will deactivate the Shadow Manager, unregister all the advanced lighting features and then finally send a trigger to let everyone know the LightManager has been deactivated.
	
	Syntax::

		deactivate()
	
	:return: no return value.

	Examples::
	
		if (mLightManager)
   			mLightManager->deactivate();
			
.. cpp:function:: setLightInfo( ProcessedMaterial *, const Material *, const SceneGraphData &, const SceneState *, U32, GFXShaderConstBuffer * ) 

	Will make sure that the current lighting constants are initialized, then it will update the lighting constants via ``_update4LightConsts::_update4LightConsts``.
	
	Syntax::

		setLightInfo(ProcessedMaterial *pmat, Material *mat, const SceneGraphData &sgData, SceneState *state, U32 pass, GFXShaderConstBuffer *shaderConsts ) 
		
	:param pmat: Not used.
	:param mat: Not used.
	:param sgData: Used in the call for _update4LightConsts. See LightManager::_update4LightConsts.
	:param state: Not used.
	:param pass: Not used.
	:param shaderConsts: Is used to check to see if it is the same as the last shader. This check is done because T3D sorts by material and the light manager should get hit repeatedly by the same shader. The advantage of the check is that it gives optimization that will prevent has table look ups. It is also used in the call for ``_update4LightConsts``. See ``LightManager::_update4LightConsts``.
	
	:return: no return value.

	Examples::
	
		// From inside of ProcessedShaderMaterial::setSceneInfo
		LIGHTMGR->setLightInfo( this, mMaterial, sgData, state, pass, shaderConsts );
		
.. cpp:function:: setTextureStage( const SceneGraphData &sgData, const U32 currTexFlag, const U32 textureSlot, GFXShaderConstBuffer *shaderConsts, ShaderConstHandles *handles )  

	Will always return false.
	
	Syntax::

		setTextureStage(const SceneGraphData &sgData, const U32 currTexFlag, const U32 textureSlot, GFXShaderConstBuffer *shaderConsts, ShaderConstHandles *handles ) 
		
	:param sgData: Not used.
	:param currTexFlag: Not used.
	:param textureSlot: Not used
	:param shaderConsts: Not used.
	:param handles: Not used.

	:return: no return value.

	Examples::
	
		// From inside of ProcessedCustomMaterial::setTextureStages
		lm->setTextureStage(sgData, currTexFlag, i, shaderConsts, handles )