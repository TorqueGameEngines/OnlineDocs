Game Controls
=============

GUI controls dedicated to game play systems, such as heads up displays. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/GuiClockHud
	class/GuiCrossHairHud
	class/GuiGameListMenuCtrl
	class/GuiGameListMenuProfile
	class/GuiGameListOptionsCtrl
	class/GuiGameListOptionsProfile
	class/GuiHealthBarHud
	class/GuiHealthTextHud
	class/GuiShapeNameHud

Functions
---------

.. cpp:function:: void snapToggle()

	Prevents mouse movement from being processed. In the source, whenever a mouse move event occurs GameTSCtrl::onMouseMove() is called. Whenever snapToggle() is called, it will flag a variable that can prevent this from happening: gSnapLine. This variable is not exposed to script, so you need to call this function to trigger it.

	Example::

		// Snapping is off by default, so we will toggle
		// it on first:
		PlayGui.snapToggle();
		
		// Mouse movement should be disabled
		// Lets turn it back on
		PlayGui.snapToggle();
