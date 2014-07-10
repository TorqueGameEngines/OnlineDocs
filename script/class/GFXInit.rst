GFXInit
=======

Functions for tracking GFX adapters and initializing them into devices.

Description
-----------

Functions for tracking GFX adapters and initializing them into devices.

Methods
-------

.. cpp:function:: static void GFXInit::createNullDevice()

	Create the NULL graphics device used for testing or headless operation.

.. cpp:function:: static String GFXInit::getAdapterMode(int index, int modeIndex)

	Gets the details of the specified adapter mode.

	:param index: Index of the adapter to query.
	:param modeIndex: Index of the mode to get data from.

	:return: A video mode string in the format 'width height fullscreen bitDepth refreshRate aaLevel'. 

.. cpp:function:: static int GFXInit::getAdapterModeCount(int index)

	Gets the number of modes available on the specified adapter.

	:param index: Index of the adapter to get modes from.

	:return: The number of video modes supported by the adapter or -1 if the given adapter was not found. 

.. cpp:function:: static String GFXInit::getAdapterName(int index)

	Returns the name of the graphics adapter.

	:param index: The index of the adapter.

.. cpp:function:: static String GFXInit::getAdapterOutputName(int index)

	Returns the name of the graphics adapter's output display device.

	:param index: The index of the adapter.

.. cpp:function:: static float GFXInit::getAdapterShaderModel(int index)

	Returns the supported shader model of the graphics adapter or -1 if the index is bad.

	:param index: The index of the adapter.

.. cpp:function:: static  GFXAdapterType  GFXInit::getAdapterType(int index)

	Returns the type (D3D9, D3D8, GL, Null) of a graphics adapter.

	:param index: The index of the adapter.

.. cpp:function:: static int GFXInit::getDefaultAdapterIndex()

	Returns the index of the default graphics adapter. This is the graphics device which will be used to initialize the engine.
