GuiGameListMenuProfile
======================

A GuiControlProfile with additional fields specific to GuiGameListMenuCtrl.

Inherit:
	:doc:`GuiControlProfile`

Description
-----------

A GuiControlProfile with additional fields specific to GuiGameListMenuCtrl.

Example::

	newGuiGameListMenuProfile()
	{
	   hitAreaUpperLeft = "10 2";
	   hitAreaLowerRight = "190 18";
	   iconOffset = "10 2";
	   rowSize = "200 20";
	   //Properties not specific to this control have been omitted from this example.
	};


Fields
------


.. cpp:member:: Point2I  GuiGameListMenuProfile::hitAreaLowerRight

	Position of the lower right corner of the row hit area (relative to row's top left corner).

.. cpp:member:: Point2I  GuiGameListMenuProfile::hitAreaUpperLeft

	Position of the upper left corner of the row hit area (relative to row's top left corner).

.. cpp:member:: Point2I  GuiGameListMenuProfile::iconOffset

	Offset from the row's top left corner at which to render the row icon.

.. cpp:member:: Point2I  GuiGameListMenuProfile::rowSize

	The base size ("width height") of a row.
