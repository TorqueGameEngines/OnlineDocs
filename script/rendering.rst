Rendering
=========

All rendering related functionality. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/BarrelDistortionPostEffect
	class/PostEffect
	class/TheoraTextureObject

Enumeration
-----------

.. cpp:member:: enum  PFXRenderTime

	When to process this effect during the frame.

	:param PFXBeforeBin: Before a RenderInstManager bin.
	:param PFXAfterBin: After a RenderInstManager bin.
	:param PFXAfterDiffuse: After the diffuse rendering pass.
	:param PFXEndOfFrame: When the end of the frame is reached.
	:param PFXTexGenOnDemand: This PostEffect is not processed by the manager. It will generate its texture when it is requested.

.. cpp:member:: enum  PFXTargetClear

	Describes when the target texture should be cleared.

	:param PFXTargetClear_None: Never clear the PostEffect target.
	:param PFXTargetClear_OnCreate: Clear once on create.
	:param PFXTargetClear_OnDraw: Clear before every draw.

.. cpp:member:: enum  PFXTargetViewport

	Specifies how the viewport should be set up for a PostEffect's target.

	:param PFXTargetViewport_TargetSize: Set viewport to match target size (default).
	:param PFXTargetViewport_GFXViewport: Use the current GFX viewport (scaled to match target size).
	:param PFXTargetViewport_NamedInTexture0: Use the input texture 0 if it is named (scaled to match target size), otherwise revert to PFXTargetViewport_TargetSize if there is none.

Functions
---------

.. cpp:function:: void addGlobalShaderMacro(string name, string value)

	Adds a global shader macro which will be merged with the script defined macros on every shader. The macro will replace the value of an existing macro of the same name. For the new macro to take effect all the shaders in the system need to be reloaded.

.. cpp:function:: void beginSampling()

	Takes a string informing the backend where to store sample data and optionally a name of the specific logging backend to use. The default is the CSV backend. In most cases, the logging store will be a file name.

	Example::

		beginSampling( "mysamples.csv" );

.. cpp:function:: void enableSamples()

	Enable sampling for all keys that match the given name pattern. Slashes are treated as separators.

.. cpp:function:: int getActiveDDSFiles()

	Returns the count of active DDSs files in memory.

.. cpp:function:: String getBitmapInfo(string filename)

	Returns image info in the following format: width TAB height TAB bytesPerPixel. It will return an empty string if the file is not found.

.. cpp:function:: void initDisplayDeviceInfo()

	Initializes variables that track device and vendor information/IDs.

.. cpp:function:: void playJournalToVideo(string journalFile, string videoFile, string encoder, float framerate, Point2I resolution)

	Load a journal file and capture it video.

.. cpp:function:: void removeGlobalShaderMacro(string name)

	Removes an existing global macro by name.

.. cpp:function:: void startVideoCapture(GuiCanvas canvas, string filename, string encoder, float framerate, Point2I resolution)

	Begins a video capture session.

.. cpp:function:: void stopSampling()

	Stops the rendering sampler.

.. cpp:function:: void stopVideoCapture()

	Stops the video capture session.

Variables
---------

.. cpp:member:: bool $pref::imposter::canShadow

	User preference which toggles shadows from imposters. Defaults to true.

.. cpp:member:: float $pref::TS::detailAdjust

	User perference for scaling the TSShape level of detail. The smaller the value the closer the camera must get to see the highest LOD. This setting can have a huge impact on performance in mesh heavy scenes. The default value is 1.

.. cpp:member:: bool $Scene::disableTerrainOcclusion

	Used to disable the somewhat expensive terrain occlusion testing.

.. cpp:member:: bool $Scene::disableZoneCulling

	If true, zone culling will be disabled and the scene contents will only be culled against the root frustum.

.. cpp:member:: int $TSControl::frameCount

	The number of frames that have been rendered since this control was created.

.. cpp:member:: int $pref::Reflect::frameLimitMS

	ReflectionManager tries not to spend more than this amount of time updating reflections per frame.

.. cpp:member:: int $Sampler::frequency

	Samples taken every nth frame.

.. cpp:member:: bool $Scene::lockCull

	Debug tool which locks the frustum culling to the current camera location.

.. cpp:member:: int $pref::TS::maxInstancingVerts

	Enables mesh instancing on non-skin meshes that have less that this count of verts. The default value is 200. Higher values can degrade performance.

.. cpp:member:: int $Scene::maxOccludersPerZone

	Maximum number of occluders that will be concurrently allowed into the scene culling state of any given zone.

.. cpp:member:: float $Scene::occluderMinHeightPercentage

	TODO.

.. cpp:member:: float $Scene::occluderMinWidthPercentage

	TODO.

.. cpp:member:: float $pref::Reflect::refractTexScale

	RefractTex has dimensions equal to the active render target scaled in both x and y by this float.

.. cpp:member:: bool $Scene::renderBoundingBoxes

	If true, the bounding boxes of objects will be displayed.

.. cpp:member:: int $pref::TS::skipLoadDLs

	User perference which causes TSShapes to skip loading higher lods. This potentialy reduces the GPU resources and materials generated as well as limits the LODs rendered. The default value is 0.

.. cpp:member:: int $pref::TS::skipRenderDLs

	User perference which causes TSShapes to skip rendering higher lods. This will reduce the number of draw calls and triangles rendered and improve rendering performance when proper LODs have been created for your models. The default value is 0.

.. cpp:member:: float $pref::TS::smallestVisiblePixelSize

	User perference which sets the smallest pixel size at which TSShapes will skip rendering. This will force all shapes to stop rendering when they get smaller than this size. The default value is -1 which disables it.

.. cpp:member:: float $pref::windEffectRadius

	Radius to affect the wind.
