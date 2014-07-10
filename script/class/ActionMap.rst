ActionMap
=========

ActionMaps assign platform input events to console commands.

Inherit:
	:doc:`SimObject`

Description
-----------

Any platform input event can be bound in a single, generic way. In theory, the game doesn't need to know if the event came from the keyboard, mouse, joystick or some other input device. This allows users of the game to map keys and actions according to their own preferences. Game action maps are arranged in a stack for processing so individual parts of the game can define specific actions. For example, when the player jumps into a vehicle it could push a vehicle action map and pop the default player action map.

Creating an ActionMap
~~~~~~~~~~~~~~~~~~~~~

The input system allows for the creation of multiple ActionMaps, so long as they have unique names and do not already exist. It's a simple three step process.

#. Check to see if the ActionMap exists 
#. Delete it if it exists 
#. Instantiate the ActionMap

The following is an example of how to create a new ActionMap:

Example::

	if ( isObject( moveMap ) )
	   moveMap.delete();
	newActionMap(moveMap);

Binding Functions
~~~~~~~~~~~~~~~~~

Once you have created an ActionMap, you can start binding functionality to events. Currently, Torque 3D supports the following devices out of the box

* Mouse
* Keyboard
* Joystick/Gamepad
* Xbox 360 Controller

The two most commonly used binding methods are bind() and bindCmd(). Both are similar in that they will bind functionality to a device and event, but different in how the event is interpreted. With bind(), you specify a device, action to bind, then a function to be called when the event happens.

Example::

	// Simple function that prints to console// %val - Sent by the device letting the user know// if an input was pressed (true) or released (false)
	function testInput(%val)
	{
	   if(%val)
	     echo("Key is down");
	   elseecho("Key was released");
	}
	
	// Bind the K key to the testInput function
	moveMap.bind(keyboard, "k", testInput);

bindCmd is an alternative method for binding commands. This function is similar to bind(), except two functions are set to be called when the event is processed.

One will be called when the event is activated (input down), while the other is activated when the event is broken (input release). When using bindCmd(), pass the functions as strings rather than the function names.

Example::

	// Print to the console when the spacebar is pressed
	function onSpaceDown()
	{
	   echo("Space bar down!");
	}
	
	// Print to the console when the spacebar is released
	function onSpaceUp()
	{
	   echo("Space bar up!");
	}
	
	// Bind the commands onSpaceDown and onSpaceUp to spacebar events
	moveMap.bindCmd(keyboard, "space", "onSpaceDown();", "onSpaceUp();");

Switching ActionMaps
~~~~~~~~~~~~~~~~~~~~

Let's say you want to have different ActionMaps activated based on game play situations. A classic example would be first person shooter controls and racing controls in the same game. On foot, spacebar may cause your player to jump. In a vehicle, it may cause some kind of "turbo charge". You simply need to push/pop the ActionMaps appropriately:

First, create two separate ActionMaps:

Example::

	// Create the two ActionMaps
	if ( isObject( moveMap ) )
	   moveMap.delete();
	newActionMap(moveMap);
	
	if ( isObject( carMap ) )
	   carMap.delete();
	newActionMap(carMap);

Next, create the two separate functions. Both will be bound to spacebar, but not the same ActionMap:

Example::

	// Print to the console the player is jumping
	function playerJump(%val)
	{
	   if(%val)
	     echo("Player jumping!");
	}
	
	// Print to the console the vehicle is charging
	function turboCharge()
	{
	   if(%val)
	     echo("Vehicle turbo charging!");
	}

You are now ready to bind functions to your ActionMaps' devices:

Example::

	// Bind the spacebar to the playerJump function
	// when moveMap is the active ActionMap
	moveMap.bind(keyboard, "space", playerJump);
	
	// Bind the spacebar to the turboCharge function
	// when carMap is the active ActionMap
	carMap.bind(keyboard, "space", turboCharge);

Finally, you can use the push() and pop() commands on each ActionMap to toggle activation. To activate an ActionMap, use push():

Example::

	// Make moveMap the active action map
	// You should now be able to activate playerJump with spacebar
	moveMap.push();

To switch ActionMaps, first pop() the old one. Then you can push() the new one:

Example::

	// Deactivate moveMap
	moveMap.pop();
	
	// Activate carMap
	carMap.push();

Methods
-------

.. cpp:function:: bool ActionMap::bind(string device, string action, string command)

	Associates a function to an input event. When the input event is raised, the specified function will be called.

	:param device: The input device, such as mouse or keyboard.
	:param action: The input event, such as space, button0, etc.
	:param command: The function to bind to the action. Function must have a single boolean argument.

	:return: True if the binding was successful, false if the device was unknown or description failed.

	Example::

		// Simple function that prints to console
		// %val - Sent by the device letting the user know
		// if an input was pressed (true) or released (false)
		function testInput(%val)
		{
		   if(%val)
		     echo("Key is down");
		   elseecho("Key was released");
		}
		
		// Bind the K key to the testInput function
		moveMap.bind(keyboard, k, testInput);

.. cpp:function:: bool ActionMap::bind(string device, string action, string flag, string deadZone, string scale, string command)

	Associates a function and input parameters to an input event. When the input event is raised, the specified function will be called. Modifier flags may be specified to process dead zones, input inversion, and more. Valid modifier flags: 
	
	* R - Input is Ranged.
	* S - Input is Scaled.
	* I - Input is inverted.
	* D - Dead zone is present.
	* N - Input should be re-fit to a non-linear scale.

	:param device: The input device, such as mouse or keyboard.
	:param action: The input event, such as space, button0, etc.
	:param flag: Modifier flag assigned during binding, letting event know there are additional parameters to consider.
	:param deadZone: Restricted region in which device motion will not be acknowledged.
	:param scale: Modifies the deadZone region.
	:param command: The function bound to the action. Must take in a single argument.

	:return: True if the binding was successful, false if the device was unknown or description failed.

	Example::

		// Simple function that adjusts the pitch of the camera 
		// based on the mouses movement along the X axis.
		function testPitch(%val)
		{
		   %pitchAdj = getMouseAdjustAmount(%val);
		    $mvPitch += %pitchAdj;
		}
		
		// Bind the mouses X axis to the testPitch function
		// DI is flagged, meaning input is inverted and has a deadzone
		%this.bind( mouse, "xaxis", "DI", "-0.23 0.23", testPitch );

.. cpp:function:: bool ActionMap::bindCmd(string device, string action, string makeCmd, string breakCmd)

	Associates a make command and optional break command to a specified input device action. Must include parenthesis and semicolon in the make and break command strings.

	:param device: The device to bind to. Can be a keyboard, mouse, joystick or gamepad.
	:param action: The device action to bind to. The action is dependant upon the device. Specify a key for keyboards.
	:param makeCmd: The command to execute when the device/action is made.
	:param breakCmd: [optional] The command to execute when the device or action is unmade.

	:return: True the bind was successful, false if the device was unknown or description failed. 

	Example::

		// Print to the console when the spacebar is pressed
		function onSpaceDown()
		{
		   echo("Space bar down!");
		}
		
		// Print to the console when the spacebar is released
		function onSpaceUp()
		{
		   echo("Space bar up!");
		}
		
		// Bind the commands onSpaceDown() and onSpaceUp() to spacebar events
		
		moveMap.bindCmd(keyboard, "space", "onSpaceDown();", "onSpaceUp();");

.. cpp:function:: bool ActionMap::bindObj(string device, string action, string command, SimObjectID object)

	Associates a function to an input event for a specified class or object. You must specify a device, the action to bind, a function, and an object to be called when the event happens. The function specified must be set to receive a single boolean value passed.

	:param device: The input device, such as mouse or keyboard.
	:param action: The input event, such as space, button0, etc.
	:param command: The function bound to the action.
	:param object: The object or class bound to the action.

	:return: True if the binding was successful, false if the device was unknown or description failed.

	Example::

		moveMap.bindObj(keyboard, "numpad1", "rangeChange", %player);

.. cpp:function:: bool ActionMap::bindObj(string device, string action, string flag, string deadZone, string scale, string command, SimObjectID object)

	Associates a function to an input event for a specified class or object. You must specify a device, the action to bind, a function, and an object to be called when the event happens. The function specified must be set to receive a single boolean value passed. Modifier flags may be specified to process dead zones, input inversion, and more. Valid modifier flags: 
	
	* R - Input is Ranged.
	* S - Input is Scaled.
	* I - Input is inverted.
	* D - Dead zone is present.
	* N - Input should be re-fit to a non-linear scale.

	:param device: The input device, such as mouse or keyboard.
	:param action: The input event, such as space, button0, etc.
	:param flag: Modifier flag assigned during binding, letting event know there are additional parameters to consider.
	:param deadZone: [Required only when flag is set] Restricted region in which device motion will not be acknowledged.
	:param scale: [Required only when flag is set] Modifies the deadZone region.
	:param command: The function bound to the action.
	:param object: The object or class bound to the action.

	:return: True if the binding was successful, false if the device was unknown or description failed.

	Example::

		// Bind the mouses movement along the x-axis to 
		// the testInput function of the Player class
		// DSI is flagged, meaning input is inverted, 
		// has scale and has a deadzone
		%this.bindObj( mouse, "xaxis", "DSI", %deadZone, %scale, "testInput", %player );

.. cpp:function:: string ActionMap::getBinding(string command)

	Gets the ActionMap binding for the specified command. Use getField() on the return value to get the device and action of the binding.

	:param command: The function to search bindings for.

	:return: The binding against the specified command. Returns an empty string("") if a binding wasn't found. 

	Example::

		// Find what the function "jump()" is bound to in moveMap
		%bind = moveMap.getBinding( "jump" );
		
		if ( %bind !$= "" )
		{
		   // Find out what device is used in the binding
		   %device = getField( %bind, 0 );
		
		   // Find out what action (such as a key) is used in the binding
		   %action = getField( %bind, 1 );
		}

.. cpp:function:: string ActionMap::getCommand(string device, string action)

	Gets ActionMap command for the device and action.

	:param device: The device that was bound. Can be a keyboard, mouse, joystick or a gamepad.
	:param action: The device action that was bound. The action is dependant upon the device. Specify a key for keyboards.

	:return: The command against the specified device and action. 

	Example::

		// Find what function is bound to a devices action
		// In this example, "jump()" was assigned to the space key in another script
		%command = moveMap.getCommand("keyboard", "space");
		
		// Should print "jump" in the console
		echo(%command)

.. cpp:function:: string ActionMap::getDeadZone(string device, string action)

	Gets the Dead zone for the specified device and action.

	:param device: The device that was bound. Can be a keyboard, mouse, joystick or a gamepad.
	:param action: The device action that was bound. The action is dependant upon the device. Specify a key for keyboards.

	:return: The dead zone for the specified device and action. Returns "0 0" if there is no dead zone or an empty string("") if the mapping was not found. 

	Example::

		%deadZone = moveMap.getDeadZone( "gamepad", "thumbrx");

.. cpp:function:: float ActionMap::getScale(string device, string action)

	Get any scaling on the specified device and action.

	:param device: The device that was bound. Can be keyboard, mouse, joystick or gamepad.
	:param action: The device action that was bound. The action is dependant upon the device. Specify a key for keyboards.

	:return: Any scaling applied to the specified device and action. 

	Example::

		%scale = %moveMap.getScale( "gamepad", "thumbrx");

.. cpp:function:: bool ActionMap::isInverted(string device, string action)

	Determines if the specified device and action is inverted. Should only be used for scrolling devices or gamepad/joystick axes.

	:param device: The device that was bound. Can be a keyboard, mouse, joystick or a gamepad.
	:param action: The device action that was bound. The action is dependant upon the device. Specify a key for keyboards.

	:return: True if the specified device and action is inverted. 

	Example::

		%if ( moveMap.isInverted( "mouse", "xaxis"))
		   echo("Mouses xAxis is inverted");

.. cpp:function:: void ActionMap::pop()

	Pop the ActionMap off the ActionMap stack. Deactivates an ActionMap and removes it from the  stack.

	Example::

		// Deactivate moveMap
		moveMap.pop();

.. cpp:function:: void ActionMap::push()

	Push the ActionMap onto the ActionMap stack. Activates an ActionMap and placees it at the top of the ActionMap stack.

	Example::

		// Make moveMap the active action map
		moveMap.push();

.. cpp:function:: void ActionMap::save(string fileName, bool append)

	Saves the ActionMap to a file or dumps it to the console.

	:param fileName: The file path to save the ActionMap to. If a filename is not specified the ActionMap will be dumped to the console.
	:param append: Whether to write the ActionMap at the end of the file or overwrite it.

	Example::

		// Write out the actionmap into the config.cs file
		moveMap.save( "scripts/client/config.cs" );

.. cpp:function:: bool ActionMap::unbind(string device, string action)

	Removes the binding on an input device and action.

	:param device: The device to unbind from. Can be a keyboard, mouse, joystick or a gamepad.
	:param action: The device action to unbind from. The action is dependant upon the device. Specify a key for keyboards.

	:return: True if the unbind was successful, false if the device was unknown or description failed.

	Example::

		moveMap.unbind("keyboard", "space");

.. cpp:function:: bool ActionMap::unbindObj(string device, string action, string obj)

	Remove any object-binding on an input device and action.

	:param device: The device to bind to. Can be keyboard, mouse, joystick or gamepad.
	:param action: The device action to unbind from. The action is dependant upon the device. Specify a key for keyboards.
	:param obj: The object to perform unbind against.

	:return: True if the unbind was successful, false if the device was unknown or description failed. 

	Example::

		moveMap.unbindObj("keyboard", "numpad1", "rangeChange", %player);
