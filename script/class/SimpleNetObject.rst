SimpleNetObject
===============

A very simple example of a class derived from NetObject.

Inherit:
	:doc:`NetObject`

Description
-----------

This object exists purely for instructional purposes. It is primarily geared toward developers that wish to understand the inner-working of Torque 3D's networking system. This is not intended for actual game development.

Example::

	// On the server, create a new SimpleNetObject.  This is a ghost always
	// object so it will be immediately ghosted to all connected clients.
	$s = newSimpleNetObject();
	
	// All connected clients will see the following in their console:
	// 
	// Got message: Hello World!

Methods
-------

.. cpp:function:: void SimpleNetObject::setMessage(string msg)

	Sets the internal message variable. SimpleNetObject is set up to automatically transmit this new message to all connected clients. It will appear in the clients' console.

	:param msg: The new message to send

	Example::

		// On the server, create a new SimpleNetObject.  This is a ghost always
		// object so it will be immediately ghosted to all connected clients.
		$s = newSimpleNetObject();
		
		// All connected clients will see the following in their console:
		// 
		// Got message: Hello World!
		// Now again on the server, change the message.  This will cause it to
		// be sent to all connected clients.
		$s.setMessage("A new message from me!");
		
		// All connected clients will now see in their console:
		// 
		// Go message: A new message from me!
