GuiCheckBoxCtrl
===============

A named checkbox that can be toggled on and off.

Inherit:
	:doc:`GuiButtonBaseCtrl`

Description
-----------

A GuiCheckBoxCtrl displays a text label next to a checkbox that can be toggled on and off by the user. Checkboxes are usually used to present boolean choices like, for example, a switch to toggle fullscreen video on and off.

Example::

	// Create a checkbox that allows to toggle fullscreen on and off.
	newGuiCheckBoxCtrl( FullscreenToggle )
	{
	   text = "Fullscreen";
	};
	
	// Set the initial state to match the current fullscreen setting.
	FullscreenToggle.setStateOn( Canvas.isFullscreen() );
	
	// Define function to be called when checkbox state is toggled.
	function FullscreenToggle::onClick( %this )
	{
	   Canvas.toggleFullscreen();
	}

Methods
-------

.. cpp:function:: bool GuiCheckBoxCtrl::isStateOn()

	Test whether the checkbox is currently checked.

	:return: True if the checkbox is currently ticked, false otherwise. 

.. cpp:function:: void GuiCheckBoxCtrl::setStateOn(bool newState)

	Set whether the checkbox is ticked or not. Reimplemented from GuiButtonBaseCtrl .

	:param newState: If true the box will be checked, if false, it will be unchecked.
