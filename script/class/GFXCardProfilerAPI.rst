GFXCardProfilerAPI
==================

This class is the interface between TorqueScript and GFXCardProfiler.

Description
-----------

You will not actually declare GFXCardProfilerAPI in TorqueScript. It exists solely to give access to the GFXCardProfiler's querying functions, such as GFXCardProfiler::getRenderer.

Example::

	// Example of accessing GFXCardProfiler function from script
	// Notice you are not using the API version
	%videoMem = GFXCardProfiler::getVideoMemoryMB();

Methods
-------

.. cpp:function:: static String GFXCardProfilerAPI::getCard()

	Returns the card name.

.. cpp:function:: static String GFXCardProfilerAPI::getRenderer()

	Returns the renderer name. For example D3D9 or OpenGL.

.. cpp:function:: static String GFXCardProfilerAPI::getVendor()

	Returns the card vendor name.

.. cpp:function:: static String GFXCardProfilerAPI::getVersion()

	Returns the driver version string.

.. cpp:function:: static int GFXCardProfilerAPI::getVideoMemoryMB()

	Returns the amount of video memory in megabytes.

.. cpp:function:: static int GFXCardProfilerAPI::queryProfile(string name, int defaultValue)

	Used to query the value of a specific card capability.

	:param name: The name of the capability being queried.
	:param defaultValue: The value to return if the capability is not defined.

.. cpp:function:: static void GFXCardProfilerAPI::setCapability(string name, int value)

	Used to set the value for a specific card capability.

	:param name: The name of the capability being set.
	:param value: The value to set for that capability.
