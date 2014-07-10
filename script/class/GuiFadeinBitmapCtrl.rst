GuiFadeinBitmapCtrl
===================

A GUI control which renders a black square over a bitmap image. The black square will fade out, then fade back in after a determined time. This control is especially useful for transitions and splash screens.

Inherit:
	:doc:`GuiBitmapCtrl`

Description
-----------

A GUI control which renders a black square over a bitmap image. The black square will fade out, then fade back in after a determined time. This control is especially useful for transitions and splash screens.

Example::

	newGuiFadeinBitmapCtrl()
	   {
	      fadeinTime = "1000";
	      waitTime = "2000";
	      fadeoutTime = "1000";
	      done = "1";
	      // Additional GUI properties that are not specific to GuiFadeinBitmapCtrl have been omitted from this example.
	   };


Methods
-------


.. cpp:function:: void GuiFadeinBitmapCtrl::click()

	Informs the script level that this object received a Click event from the cursor or keyboard.

	Example::

		GuiFadeInBitmapCtrl::click(%this)
		   {
		      // Code to run when click occurs
		   }

.. cpp:function:: void GuiFadeinBitmapCtrl::onDone()

	Informs the script level that this object has completed is fade cycle.

	Example::

		GuiFadeInBitmapCtrl::onDone(%this)
		   {
		      // Code to run when the fade cycle completes
		   }

Fields
------


.. cpp:member:: bool  GuiFadeinBitmapCtrl::done

	Whether the fade cycle has finished running.

.. cpp:member:: ColorF  GuiFadeinBitmapCtrl::fadeColor

	Color to fade in from and fade out to.

.. cpp:member:: EaseF  GuiFadeinBitmapCtrl::fadeInEase

	Easing curve for fade-in.

.. cpp:member:: int  GuiFadeinBitmapCtrl::fadeInTime

	Milliseconds for the bitmap to fade in.

.. cpp:member:: EaseF  GuiFadeinBitmapCtrl::fadeOutEase

	Easing curve for fade-out.

.. cpp:member:: int  GuiFadeinBitmapCtrl::fadeOutTime

	Milliseconds for the bitmap to fade out.

.. cpp:member:: int  GuiFadeinBitmapCtrl::waitTime

	Milliseconds to wait after fading in before fading out the bitmap.
