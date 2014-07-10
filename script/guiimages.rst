Image and Video Controls
========================

Controls that display images or videos. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/GuiBitmapBorderCtrl
	class/GuiChunkedBitmapCtrl
	class/GuiTheoraCtrl

Enumeration
-----------

.. cpp:member:: enum  GuiBitmapMode

	Rendering behavior when placing bitmaps in controls.

	:param Stretched: Stretch bitmap to fit control extents.
	:param Centered: Center bitmap in control.

.. cpp:member:: enum  GuiIconButtonIconLocation


	:param None: 
	:param Left: 
	:param Right: 
	:param Center: 

.. cpp:member:: enum  GuiIconButtonTextLocation


	:param None: 
	:param Bottom: 
	:param Right: 
	:param Top: 
	:param Left: 
	:param Center: 

.. cpp:member:: enum  GuiTheoraTranscoder

	Routine to use for converting Theora's Y'CbCr pixel format to RGB color space.

	:param Auto: Automatically detect most appropriate setting.
	:param Generic: Slower but beneric transcoder that can convert all Y'CbCr input formats to RGB or RGBA output.
	:param SSE2420RGBA: Fast SSE2-based transcoder with fixed conversion from 4:2:0 Y'CbCr to RGBA.
