ShadowManager
***************

**ShadowManager Class Reference**

.. cpp:function:: activate()

	Called when the shadow manager should become active. It will assign the class variable "SceneGraph* mSceneManager" to the global "SceneGraph* gClientSceneGraph" variable.
	
	Syntax::

		activate()
	
	:return: no return value.

	Examples::
	
		// Called from within the AdvancedLightManager::activate, SHADOWMGR is a #define
		// of the ShadowMapManager::instance() function.
		SHADOWMGR->activate();
		
.. cpp:function:: deactivate()

	Called when we don't want the shadow manager active (should clean up). As this is basically just a base class, this function does nothing and should be overridden by the super class to clean clean up its own data.
	
	Syntax::

		deactivate()
	
	:return: no return value.

	Examples::
	
		// Called from within the AdvancedLightManager::deactivate, SHADOWMGR is a #define
		// of the ShadowMapManager::instance() function.
		SHADOWMGR->deactivate();

.. cpp:function:: canActivate()

	Called to find out if it is valid to activate this shadow system. Currently this function will always return true.
	
	Syntax::

		canActivate()
	
	:return: Will always return true (**bool**).

	Examples::
	
		Currently this function is not called in the base and is left up to the user to implement.