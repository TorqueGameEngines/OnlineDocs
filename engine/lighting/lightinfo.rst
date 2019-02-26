LightInfo 
**********

**LightInfo Class Reference**

.. cpp:function:: unpackExtended( BitStream * )   

	Will traverse the vector of LightInfoEx pointers (mExtended) and call their individual unpackUpdate function with the passed in stream as a parameter.  
	
	Syntax::

		unpackExtended( BitStream *stream )isCompatible() 
		
	:param stream: Used to pass to the individual calls of the unpackUpdate through the traversed mExtended.
	
	:return: No return value.

	Examples::
	
		// From LightBase::unpackUpdate
		mLight->unpackExtended( stream );
		
.. cpp:function:: packExtended( BitStream * )  

	Will traverse the vector of LightInfoEx pointers (mExtended) and call their individual packUpdate function with the passed in stream as a parameter.
	
	Syntax::

		packExtended( BitStream *stream ) 
		
	:param stream: Used to pass to the individual calls of the packUpdate through the traversed mExtended.
	
	:return: No return value.

	Examples::
	
		// From LightNase::packUpdate at lightBase.cpp
		mLight->packExtended( stream ); 
		
.. cpp:function:: packExtended( BitStream * ) 

	Will traverse the vector of LightInfoEx pointers (mExtended) and call their individual packUpdate function with the passed in stream as a parameter.
	
	Syntax::

		packExtended( BitStream *stream ) 
		
	:param stream: Used to pass to the individual calls of the packUpdate through the traversed mExtended.
	
	:return: No return value.

	Examples::
	
		// From LightNase::packUpdate at lightBase.cpp
		mLight->packExtended( stream );
		
.. cpp:function:: getWorldToLightProj( MatrixF * )  

	Builds the world to light view projected used for shadow texture and cookie lookups.
	
	Syntax::

		getWorldToLightProj( MatrixF *outMatrix ) 
		
	:param outMatrix: The generated Matrix, if the type of the light is a spot then this matrix will be created by multiplying the cone projection by the inverse transform of the light. If the type of the light is not a Spot, then the Matrix will be assigned to the inverse of the light.
	
	:return: No return value.

	Examples::
	
		// From AdvancedLightManager::setLightInfo
		MatrixF proj;
		light->getWorldToLightProj( &proj );
		
.. cpp:function:: deleteAllLightInfoEx()   

	Deletes all LightInfoEx objects.
	
	Syntax::

		deleteAllLightInfoEx() 
	
	:return: No return value.

	Examples::
	
		// From the destructor of LightInfo
		deleteAllLightInfoEx();
		
.. cpp:function:: addExtended( LightInfoEx * )  

	Will add the passed in LightInfoEx * to the current vector of LightInfo * (mExtended) if it is not null.
	
	Syntax::

		addExtended( LightInfoEx *lightInfoEx )
		
	:param lightInfoEx: Will be added to mExtended.
	
	:return: No return value.

	Examples::
	
		// AdvancedLightManager::_addLightInfoEx from advancedLightManager.cpp
		lightInfo->addExtended( new ShadowMapParams( lightInfo ) );
		
.. cpp:function:: getExtended( const LightInfoExType & )   

	Will return the LightInfoEx * mExtended based upon the LightInfoExType passed in.
	
	Syntax::

		getExtended( const LightInfoExType &type ) 
		
	:param type: The type of a LightInfoEx to be used to return the LightInfoExType.
	
	:return: ``LightInfoEx *`` The LightInfoEx * from mExtended with regards to the type passed in.

	Examples::
	
		// From CubeLightShadowMap::setShaderParameters at cubeLightShadowMap.cpp
		ShadowMapParams *p = mLight->getExtended<ShadowMapParams>();
		
.. cpp:function:: setGFXLight( GFXLightInfo * )  

	Sets a fixed function GFXLight with the properties on this class. 
	
	Syntax::

		setGFXLight(GFXLightInfo *light ) 
		
	:param light: The light that will have its properties filled in based upon the properties of this class.
	
	:return: No return value.

	Examples::
	
		// From ProcessedFFMaterial::_setPrimaryLightInfo at porcessedFFMaterial.cpp
		GFXLightInfo xlatedLight;
		light->setGFXLight(&xlatedLight);
		
.. cpp:function:: set( const LightInfo * )   

	Copies the data passed in from the LightInfo passed in, such as the properties and the contents of mExtended.
	
	Syntax::

		set(const LightInfo *light ) 
		
	:param light: The light in which the information to be set to this class should be obtained from.
	
	:return: No return value.

	Examples::
	
		None.