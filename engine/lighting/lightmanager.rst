LightManager
*************

**LightManager Class Reference**

.. cpp:function:: lightScene( const char*, const char* ) 

	Will generate static lighting (aka lightmaps) for the scene if supported by the active light manager. If mode is "forceAlways", the lightmaps will be regenerated regardless of whether lighting cache files can be written to. If mode is "forceWritable", then the lightmaps will be regenerated only if the lighting cache files can be written. 
	
	Syntax::

		lightScene(const char* callback, const char* param )
	
	:param callback:  The name of the function to execute when the lighting is complete.
	:param param: Either "forceAlways" or "forceWritable".
	
	:return: **bool** Returns true if the scene lighting process was started.

	Examples::
	
		// Get the sunlight.
		LightInfo *sunLight = mLightManager->getSpecialLight( LightManager::slSunLightType );
		
.. cpp:function:: getSceneLightingInterface( )  

	Will return the AvailableSLInterfaces for the LightManager, if there is no available lighting system then it will create a new AvailableSLInterfaces and then return that.  
	
	Syntax::

		getSceneLightingInterface()
	
	:return: ``LightInfo *`` The LightInfo * of the special light.

	Examples::
	
		// From PersistInfo::read 
		SceneLightingInterfaces sli = LIGHTMGR->getSceneLightingInterface()->
		mAvailableSystemInterfaces;

.. cpp:function:: _update4LightConsts( const SceneGraphData &sgData, GFXShaderConstHandle *, GFXShaderConstHandle *,GFXShaderConstHandle *, GFXShaderConstHandle *, GFXShaderConstHandle *,GFXShaderConstHandle *,GFXShaderConstBuffer *) 

	Will update the shader constants of ``GFXShaderConstBuffer *`` depending on the validity of the ``GFXShaderConstHandle *``'s passed in. 
	
	Syntax::

		update4LightConsts(const SceneGraphData &sgData, GFXShaderConstHandle *lightPositionSC, GFXShaderConstHandle *lightDiffuseSC, GFXShaderConstHandle *lightAmbientSC, GFXShaderConstHandle *lightInvRadiusSqSC, GFXShaderConstHandle *lightSpotDirSC, GFXShaderConstHandle **lightSpotAngleSC, GFXShaderConstBuffer *shaderConsts) 
	
	:param sgData: The scene graph data related to how the lights will be used.
	:param lightPositionSC: The shader constant for the position paramter.
	:param lightDiffuseSC: The shader constant for the diffuse paramter.
	:param lightAmbientSC: The shader constant for the ambient paramter.
	:param lightInvRadiusSqSC: The shader constant for the light inverse radius paramter.
	:param lightSpotDirSC: The shader constant for the spot light direction paramter.
	:param lightSpotAngleSC: The shader constant for the spot light angle paramter.
	:param shaderConsts: The shader consts for the buffer.
	
	:return: no return value.

	Examples::
	
		// From AdvancedLightManager::setLightInfo
		// Update the forward shading light constants.
		_update4LightConsts( sgData,
                        lsc->mLightPositionSC,
                        lsc->mLightDiffuseSC,
                        lsc->mLightAmbientSC,
                        lsc->mLightInvRadiusSqSC,
                        lsc->mLightSpotDirSC,
                        lsc->mLightSpotAngleSC,
                        shaderConsts );
		

.. cpp:function:: getAllUnsortedLights( Vector * ) 

	Will append all of the registered lights to the "Vector *" variable passed in. 
	
	Syntax::

		getAllUnsortedLights(Vector *list) 
		
	:param list: A vector of "LightInfo" pointers that will have the registered lights added to it.

	:return: no return value.

	Examples::
	
		// From SceneLighting::light
		LIGHTMGR->getAllUnsortedLights(&mLights);
		
.. cpp:function:: unregisterAllLights() 

	Will clear out all of the special lights and registered lights.
	
	Syntax::

		unregisterAllLights()
		
	:return: no return value.

	Examples::
	
		// Unregister all the lights in the light manager.
		LIGHTMGR->unregisterAllLights();
		
.. cpp:function:: unregisterLocalLight( LightInfo * ) 

	Empty function. 
	
	Syntax::

		Not used.
		
	:return: no return value.

	Examples::
	
		None.

.. cpp:function:: registerLocalLight( LightInfo * ) 

	Empty function. 
	
	Syntax::

		Not used.
		
	:return: no return value.

	Examples::
	
		None.
		
.. cpp:function:: unregisterGlobalLight( LightInfo * ) 

	Will remove the passed in light from the registered lights. If the light passed in is the sun, then it will clear the suns special light also. 
	
	Syntax::

		unregisterGlobalLight(LightInfo *light) 
	
	:param light: The light to be registered from mRegisteredLights.
	
	:return: no return value.

	Examples::
	
		lightManager->unregisterGlobalLight( mLight );
		
.. cpp:function:: registerGlobalLight( LightInfo *, SimObject * ) 

	If the light is not already registered, then the light will be added to the registered lights. If it already added, a AssertFatal will be thrown. 
	
	Syntax::

		registerGlobalLight(LightInfo *light, SimObject *obj )
	
	:param light: The light to be registered to mRegisteredLights.
	:param obj: Not used.
	
	:return: no return value.

	Examples::
	
		// From inside of Item::registerLights
		lightManager->registerGlobalLight( mLight, this );
		
.. cpp:function:: registerGlobalLights( const Frustum *, bool ) 

	Register the lights depending if there is a Frustum or if there is static lighting. If there is no frustum or there is static lighting, then there will be no light culling. If there is a frustum or there is no static lighting, then cull the lights using the frustum.

	After the decision for light culling or not, it will have the lights register themselves.
	
	Syntax::

		registerGlobalLights(const Frustum *frustum, bool staticLighting ) 
	
	:param frustrum: The frustum to be used for light culling.
	:param staticLighting: Whether or not static lighting is being processed.
	
	:return: no return value.

	Examples::
	
		// Get the lights for rendering the scene.
		LIGHTMGR->registerGlobalLights( &sceneState->getFrustum(), false);
		
.. cpp:function:: setSpecialLight( LightManager::SpecialLightTypesEnum, LightInfo * ) 

	Register the light with the LightManager and set the light to one of the special light types for the LightManager.
	
	Syntax::

		setSpecialLight(LightManager::SpecialLightTypesEnum type, LightInfo *light ) 
	
	:param type: The special light type.
	:param light: The light to apply the type to.
	
	:return: no return value.

	Examples::
	
		// Set the sunlight. 
		mLightManager->setSpecialLight( LightManager::slSunLightType, theSun );
		
.. cpp:function:: getSpecialLight( LightManager::SpecialLightTypesEnum , bool ) 

	Will return the special light based upon the type passed in if it is available. If it is not available, and the useDefault is set to true then it will return the result of getDefaultLight(). In the event that the special light is not found and useDefault is false, the function will return false.
	
	Syntax::

		getSpecialLight(LightManager::SpecialLightTypesEnum type, bool useDefault )  
	
	:param type: The special light type to find.
	:param useDefault: If the special light based up the light is not found, it will return the default light from ``getDefaultLight()``. useDefault is set to true by default.
	
	:return: ``LightInfo *`` The LightInfo * of the special light.

	Examples::
	
		// Get the sunlight. 
		LightInfo *sunLight = mLightManager->getSpecialLight( LightManager::slSunLightType );
		
.. cpp:function:: getDefaultLight() 

	Will return the sun if it is registered, as it is always the default light. However, if the sun has not been registered yet then it will create a dummy special light.
	
	Syntax::

		getDefaultLight()   
	
	:return: ``LightInfo *`` The LightInfo * of the special light.

	Examples::
	
		// Get the default light, which will be the sun if it is registered
		mLightManager->getDefaultLight();
		
.. cpp:function:: deactivate() 

	Will check to see if the LightManager has been already been deactived and that it is the active light manager. If it is passes those two checks, it will call it's deactivate callback and then unregister all of the lights associated with LightManager (via unregiserAllLights(), detailed below).
	
	Syntax::

		deactivate()  
	
	:return: No return value.

	Examples::
	
		// Deactivate the light manager
		mLightManager->deactivate();
		
.. cpp:function:: activate( SceneGraph *) 

	Will activate the LightManager if it is not already activate (in which case an AssertFatal will be thrown) and call the callback for activating the light manager.
	
	Syntax::

		activate(SceneGraph *sceneManager); 
		
	:param sceneManager: The SceneGraph that will be used to activate rendering passes and the post effect fog if there is a prepass.
	
	:return: No return value.

	Examples::
	
		// From inside of "SceneGraph::_setLightManager( LightManager *lm )" located in 
		// sceneGraph.cpp
		mLightManager->activate( this );
		
.. cpp:function:: initLightFields()  

	A static function that will traverse the LightManagerMap and will call each LightManager's _initLightFields function. Since _initLightFields is a pure virtual function, it will call the derived classes _initLightFields.
	
	Syntax::

		initLightFields() 
		
	:return: No return value.

	Examples::
	
		LightManager::initLightFields();

.. cpp:function:: getLightManagerNames( String * )   

	A static function that will create a String containing all of the LightManager names from the LightManagerMap.
	
	Syntax::

		getLightManagerNames(String *outString);
	
	:param outString: The string that will be constructed based upon the available LightManger names from the LightManagerMap.
		
	:return: No return value.

	Examples::
	
		If the LightManagerMap had two LightManager's inside of it, one being 
		"Advanced Lighting" and the other "Basic Lighting" then outString will be 
		"Advanced Lighting    Basic Lighting". The spacing between "Advanced Lighting" 
		and "Basic Lighting" is a tab ("\\t").		

.. cpp:function:: findByName( const char * )   

	A static function that traverses the LightManagerMap for the LightManager with the name passed in. If no LightManager in the LightManagerMap contains that name, it will return NULL.
	
	Syntax::

		findByName(const char *name); 
	
	:param name: The name of the LightManager to find.
		
	:return: ``LightManager*`` The LightManager found in the LightManagerMap with the name passed in.

	Examples::
	
		// Find the LightManager with the name "Advanced Lighting"
		LightManager::findByName( "Advanced Lighting" )
		
.. cpp:function:: _getLightManagers() 

	Returns the static LightManagerMap.
	
	Syntax::

		_getLightManagers() 
		
	:return: ``LightManagerMap``

	Examples::
	
		// Retrieve the LightManagerMap, example is from LightManagerMap::findByName
		LightManagerMap &lightManagers = _getLightManagers();
		
.. cpp:function:: ~LightManager()  

	Will safely delete the default light and Available Scene Lighting Interfaces. It will also remove its self from the LightManagerMap.
	
	Syntax::

		~LightManager() 
		
	:return: No return value.

	Examples::
	
		This function is called implicitly at the destruction of LightManager.
		
.. cpp:function:: LightManager( const char *, const char * ) 

	Initializes the class variables to the default values.
	
	Syntax::

		LightManager(const char *name, const char * id);

	:param name: The name of the LightManager.
	:param id: The id of the LightManager, often an abbreviation of the name.
		
	:return: No return value.

	Examples::
	
		// The LightManager being given the name "Advanced Lighting" and the id of "ADVLM"
		LightManager( "Advanced Lighting", "ADVLM" )