Water Plane
===========

Like a Water Block, the Water Plane object can add realism to the environment of your level. However, the Water Plane is an infinite body of water with an adjustable height. The moment you add this object to your scene, everything below the height of the Water Plane will be submerged, similarly to a Water Block, but the Water Plane has no edges.

Adding a Water Plane
--------------------

To add a Water Plane, select the Library tab in the Scene Tree Panel. Select the Level tab and double-click the Environment folder. Locate the WaterPlane object.

.. image:: waterplane/WPLibrary.jpg

Double-click the WaterPlane entry. the Create Object dialog window will appear.

.. image:: waterplane/AddWaterPlane.jpg

Enter a name for your Water Plane, then click the Create New button. A new Water Plane will be added to your scene. If your entire screen fills up with a dark blue or black color, this means the WaterPlane was placed above your camera so that your camera is underwater. Just move your camera up to get out of the water.

.. image:: waterplane/WaterPlaneAdded.jpg

This is typical if your objects are set to drop at or above your camera in the Object > Drop Location sub-menu.

Water Plane Properties
----------------------

Additional properties can be changed with the Inspector pane and are identical to what you will find in a WaterBlock. To change a Water Planes properties using the Inspector Pane, click the Scene tab, then click the name of your new Water Plane object. The Inspector pane will update to display the current properties of your new Water Plane.

Inspector
~~~~~~~~~

Name
	TypeName. Optional global name of this object.

id
	TypeCaseString. SimObjectId of this object. Read Only.

Source Class
	TypeCaseString. Source code class of this object. Read Only.

Transform
~~~~~~~~~

position
	MatrixPosition. Object world position.

WaterPlane
~~~~~~~~~~

gridSize
	TypeF32. Duplicate of gridElementSize for backwards compatibility.

gridElementSize
	TypeF32. Spacing between vertices in the WaterPlane.

WaterObject
~~~~~~~~~~~

density
	TypeF32. Affects buoyancy of an object, thus affecting the Z velocity of a player (jumping, falling, etc).

viscosity
	TypeF32. Affects drag force applied to an object submerged in this container.

liquidType
	TypeRealString. Liquid type of WaterPlane, such as water, ocean, lava. Currently only Water is defined and used.

baseColor
	TypeColorI. Changes color of water fog, which is what gives the water its color appearance.

fresnelBias
	TypeF32. Extent of fresnel affecting reflection fogging.

fresnelPower
	TypeF32. Measures intensity of affect on reflection based on fogging.

specularPower
	TypeName. Power used for specularity on the water surface (sun only).

specularColor
	TypeColorF. Color used for specularity on the water surface (sun only).

emissive
	TypeBool. When true, the water colors do not react to changes in environmental lighting.

Waves (vertex undulation)
~~~~~~~~~~~~~~~~~~~~~~~~~

overallWaveMagnitude
	TypeF32. Master variable affecting entire body of water undulation.

rippleTex
	TypeImageFilename. Normal map used to simulate small surface ripples.

Ripples (texture undulation)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

overallRippleMagnitude
	TypeF32. Master variable affecting the entire surface of the waterplane.

foamTex
	TypeImage Filename. Diffuse texture for foam in shallow water (advanced lighting only).

Foam
~~~~

overalFoamOpacity
	TypeF32. Opacity of foam texture.

foamMaxDepth
	TypeF32. Maximum depth for foam texture display.

foamAmbientLerp
	TypeF32. Interpolation for foam settings.

foamRippleInfluence
	TypeF32. Intensity of the ripples.

Reflect
~~~~~~~

cubemap
	TypeCubemapName. Cubemap is used instead of reflection texture if fullReflect is off.

fullReflect
	TypeBool. Enables dynamic reflection rendering.

reflectivity
	TypeF32. Overall reflectivity of the water surface.

reflectPriority
	TypeF32. Affects the sort order of reflected objects.

reflectMaxRateMs
	TypeF32. Affects the sort time of reflected objects.

reflectDetailAdjust
	TypeF32. Scale up or down the detail level for objects rendered in a reflection.

reflectNormalUp
	TypeBool. Always use Z up as the reflection normal.

useOcclusionQuery
	TypeBool. Turn off reflection rendering when occluded (delayed).

reflectTexSize
	TypeF32. Texure size used for reflections (square).

Underwater Fogging
~~~~~~~~~~~~~~~~~~

waterFogDensity
	TypeF32. Intensity of underwater fogging.

waterFogDensityOffset
	TypeF32. Delta, or limit, applied to waterFogDensity.

wetDepth
	TypeF32. The depth in world units at which full darkening will be received giving a wet appearance.

wetDarkening
	TypeF32. The refract color intensity scaled at wetDepth.

Misc
~~~~

depthGradientTex
	TypeImage filename. 1D texture defining the base water color.

depthGradientMax
	TypeF32. Depth in world units, the max range of the color gradient texture.

Distortion
~~~~~~~~~~

distortStartDist
	TypeF32. Determines start of distortion effect where water surface intersects.

distortEndDist
	TypeF32. Max distance that distortion algorithm is performed.

distortFullDepth
	TypeF32. Determines the scaling down of distortion in shallow water.

Basic Lighting
~~~~~~~~~~~~~~

clarity
	TypeF32. Relative opacity or transparency of the water surface.

underwaterColor
	TypeColor. Changes the color shading of objects beneath the water surface.

Sound
~~~~~

soundAmbience
	TypeSFXAmbienceName. Ambient sound environment when listener is active.

Editing
~~~~~~~

isRenderEnabled
	TypeBool. Toggles whether the object is rendered.

isSelectionEnabled
	TypeBool. Toggle whether this object can be selected in the editor.

hidden
	TypeBool.Toggle visibility in editor.

locked
	TypeBool. Toggle whether the object can be edited.

Mounting
~~~~~~~~

mountPID
	TypePID. Unique identifier of the mount.

mountNode
	TypeS32. Node where the mount occurs.

mountPos
	TypeS32. Offset for positioning the node.

mountRot
	TypeS32. Rotation of this object in relation to the mount node.

Object
~~~~~~

internalName
	TypeString. Non-unique name used by child objects of a group.

parentGroup
	TypeString. Group object belongs to.

class
	TypeString. Links object to script class namespace.

superClass
	TypeString. Links object to script super class (parent) namespace.

Persistence
~~~~~~~~~~~

canSave
	TypeBool. Toggle whether the object can be saved in the editor.

canSaveDynamicFields
	TypeBool. True if dynamic fields (added at runtime) should be saved, defaults to true.
