GFX
===

The low level graphics interface to the engine.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/CubemapData
	class/DebugDrawer
	class/GFXCardProfiler
	class/GFXCardProfilerAPI
	class/GFXInit
	class/GFXSamplerStateData
	class/GFXStateBlockData
	class/Material
	class/PfxVis
	class/RenderFormatToken

Description
-----------

In Torque the GFX layer provides access to abstracted low level graphics concepts. From script you have limited access to graphics rendering as it is usually too slow to do individual draw calls thru the scripting interface. For drawing its usually better to use the higher level gameplay objects.

.. note::

	Detailed technical descriptions of when to use specific GFXStateBlockData fields, how GFXBlendOp works, or other interfaces of that nature are outside the scope of this manual. Since Torque is based on DirectX and OpenGL any reference documents for those APIs will provide the background needed to learn about rendering.

Enumeration
-----------

.. cpp:type:: enum  GFXAdapterType

	Back-end graphics API used by the GFX subsystem.

	:param OpenGL: OpenGL.
	:param D3D8: Direct3D 8.
	:param D3D9: Direct3D 9.
	:param NullDevice: Null device for dedicated servers.
	:param Xenon: Direct3D 9 on Xbox 360.

.. cpp:type:: enum  GFXBlend

	The supported blend modes.

	:param GFXBlendZero: (0, 0, 0, 0)
	:param GFXBlendOne: (1, 1, 1, 1)
	:param GFXBlendSrcColor: (Rs, Gs, Bs, As)
	:param GFXBlendInvSrcColor: (1 - Rs, 1 - Gs, 1 - Bs, 1 - As)
	:param GFXBlendSrcAlpha: (As, As, As, As)
	:param GFXBlendInvSrcAlpha: ( 1 - As, 1 - As, 1 - As, 1 - As)
	:param GFXBlendDestAlpha: (Ad Ad Ad Ad)
	:param GFXBlendInvDestAlpha: (1 - Ad 1 - Ad 1 - Ad 1 - Ad)
	:param GFXBlendDestColor: (Rd, Gd, Bd, Ad)
	:param GFXBlendInvDestColor: (1 - Rd, 1 - Gd, 1 - Bd, 1 - Ad)
	:param GFXBlendSrcAlphaSat: (f, f, f, 1) where f = min(As, 1 - Ad)

.. cpp:type:: enum  GFXBlendOp

	The blend operators.

	:param GFXBlendOpAdd: 
	:param GFXBlendOpSubtract: 
	:param GFXBlendOpRevSubtract: 
	:param GFXBlendOpMin: 
	:param GFXBlendOpMax: 

.. cpp:type:: enum  GFXCmpFunc

	The supported comparison functions.

	:param GFXCmpNever: 
	:param GFXCmpLess: 
	:param GFXCmpEqual: 
	:param GFXCmpLessEqual: 
	:param GFXCmpGreater: 
	:param GFXCmpNotEqual: 
	:param GFXCmpGreaterEqual: 
	:param GFXCmpAlways: 

.. cpp:type:: enum  GFXCullMode

	The render cull modes.

	:param GFXCullNone: 
	:param GFXCullCW: 
	:param GFXCullCCW: 

.. cpp:type:: enum  GFXFormat

	The texture formats.

	:param GFXFormatR8G8B8: 
	:param GFXFormatR8G8B8A8: 
	:param GFXFormatR8G8B8X8: 
	:param GFXFormatR32F: 
	:param GFXFormatR5G6B5: 
	:param GFXFormatR5G5B5A1: 
	:param GFXFormatR5G5B5X1: 
	:param GFXFormatA4L4: 
	:param GFXFormatA8L8: 
	:param GFXFormatA8: 
	:param GFXFormatL8: 
	:param GFXFormatDXT1: 
	:param GFXFormatDXT2: 
	:param GFXFormatDXT3: 
	:param GFXFormatDXT4: 
	:param GFXFormatDXT5: 
	:param GFXFormatD32: 
	:param GFXFormatD24X8: 
	:param GFXFormatD24S8: 
	:param GFXFormatD24FS8: 
	:param GFXFormatD16: 
	:param GFXFormatR32G32B32A32F: 
	:param GFXFormatR16G16B16A16F: 
	:param GFXFormatL16: 
	:param GFXFormatR16G16B16A16: 
	:param GFXFormatR16G16: 
	:param GFXFormatR16F: 
	:param GFXFormatR16G16F: 
	:param GFXFormatR10G10B10A2: 

.. cpp:type:: enum  GFXStencilOp

	The stencil operators.

	:param GFXStencilOpKeep: 
	:param GFXStencilOpZero: 
	:param GFXStencilOpReplace: 
	:param GFXStencilOpIncrSat: 
	:param GFXStencilOpDecrSat: 
	:param GFXStencilOpInvert: 
	:param GFXStencilOpIncr: 
	:param GFXStencilOpDecr: 

.. cpp:type:: enum  GFXTextureAddressMode

	The texture address modes.

	:param GFXAddressWrap: 
	:param GFXAddressMirror: 
	:param GFXAddressClamp: 
	:param GFXAddressBorder: 
	:param GFXAddressMirrorOnce: 

.. cpp:type:: enum  GFXTextureArgument

	The texture arguments.

	:param GFXTADiffuse: 
	:param GFXTACurrent: 
	:param GFXTATexture: 
	:param GFXTATFactor: 
	:param GFXTASpecular: 
	:param GFXTATemp: 
	:param GFXTAConstant: 
	:param OneMinus: 
	:param AlphaReplicate: 

.. cpp:type:: enum  GFXTextureFilterType

	The texture filter types.

	:param GFXTextureFilterNone: 
	:param GFXTextureFilterPoint: 
	:param GFXTextureFilterLinear: 
	:param GFXTextureFilterAnisotropic: 
	:param GFXTextureFilterPyramidalQuad: 
	:param GFXTextureFilterGaussianQuad: 

.. cpp:type:: enum  GFXTextureOp

	The texture operators.

	:param GFXTOPDisable: 
	:param GFXTOPSelectARG1: 
	:param GFXTOPSelectARG2: 
	:param GFXTOPModulate: 
	:param GFXTOPModulate2X: 
	:param GFXTOPModulate4X: 
	:param GFXTOPAdd: 
	:param GFXTOPAddSigned: 
	:param GFXTOPAddSigned2X: 
	:param GFXTOPSubtract: 
	:param GFXTOPAddSmooth: 
	:param GFXTOPBlendDiffuseAlpha: 
	:param GFXTOPBlendTextureAlpha: 
	:param GFXTOPBlendFactorAlpha: 
	:param GFXTOPBlendTextureAlphaPM: 
	:param GFXTOPBlendCURRENTALPHA: 
	:param GFXTOPPreModulate: 
	:param GFXTOPModulateAlphaAddColor: 
	:param GFXTOPModulateColorAddAlpha: 
	:param GFXTOPModulateInvAlphaAddColor: 
	:param GFXTOPModulateInvColorAddAlpha: 
	:param GFXTOPBumpEnvMap: 
	:param GFXTOPBumpEnvMapLuminance: 
	:param GFXTOPDotProduct3: 
	:param GFXTOPLERP: 

.. cpp:type:: enum  GFXTextureTransformFlags

	The texture transform state flags.

	:param GFXTTFDisable: 
	:param GFXTTFFCoord1D: 
	:param GFXTTFFCoord2D: 
	:param GFXTTFFCoord3D: 
	:param GFXTTFFCoord4D: 
	:param GFXTTFProjected: 

.. cpp:type:: enum  MaterialAnimType

	The type of animation effect to apply to this material.

	:param Scroll: Scroll the material along the X/Y axis.
	:param Rotate: Rotate the material around a point.
	:param Wave: Warps the material with an animation using Sin, Triangle or Square mathematics.
	:param Scale: Scales the material larger and smaller with a pulsing effect.
	:param Sequence: Enables the material to have multiple frames of animation in its imagemap.

.. cpp:type:: enum  MaterialBlendOp

	The type of graphical blending operation to apply to this material.

	:param None: Disable blending for this material.
	:param Mul: Multiplicative blending.
	:param Add: Adds the color of the material to the frame buffer with full alpha for each pixel.
	:param AddAlpha: The color is modulated by the alpha channel before being added to the frame buffer.
	:param Sub: Subtractive Blending. Reverses the color model, causing dark colors to have a stronger visual effect.
	:param LerpAlpha: Linearly interpolates between Material color and frame buffer color based on alpha.

.. cpp:type:: enum  MaterialWaveType

	When using the Wave material animation, one of these Wave Types will be used to determine the type of wave to display.

	:param Sin: Warps the material along a curved Sin Wave.
	:param Triangle: Warps the material along a sharp Triangle Wave.
	:param Square: Warps the material along a wave which transitions between two oppposite states. As a Square Wave, the transition is quick and sudden.

Functions
---------

.. cpp:function:: void cleanupTexturePool()

	Release the unused pooled textures in texture manager freeing up video memory.

.. cpp:function:: void clearGFXResourceFlags()

	Clears the flagged state on all allocated GFX resources. See flagCurrentGFXResources for usage details.

.. cpp:function:: void describeGFXResources(string resourceTypes, string filePath, bool unflaggedOnly)

	Dumps a description of GFX resources to a file or the console. 
	
	* texture
	* texture target
	* window target
	* vertex buffers
	* primitive buffers
	* fences
	* cubemaps
	* shaders
	* stateblocks 

	:param resourceTypes: A space seperated list of resource types or an empty string for all resources.
	:param filePath: A file to dump the list to or an empty string to write to the console.
	:param unflaggedOnly: If true only unflagged resources are dumped. See flagCurrentGFXResources.

.. cpp:function:: void describeGFXStateBlocks(string filePath)

	Dumps a description of all state blocks.

	:param filePath: A file to dump the state blocks to or an empty string to write to the console.

.. cpp:function:: void dumpRandomNormalMap()

	Creates a 64x64 normal map texture filled with noise. The texture is saved to randNormTex.png in the location of the game executable.

.. cpp:function:: void dumpTextureObjects()

	Dumps a list of all active texture objects to the console.

.. cpp:function:: void flagCurrentGFXResources()

	Flags all currently allocated GFX resources. Used for resource allocation and leak tracking by flagging current resources then dumping a list of unflagged resources at some later point in execution.

.. cpp:function:: void flushTextureCache()

	Releases all textures and resurrects the texture manager.

.. cpp:function:: static int GFXInit::getAdapterCount()

	Return the number of graphics adapters available.

.. cpp:function:: GFXFormat  getBestHDRFormat()

	Returns the best texture format for storage of HDR data for the active device.

.. cpp:function:: Point3F getDesktopResolution()

	Returns the width, height, and bitdepth of the screen/desktop.

.. cpp:function:: string getDisplayDeviceInformation()

	Get the string describing the active GFX device.

.. cpp:function:: String getDisplayDeviceList()

	Returns a tab-seperated string of the detected devices across all adapters.

.. cpp:function:: float getPixelShaderVersion()

	Returns the pixel shader version for the active device.

.. cpp:function:: String getTextureProfileStats()

	Returns a list of texture profiles in the format: ProfileName TextureCount TextureMB.

.. cpp:function:: void listGFXResources(bool unflaggedOnly)

	Returns a list of the unflagged GFX resources. See flagCurrentGFXResources for usage details.

.. cpp:function:: void reloadTextures()

	Reload all the textures from disk.

.. cpp:function:: void screenShot(string file, string format, int tileCount, float tileOverlap)

	Takes a screenshot with optional tiling to produce huge screenshots.

	:param file: The output image file path.
	:param format: Either JPEG or PNG.
	:param tileCount: If greater than 1 will tile the current screen size to take a large format screenshot.
	:param tileOverlap: The amount of horizontal and vertical overlap between the tiles used to remove tile edge artifacts from post effects.

.. cpp:function:: void setPixelShaderVersion(float version)

	Sets the pixel shader version for the active device. This can be used to force a lower pixel shader version than is supported by the device for testing or performance optimization.

	:param version: The floating point shader version number.

.. cpp:function:: void setReflectFormat(GFXFormat format)

	Set the reflection texture format.

Variables
---------

.. cpp:member:: bool $gfx::disableOcclusionQuery

	Debug helper that disables all hardware occlusion queries causing them to return only the visibile state.

.. cpp:member:: bool $pref::Video::disableVerticalSync

	Disables vertical sync on the active device.

.. cpp:member:: bool $gfx::disassembleAllShaders

	On supported devices this will dump shader disassembly to the procedural shader folder.

.. cpp:member:: float $pref::Video::forcedPixVersion

	Will force the shader model if the value is positive and less than the shader model supported by the active device. Use 0 for fixed function.

.. cpp:member:: string $pref::Video::missingTexturePath

	The file path of the texture to display when the requested texture is missing.

.. cpp:member:: int $pref::Video::textureReductionLevel

	The number of mipmap levels to drop on loaded textures to reduce video memory usage. It will skip any textures that have been defined as not allowing down scaling.

.. cpp:member:: string $pref::Video::unavailableTexturePath

	The file path of the texture to display when the requested texture is unavailable. Often this texture is used by GUI controls to indicate that the request image is unavailable.

.. cpp:member:: string $pref::Video::warningTexturePath

	The file path of the texture used to warn the developer.

.. cpp:member:: bool $gfx::wireframe

	Used to toggle wireframe rendering at runtime.
