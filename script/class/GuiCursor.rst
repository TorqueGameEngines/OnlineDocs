GuiCursor
=========

Acts as a skin for the cursor, where each GuiCursor object can have its own look and click-zone.

Inherit:
	:doc:`SimObject`

Description
-----------

GuiCursors act as skins for the cursor in the game, where each individual GuiCursor can have its own defined imagemap, click zone and render offset. This allows a game to easily support a wide range of cursors. The active cursor can de changed for each Canvas using canvasObj.setCursor(GuiCursor);.

Example::

	newGuiCursor(DefaultCursor)
	{
	   hotSpot = "1 1";
	   renderOffset = "0 0";
	   bitmapName = "~/art/gui/images/defaultCursor";
	};


Fields
------

.. cpp:member:: filename  GuiCursor::bitmapName

	File name of the bitmap for the cursor.

.. cpp:member:: Point2I  GuiCursor::hotSpot

	The location of the cursor's hot spot (which pixel carries the click).

.. cpp:member:: Point2F  GuiCursor::renderOffset

	Offset of the bitmap, where 0 signifies left edge of the bitmap, 1, the right. Similarly for the Y-component.
