GuiAutoScrollCtrl
=================

Inherit:
	:doc:`GuiTickCtrl`

Description
-----------

A container that scrolls its child control up over time.

This container can be used to scroll a single child control in either of the four directions.

Example::

	// Create a GuiAutoScrollCtrl that scrolls a long text of credits.newGuiAutoScrollCtrl( CreditsScroller )
	{
	   position = "0 0";
	   extent = Canvas.extent.x SPC Canvas.extent.y;
	
	   scrollDirection = "Up"; // Scroll upwards.startDelay = 4; // Wait 4 seconds before starting to scroll.isLooping = false; // Dont loop the credits.scrollOutOfSight = true; // Scroll up fully.newGuiMLTextCtrl()
	   {
	      text = $CREDITS;
	   };
	};
	
	function CreditsScroller::onComplete( %this )
	{
	   // Switch back to main menu after credits have rolled.
	   Canvas.setContent( MainMenu );
	}
	
	// Start rolling credits.
	Canvas.setContent( CreditsScroller );


Methods
-------


.. cpp:function:: void GuiAutoScrollCtrl::onComplete()

	Called when the child control has been scrolled in entirety.

.. cpp:function:: void GuiAutoScrollCtrl::onReset()

	Called when the child control is reset to its initial position and the cycle starts again.

.. cpp:function:: void GuiAutoScrollCtrl::onStart()

	Called when the control starts to scroll.

.. cpp:function:: void GuiAutoScrollCtrl::onTick()

	Called every 32ms on the control.

.. cpp:function:: void GuiAutoScrollCtrl::reset()

	Reset scrolling.

Fields
------


.. cpp:member:: int  GuiAutoScrollCtrl::childBorder

	Padding to put around child control (in pixels).

.. cpp:member:: bool  GuiAutoScrollCtrl::isLooping

	If true, the scrolling will reset to the beginning once completing a cycle.

.. cpp:member:: float  GuiAutoScrollCtrl::resetDelay

	Seconds to wait after scrolling completes before resetting and starting over.

.. cpp:member:: GuiAutoScrollDirection GuiAutoScrollCtrl::scrollDirection

	Direction in which the child control is moved.

.. cpp:member:: bool  GuiAutoScrollCtrl::scrollOutOfSight

	If true, the child control will be completely scrolled out of sight; otherwise it will only scroll until the other end becomes visible.

.. cpp:member:: float  GuiAutoScrollCtrl::scrollSpeed

	Scrolling speed in pixels per second.

.. cpp:member:: float  GuiAutoScrollCtrl::startDelay

	Seconds to wait before starting to scroll.
