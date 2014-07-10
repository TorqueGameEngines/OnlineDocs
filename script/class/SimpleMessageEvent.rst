SimpleMessageEvent
==================

A very simple example of a network event.

Description
-----------

This object exists purely for instructional purposes. It is primarily geared toward developers that wish to understand the inner-working of Torque 3D's networking system. This is not intended for actual game development.

Methods
-------

.. cpp:function:: static void SimpleMessageEvent::msg(NetConnection con, string message)

	Send a SimpleMessageEvent message to the specified connection. The far end that receives the message will print the message out to the console.

	:param con: The unique ID of the connection to transmit to
	:param message: The string containing the message to transmit

	Example::

		// Send a message to the other end of the given 
		NetConnectionSimpleMessageEvent::msg( %conn, "A message from me!");
		
		// The far end will see the following in the console
		// (Note: The number may be something other than 1796 as it is the SimObjectID
		// of the received event)
		// 
		// RMSG 1796  A message from me!
