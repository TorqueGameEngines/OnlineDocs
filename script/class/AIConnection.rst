AIConnection
============

Special client connection driven by an AI, rather than a human.

Inherit:
	:doc:`GameConnection`

Description
-----------

Unlike other net connections, AIConnection is intended to run unmanned. Rather than gathering input from a human using a device, move events, triggers, and look events are driven through functions like AIConnection::setMove.

In addition to having its own set of functions for managing client move events, a member variable inherited by GameConnection is toggle: mAIControlled. This is useful for a server to determine if a connection is AI driven via the function GameConnection::isAIControlled

AIConnection is an alternative to manually creating an AI driven game object. When you want the server to manage AI, you will create a specific one from script using a class like AIPlayer. If you do not want the server managing the AI and wish to simulate a complete client connection, you will use AIConnection

.To get more specific, if you want a strong alternative to AIPlayer (and wish to make use of the AIConnection structure), consider AIClient. AIClient inherits from AIConnection, contains quite a bit of functionality you will find in AIPlayer, and has its own Player object.

Example::

	// Create a new AI client connection
	%botConnection = aiConnect("MasterBlaster" @ %i, -1, 0.5, false, "SDF", 1.0);
	
	// In another area of the code, you can locate this and any other AIConnections
	// using the isAIControlled function
	for(%i = 0; %i < ClientGroup.getCount(); %i++)
	{
	   %client = ClientGroup.getObject(%i);
	   if(%client.isAIControlled())
	   {
	      // React to this AI controlled client
	   }
	}


Methods
-------

.. cpp:function:: float AIConnection::getMove(string field)

	Get the given field of a move.

	:param field: One of {'x','y','z','yaw','pitch','roll'}

	:return: The requested field on the current move. 

.. cpp:function:: bool AIConnection::getTrigger(int trigger)

	Is the given trigger set?

.. cpp:function:: void AIConnection::setFreeLook(bool isFreeLook)

	Enable/disable freelook on the current move.

.. cpp:function:: void AIConnection::setMove(string field, float value)

	Set a field on the current move.

	:param field: One of {'x','y','z','yaw','pitch','roll'}
	:param value: Value to set field to.

.. cpp:function:: void AIConnection::setTrigger(int trigger, bool set)

	Set a trigger.

Fields
------

.. cpp:member:: string  AIConnection::getAddress


.. cpp:member:: bool  AIConnection::getFreeLook

	getFreeLook() Is freelook on for the current move?
