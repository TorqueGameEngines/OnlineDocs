GuiScriptNotifyCtrl
===================

A control which adds several reactions to other GUIs via callbacks.

Inherit:
	:doc:`GuiControl`

Description
-----------

GuiScriptNotifyCtrl does not exist to render anything. When parented or made a child of other controls, you can toggle flags on or off to make use of its specialized callbacks. Normally these callbacks are used as utility functions by the GUI Editor, or other container classes. However, for very fancy GUI work where controls interact with each other constantly, this is a handy utility to make use of.

Example::

	// Common member fields left out for sake of examplenewGuiScriptNotifyCtrl()
	{
	   onChildAdded = "0";
	   onChildRemoved = "0";
	   onChildResized = "0";
	   onParentResized = "0";
	};


Methods
-------

.. cpp:function:: void  GuiScriptNotifyCtrl::onChildAdded(SimObjectId ID, SimObjectId childID)

	Called when a child is added to this GUI.

	:param ID: Unique object ID assigned when created (this in script).
	:param childID: Unique object ID of child being added.

.. cpp:function:: void  GuiScriptNotifyCtrl::onChildRemoved(SimObjectId ID, SimObjectId childID)

	Called when a child is removed from this GUI.

	:param ID: Unique object ID assigned when created (this in script).
	:param childID: Unique object ID of child being removed.

.. cpp:function:: void  GuiScriptNotifyCtrl::onChildResized(SimObjectId ID, SimObjectId childID)

	Called when a child is of this GUI is being resized.

	:param ID: Unique object ID assigned when created (this in script).
	:param childID: Unique object ID of child being resized.

.. cpp:function:: void  GuiScriptNotifyCtrl::onGainFirstResponder(SimObjectId ID)

	Called when this GUI gains focus.

	:param ID: Unique object ID assigned when created (this in script).

.. cpp:function:: void  GuiScriptNotifyCtrl::onLoseFirstResponder(SimObjectId ID)

	Called when this GUI loses focus.

	:param ID: Unique object ID assigned when created (this in script).

.. cpp:function:: void  GuiScriptNotifyCtrl::onParentResized(SimObjectId ID)

	Called when this GUI's parent is resized.

	:param ID: Unique object ID assigned when created (this in script).

.. cpp:function:: void  GuiScriptNotifyCtrl::onResize(SimObjectId ID)

	Called when this GUI is resized.

	:param ID: Unique object ID assigned when created (this in script).

Fields
------

.. cpp:member:: bool  GuiScriptNotifyCtrl::onChildAdded

	Enables/disables onChildAdded callback.

.. cpp:member:: bool  GuiScriptNotifyCtrl::onChildRemoved

	Enables/disables onChildRemoved callback.

.. cpp:member:: bool  GuiScriptNotifyCtrl::onChildResized

	Enables/disables onChildResized callback.

.. cpp:member:: bool  GuiScriptNotifyCtrl::onGainFirstResponder

	Enables/disables onGainFirstResponder callback.

.. cpp:member:: bool  GuiScriptNotifyCtrl::onLoseFirstResponder

	Enables/disables onLoseFirstResponder callback.

.. cpp:member:: bool  GuiScriptNotifyCtrl::onParentResized

	Enables/disables onParentResized callback.

.. cpp:member:: bool  GuiScriptNotifyCtrl::onResize

	Enables/disables onResize callback.
