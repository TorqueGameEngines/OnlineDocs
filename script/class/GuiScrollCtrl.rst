GuiScrollCtrl
=============

A container that allows to view one or more possibly larger controls inside its area by providing horizontal and/or vertical scroll bars.

Inherit:
	:doc:`GuiContainer`

Description
-----------

A container that allows to view one or more possibly larger controls inside its area by providing horizontal and/or vertical scroll bars.

Methods
-------

.. cpp:function:: void GuiScrollCtrl::computeSizes()

	Refresh sizing and positioning of child controls.

.. cpp:function:: Point2I GuiScrollCtrl::getScrollPosition()

	Get the current coordinates of the scrolled content.

	:return: The current position of the scrolled content. 

.. cpp:function:: int GuiScrollCtrl::getScrollPositionX()

	Get the current X coordinate of the scrolled content.

	:return: The current X coordinate of the scrolled content. 

.. cpp:function:: int GuiScrollCtrl::getScrollPositionY()

	Get the current Y coordinate of the scrolled content.

	:return: The current Y coordinate of the scrolled content. 

.. cpp:function:: void GuiScrollCtrl::onScroll()

	Called each time the child controls are scrolled by some amount.

.. cpp:function:: void GuiScrollCtrl::scrollToBottom()

	Scroll all the way to the bottom of the vertical scrollbar and the left of the horizontal bar.

.. cpp:function:: void GuiScrollCtrl::scrollToObject(GuiControl control)

	Scroll the control so that the given child control is visible.

	:param control: A child control.

.. cpp:function:: void GuiScrollCtrl::scrollToTop()

	Scroll all the way to the top of the vertical and left of the horizontal scrollbar.

.. cpp:function:: void GuiScrollCtrl::setScrollPosition(int x, int y)

	Set the position of the scrolled content.

	:param x: Position on X axis.
	:param y: Position on y axis.

Fields
------

.. cpp:member:: Point2I  GuiScrollCtrl::childMargin

	Padding region to put around child contents.

.. cpp:member:: bool  GuiScrollCtrl::constantThumbHeight


.. cpp:member:: GuiScrollBarBehavior GuiScrollCtrl::hScrollBar

	When to display the horizontal scrollbar.

.. cpp:member:: bool  GuiScrollCtrl::lockHorizScroll

	Horizontal scrolling not allowed if set.

.. cpp:member:: bool  GuiScrollCtrl::lockVertScroll

	Vertical scrolling not allowed if set.

.. cpp:member:: int  GuiScrollCtrl::mouseWheelScrollSpeed

	Pixels/Tick - if not positive then mousewheel scrolling occurs instantly (like other scrolling).

.. cpp:member:: GuiScrollBarBehavior GuiScrollCtrl::vScrollBar

	When to display the vertical scrollbar.

.. cpp:member:: bool  GuiScrollCtrl::willFirstRespond

