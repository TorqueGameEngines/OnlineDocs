Lighting
========

The script functionality related to the lighting systems and lights.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/AdvancedLightBinManager
	class/LightAnimData
	class/LightBase
	class/LightDescription
	class/LightFlareData
	class/PointLight
	class/SpotLight

Functions
---------

.. cpp:function:: string getActiveLightManager()

	Returns the active light manager name.

.. cpp:function:: String getLightManagerNames()

	Returns a tab seperated list of light manager names.

.. cpp:function:: bool lightScene(string completeCallbackFn, string mode)

	Will generate static lighting for the scene if supported by the active light manager. If mode is "forceAlways", the lightmaps will be regenerated regardless of whether lighting cache files can be written to. If mode is "forceWritable", then the lightmaps will be regenerated only if the lighting cache files can be written.

	:param completeCallbackFn: The name of the function to execute when the lighting is complete.
	:param mode: One of "forceAlways", "forceWritable" or "loadOnly".

	:return: Returns true if the scene lighting process was started. 

.. cpp:function:: void onLightManagerActivate(string name)

	A callback called by the engine when a light manager is activated.

	:param name: The name of the light manager being activated.

.. cpp:function:: void onLightManagerDeactivate(string name)

	A callback called by the engine when a light manager is deactivated.

	:param name: The name of the light manager being deactivated.

.. cpp:function:: void resetLightManager()

	Deactivates and then activates the currently active light manager.This causes most shaders to be regenerated and is often used when global rendering changes have occured.

.. cpp:function:: bool setLightManager(string name)

	Finds and activates the named light manager.

	:return: Returns true if the light manager is found and activated. 

Variables
---------

.. cpp:member:: bool $Light::renderLightFrustums

	Toggles rendering of light frustums when the light is selected in the editor.

.. cpp:member:: bool $Light::renderViz

	Toggles visualization of light object's radius or cone.


Advanced Lighting
-----------------

The script functionality related to the Advanced Lghting system.

Enumeration
~~~~~~~~~~~

.. cpp:member:: enum  ShadowFilterMode

	The shadow filtering modes for Advanced Lighting shadows.

	:param None: Simple point sampled filtering. This is the fastest and lowest quality mode.
	:param SoftShadow: A variable tap rotated poisson disk soft shadow filter. It performs 4 taps to classify the point as in shadow, out of shadow, or along a shadow edge. Samples on the edge get an additional 8 taps to soften them.
	:param SoftShadowHighQuality: A 12 tap rotated poisson disk soft shadow filter. It performs all the taps for every point without any early rejection.

.. cpp:member:: enum  ShadowType

	:param Spot: 
	:param PSSM: 
	:param Paraboloid: 
	:param DualParaboloidSinglePass: 
	:param DualParaboloid: 
	:param CubeMap: 

Variables
~~~~~~~~~

.. cpp:member:: float $pref::PSSM::detailAdjustScale

	Scales the model LOD when rendering into the PSSM shadow. Use this to reduce the draw calls when rendering the shadow by having meshes LOD out nearer to the camera than normal.

.. cpp:member:: bool $Shadows::disable

	Used by the editor to disable all shadow rendering.

.. cpp:member:: bool $pref::Shadows::disable

	Used to disable all shadow rendering.

.. cpp:member:: ShadowFilterMode  $pref::shadows::filterMode

	The filter mode to use for shadows.

.. cpp:member:: bool $AL::PSSMDebugRender

	Enables debug rendering of the PSSM shadows.

.. cpp:member:: float $pref::PSSM::smallestVisiblePixelSize

	The smallest pixel size an object can be and still be rendered into the PSSM shadow. Use this to force culling of small objects which contribute little to the final shadow.

.. cpp:member:: float $pref::Shadows::textureScalar

	Used to scale the shadow texture sizes. This can reduce the shadow quality and texture memory overhead or increase them.

.. cpp:member:: bool $AL::UseSSAOMask

	Used by the SSAO PostEffect to toggle the sampling of ssaomask texture by the light shaders.


Basic Lighting
--------------

The script functionality related to the Basic Lghting system.

Variables
~~~~~~~~~

.. cpp:member:: int $BasicLightManagerStats::activePlugins

	The number of active Basic Lighting SceneObjectLightingPlugin objects this frame.

.. cpp:member:: int $BasicLightManagerStats::elapsedUpdateMs

	The number of milliseconds spent this frame updating Basic Lighting shadows.

.. cpp:member:: float $pref::ProjectedShadow::fadeEndPixelSize

	A size in pixels at which BL shadows are fully faded out. This should be a smaller value than fadeStartPixelSize.

.. cpp:member:: float $pref::ProjectedShadow::fadeStartPixelSize

	A size in pixels at which BL shadows begin to fade out. This should be a larger value than fadeEndPixelSize.

.. cpp:member:: float $BasicLightManager::shadowFilterDistance

	The maximum distance in meters that projected shadows will get soft filtering.

.. cpp:member:: int $BasicLightManagerStats::shadowsUpdated

	The number of Basic Lighting shadows updated this frame.
