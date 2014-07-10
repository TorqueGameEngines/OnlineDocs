AIClient
========

Simulated client driven by AI commands.

Inherit:
	:doc:`AIConnection`

Description
-----------

This object is derived from the AIConnection class. It introduces its own Player object to solidify the purpose of this class: Simulated client connecting as a player

To get more specific, if you want a strong alternative to AIPlayer (and wish to make use of the AIConnection structure), consider AIClient. AIClient inherits from AIConnection, contains quite a bit of functionality you will find in AIPlayer, and has its own Player object.


Fields
------


.. cpp:member:: string  AIClient::getAimLocation

	ai.getAimLocation();

.. cpp:member:: string  AIClient::getLocation

	ai.getLocation();

.. cpp:member:: string  AIClient::getMoveDestination

	ai.getMoveDestination();

.. cpp:member:: int  AIClient::getTargetObject

	ai.getTargetObject();

.. cpp:member:: void  AIClient::missionCycleCleanup

	ai.missionCycleCleanup();

.. cpp:member:: void  AIClient::move

	ai.move();

.. cpp:member:: void  AIClient::moveForward

	ai.moveForward();

.. cpp:member:: void  AIClient::setAimLocation

	ai.setAimLocation( x y z );

.. cpp:member:: void  AIClient::setMoveDestination

	ai.setMoveDestination( x y z );

.. cpp:member:: void  AIClient::setMoveSpeed

	ai.setMoveSpeed( float );

.. cpp:member:: void  AIClient::setTargetObject

	ai.setTargetObject( obj );

.. cpp:member:: void  AIClient::stop

	ai.stop();
