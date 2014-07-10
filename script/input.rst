Input
=====

Functions and classes relating to to user input.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/ActionMap
	class/LeapMotionFrame
	class/RazerHydraFrame

Description
-----------

Input events come from the OS, are translated in the platform layer and then posted to the game. By default the game then checks the input event against a global ActionMap (which supercedes all other action handlers). If there is no action specified for the event, it is passed on to the GUI system. If the GUI does not handle the input event it is passed to the currently active (non-global) ActionMap stack. 

Example: the user presses the :kbd:`~` (tilde) key, which is bound in the global ActionMap to toggleConsole. 

This causes the console function associated with the bind to be executed, which in this case is toggleConsole, resulting in the console output window being shown. If the key had not been bound in the global map, it would have passed to the first gui that could have handled it, and if none did, it would pass to any game actions that were bound to that key. 

Input Events
~~~~~~~~~~~~

The following table represents all keyboard, mouse, and joystick input events available to stock Torque 3D. It should be noted that letter and number keys directly correlate to their mapping. For example "a" is literally the letter a. The button0, button1, and button2 are the most commonly used input mappings for left mouse button, right mouse button, and middle mouse button (respectively).

Keyboard General Events:

===========  ===========  ===========  ========
backspace    end          win_apps     tilde     
tab          home         cmd          minus      
return       left         equals       enter      
up           lopt         lbracket     opt
shift        right        ropt         rbracket
ctrl         down         numlock      backslash
alt          print        scrolllock   semicolon
pause        insert       rshift       apostrophe
capslock     delete       lcontrol     comma    
escape       help         rcontrol     period
space        win_lwindow  lalt         slash
pagedown     win_rwindow  ralt         lessthan
pageup 
===========  ===========  ===========  ========

.. note::

	All general keys can be bound by simply using the key... ex. "u" will trigger the u key response.

Keyboard Numpad Events:

=======  =======  ============  =============
numpad0  numpad5  numpad9       numpadminus    
numpad1  numpad6  numpadadmult  numpaddecimal    
numpad2  numpad7  numpadadd     numpaddivide    
numpad3  numpad8  numpadsep     numpadenter    
numpad4
=======  =======  ============  =============

Keyboard Function Key Events:

====  ====  ====  ====
f1    f7    f13   f19    
f2    f8    f14   f20    
f3    f9    f15   f21    
f4    f10   f16   f22    
f5    f11   f17   f23    
f6    f12   f18   f24 
====  ====  ====  ====

Joystick/Mouse Events:

=========  ==========  ==========  ==========
button0    button8     button16    button24    
button1    button9     button17    button25    
button2    button10    button18    button26    
button3    button11    button19    button27    
button4    button12    button20    button28    
button5    button13    button21    button29    
button6    button14    button22    button30    
button7    button15    button23    button31  
=========  ==========  ==========  ==========

Joystick/Mouse Axes:

=======  =======  ========  ========
xaxis    zaxis    ryaxis    slider    
yaxis    rxaxis   rzaxis
=======  =======  ========  ========

Joystick POV:

======  ======  =======  =======
xpov    dpov    xpov2    dpov2    
ypov    lpov    ypov2    lpov2    
upov    rpov    upov2    rpov2  
======  ======  =======  =======

Miscellaneous Events:

=======  =========
anykey   nomatch
=======  =========

Functions
---------

.. cpp:function:: void activateDirectInput() 	

	Activates DirectInput. Also activates any connected joysticks.

.. cpp:function:: void deactivateDirectInput() 	

	Disables DirectInput. Also deactivates any connected joysticks.

.. cpp:function:: void disableJoystick() 	

	Disables use of the joystick.

	Note:
	DirectInput must be enabled and active to use this function.

.. cpp:function:: void disableXInput() 	

	Disables XInput for Xbox 360 controllers.

.. cpp:function:: void echoInputState() 	

	Prints information to the console stating if DirectInput and a Joystick are enabled and active.

.. cpp:function:: bool enableJoystick() 	

	Enables use of the joystick.

	.. note::

		DirectInput must be enabled and active to use this function.

.. cpp:function:: bool enableXInput() 	

	Enables XInput for Xbox 360 controllers.

	.. note::

		XInput is enabled by default. Disable to use an Xbox 360 Controller as a joystick device.

.. cpp:function:: ActionMap getCurrentActionMap() 	

	Returns the current ActionMap.

	.. seealso:: :cpp:class:`ActionMap`

.. cpp:function:: int getXInputState(int controllerID, string property, bool current)			

	Queries the current state of a connected Xbox 360 controller.

	XInput Properties:

	* XI_THUMBLX, XI_THUMBLY - X and Y axes of the left thumbstick.
	* XI_THUMBRX, XI_THUMBRY - X and Y axes of the right thumbstick.
	* XI_LEFT_TRIGGER, XI_RIGHT_TRIGGER - Left and Right triggers.
	* SI_UPOV, SI_DPOV, SI_LPOV, SI_RPOV - Up, Down, Left, and Right on the directional pad.
	* XI_START, XI_BACK - The Start and Back buttons.
	* XI_LEFT_THUMB, XI_RIGHT_THUMB - Clicking in the left and right thumbstick.
	* XI_LEFT_SHOULDER, XI_RIGHT_SHOULDER - Left and Right bumpers.
	* XI_A, XI_B , XI_X, XI_Y - The A, B, X, and Y buttons.

	:param controllerID: Zero-based index of the controller to return information about.
	:param property: Name of input action being queried, such as "XI_THUMBLX".
	:param current: True checks current device in action.
	:returns: Button queried - 1 if the button is pressed, 0 if it's not. Thumbstick queried - Int representing displacement from rest position. Trigger queried - Int from 0 to 255 representing how far the trigger is displaced.

.. cpp:function:: bool isJoystickEnabled() 	

	Queries input manager to see if a joystick is enabled.

	:returns: 1 if a joystick exists and is enabled, 0 if it's not.

.. cpp:function:: bool isXInputConnected(int controllerID) 	

	Checks to see if an Xbox 360 controller is connected.

	:param controllerID: Zero-based index of the controller to check.
	:returns: 1 if the controller is connected, 0 if it isn't, and 205 if XInput hasn't been initialized.

.. cpp:function:: void lockMouse(bool isLocked) 	

	Lock or unlock the mouse to the window.

	When true, prevents the mouse from leaving the bounds of the game window.

.. cpp:function:: void resetXInput() 	

	Rebuilds the XInput section of the InputManager.

	Requests a full refresh of events for all controllers. Useful when called at the beginning of game code after actionMaps are set up to hook up all appropriate events.

.. cpp:function:: void rumble(string device, float xRumble, float yRumble)	

	Activates the vibration motors in the specified controller.

	The controller will constantly at it's xRumble and yRumble intensities until changed or told to stop.Valid inputs for xRumble/yRumble are [0 - 1].

	:param device: Name of the device to rumble.
	:param xRumble: Intensity to apply to the left motor.
	:param yRumble: Intensity to apply to the right motor.

	.. note::

		In an Xbox 360 controller, the left motor is low-frequency, while the right motor is high-frequency.
