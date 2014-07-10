PfxVis
======

Singleton class that exposes ConsoleStaticFunctions for debug visualizing PostEffects.

Description
-----------

Singleton class that exposes ConsoleStaticFunctions for debug visualizing PostEffects.

Example::

	// Script interface...
	PfxVis::open( PostEffect ) 
	// Multiple PostEffects can be visualized at the same time
	PfxVis::clear()      
	// Clear all visualizer windows
	PfxVis::hide()       
	// Hide all windows (are not destroyed)
	PfxVis::show()

Methods
-------

.. cpp:function:: void PfxVis::clear()

	Close all visualization windows.

	Example::

		PfxVis::clear();

.. cpp:function:: void PfxVis::hide()

	Hide all visualization windows (they are not destroyed).

	Example::

		PfxVis::hide();

.. cpp:function:: void PfxVis::onWindowClosed(GuiWindowCtrl ctrl)

	Callback when a visualization window is closed.

	:param ctrl: Name of the GUI control being closed

	Example::

		PfxVis::onWindowClosed( VisWindow )

.. cpp:function:: void PfxVis::open(PostEffect effect, bool clear)

	Open visualization windows for all input and target textures.

	:param effect: Name of the PostEffect to open
	:param clear: True to close all visualization windows before opening the effect

	Example::

		// Multiple PostEffects can be visualized at the same timePfxVis::open( PostEffect )

.. cpp:function:: void PfxVis::show()

	Show all visualization windows.

	Example::

		PfxVis::show();
