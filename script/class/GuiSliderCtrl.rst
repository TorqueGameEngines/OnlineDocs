GuiSliderCtrl
=============

A control that displays a value between its minimal and maximal bounds using a slider placed on a vertical or horizontal axis.

Inherit:
	:doc:`GuiControl`

Description
-----------

A control that displays a value between its minimal and maximal bounds using a slider placed on a vertical or horizontal axis.

A slider displays a value and allows that value to be changed by dragging a thumb control along the axis of the slider. In this way, the value is changed between its allowed minimum and maximum.

To hook up script code to the value changes of a slider, use the command and altCommand properties. command is executed once the thumb is released by the user whereas altCommand is called any time the slider value changes. When changing the slider value from script, however, trigger of altCommand is suppressed by default.

The orientation of a slider is automatically determined from the ratio of its width to its height. If a slider is taller than it is wide, it will be rendered with a vertical orientation. If it is wider than it is tall, it will be rendered with a horizontal orientation.

The rendering of a slider depends on the bitmap in the slider's profile. This bitmap must be a bitmap array comprised of at least five bitmap rectangles. The rectangles are used such that:

Example::

	// Create a sound source and a slider that changes the volume of the source.
	
	%source = sfxPlayOnce( "art/sound/testing", AudioLoop2D );
	
	new GuiSlider()
	{
	   // Update the sound source volume when the slider is being dragged and released.command = %source @ ".setVolume( $ThisControl.value );";
	
	   // Limit the range to 0..1 since that is the allowable range for sound volumes.range = "0 1";
	};


Methods
-------


.. cpp:function:: float GuiSliderCtrl::getValue()

	Get the current value of the slider based on the position of the thumb.

	:return: Slider position (from range.x to range.y). 

.. cpp:function:: bool GuiSliderCtrl::isThumbBeingDragged()

	Returns true if the thumb is currently being dragged by the user. This method is mainly useful for scrubbing type sliders where the slider position is sync'd to a changing value. When the user is dragging the thumb, however, the sync'ing should pause and not get in the way of the user.

.. cpp:function:: void GuiSliderCtrl::onMouseDragged()

	Called when the left mouse button is dragged across the slider.

.. cpp:function:: void GuiSliderCtrl::setValue(float pos, bool doCallback)

	Set position of the thumb on the slider.

	:param pos: New slider position (from range.x to range.y)
	:param doCallback: If true, the altCommand callback will be invoked

Fields
------


.. cpp:member:: Point2F  GuiSliderCtrl::range

	Min and max values corresponding to left and right slider position.

.. cpp:member:: bool  GuiSliderCtrl::snap

	Whether to snap the slider to tick marks.

.. cpp:member:: int  GuiSliderCtrl::ticks

	Spacing between tick marks in pixels. 0=off.

.. cpp:member:: float  GuiSliderCtrl::value

	The value corresponding to the current slider position.
