ReflectorDesc
=============

A datablock which defines performance and quality properties for dynamic reflections.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

ReflectorDesc is not itself a reflection and does not render reflections. It is a dummy class for holding and exposing to the user a set of reflection related properties. Objects which support dynamic reflections may then reference a ReflectorDesc.

Example::

	datablock ReflectorDesc( ExampleReflectorDesc )
	{
	   texSize = 256;
	   nearDist = 0.1;
	   farDist = 500;
	   objectTypeMask = 0xFFFFFFFF;
	   detailAdjust = 1.0;
	   priority = 1.0;
	   maxRateMs = 0;
	   useOcclusionQuery = true;
	};

Fields
------

.. cpp:member:: float  ReflectorDesc::detailAdjust

	Scale applied to lod calculation of objects rendering into this reflection ( modulates $pref::TS::detailAdjust ).

.. cpp:member:: float  ReflectorDesc::farDist

	Far plane distance to use when rendering reflections.

.. cpp:member:: int  ReflectorDesc::maxRateMs

	If less than maxRateMs has elapsed since this relfection was last updated, then do not update it again. This 'skip' can be disabled by setting maxRateMs to zero.

.. cpp:member:: float  ReflectorDesc::nearDist

	Near plane distance to use when rendering this reflection. Adjust this to limit self-occlusion artifacts.

.. cpp:member:: int  ReflectorDesc::objectTypeMask

	Object types which render into this reflection.

.. cpp:member:: float  ReflectorDesc::priority

	Priority for updating this reflection, relative to others.

.. cpp:member:: int  ReflectorDesc::texSize

	Size in pixels of the (square) reflection texture. For a cubemap this value is interpreted as size of each face.

.. cpp:member:: bool  ReflectorDesc::useOcclusionQuery

	If available on the device use HOQs to determine if the reflective object is visible before updating its reflection.
