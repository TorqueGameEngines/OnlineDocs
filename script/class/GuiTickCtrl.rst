GuiTickCtrl
===========

Brief Description.

Inherit:
	:doc:`GuiControl`

Description
-----------

This Gui Control is designed to be subclassed to let people create controls which want to receive update ticks at a constant interval. This class was created to be the Parent class of a control which used a DynamicTexture along with a VectorField to create warping effects much like the ones found in visualization displays for iTunes or Winamp. Those displays are updated at the framerate frequency. This works fine for those effects, however for an application of the same type of effects for things like Gui transitions the framerate-driven update frequency is not desirable because it does not allow the developer to be able to have any idea of a consistent user-experience.

Enter the ITickable interface. This lets the Gui control, in this case, update the dynamic texture at a constant rate of once per tick, even though it gets rendered every frame, thus creating a framerate-independent update frequency so that the effects are at a consistent speed regardless of the specifics of the system the user is on. This means that the screen-transitions will occur in the same time on a machine getting 300fps in the Gui shell as a machine which gets 150fps in the Gui shell.

Methods
-------

.. cpp:function:: void GuiTickCtrl::setProcessTicks(bool tick)

	This will set this object to either be processing ticks or not. This will set this object to either be processing ticks or not.

	:param tick: (optional) True or nothing to enable ticking, false otherwise.

	Example::

		// Turn off ticking for a control, like a MenuBar (declared previously)
		%sampleMenuBar.setProcessTicks(false);
