AIPlayer
========

A Player object not controlled by conventional input, but by an AI engine.

Inherit:
	:doc:`Player`

Description
-----------

The AIPlayer provides a Player object that may be controlled from script. You control where the player moves and how fast. You may also set where the AIPlayer is aiming at -- either a location or another game object.

The AIPlayer class does not have a datablock of its own. It makes use of the PlayerData datablock to define how it looks, etc. As the AIPlayer is an extension of the Player class it can mount objects and fire weapons, or mount vehicles and drive them.

While the PlayerData datablock is used, there are a number of additional callbacks that are implemented by AIPlayer on the datablock. These are listed here:

void onReachDestination(AIPlayer obj)
	Called when the player has reached its set destination using the setMoveDestination() method. The actual point at which this callback is called is when the AIPlayer is within the mMoveTolerance of the defined destination.

void onMoveStuck(AIPlayer obj)
	While in motion, if an AIPlayer has moved less than moveStuckTolerance within a single tick, this callback is called. From here you could choose an alternate destination to get the AIPlayer moving again.

void onTargetEnterLOS(AIPlayer obj)
	When an object is being aimed at (following a call to setAimObject()) and the targeted object enters the AIPlayer's line of sight, this callback is called. The LOS test is a ray from the AIPlayer's eye position to the center of the target's bounding box. The LOS ray test only checks against interiors, statis shapes, and terrain.

void onTargetExitLOS(AIPlayer obj)
	When an object is being aimed at (following a call to setAimObject()) and the targeted object leaves the AIPlayer's line of sight, this callback is called. The LOS test is a ray from the AIPlayer's eye position to the center of the target's bounding box. The LOS ray test only checks against interiors, statis shapes, and terrain.

Example::

	// Create the demo player object
	%player = new AiPlayer()
	{
	   dataBlock = DemoPlayer;
	   path = "";
	};

Methods
-------

.. cpp:function:: void AIPlayer::clearAim()

	Use this to stop aiming at an object or a point.

.. cpp:function:: Point3F AIPlayer::getAimLocation()

	Returns the point the AIPlayer is aiming at. This will reflect the position set by setAimLocation() , or the position of the object that the bot is now aiming at. If the bot is not aiming at anything, this value will change to whatever point the bot's current line-of-sight intercepts.

	:return: World space coordinates of the object AI is aiming at. Formatted as "X Y Z".

.. cpp:function:: int AIPlayer::getAimObject()

	Gets the object the AIPlayer is targeting.

	:return:  is aiming at.

.. cpp:function:: Point3F AIPlayer::getMoveDestination()

	Get the AIPlayer's current destination.

	:return: Returns a point containing the "x y z" position of the AIPlayer's current move destination. If no move destination has yet been set, this returns "0 0 0".

.. cpp:function:: float AIPlayer::getMoveSpeed()

	Gets the move speed of an AI object.

	:return: A speed multiplier between 0.0 and 1.0.

.. cpp:function:: void AIPlayer::setAimLocation(Point3F target)

	Tells the AIPlayer to aim at the location provided.

	:param target: An "x y z" position in the game world to target.

.. cpp:function:: void AIPlayer::setAimObject(GameBase targetObject, Point3F offset)

	Sets the AIPlayer's target object. May optionally set an offset from target location.

	:param targetObject: The object to target
	:param offset: Optional three-element offset vector which will be added to the position of the aim object.

	Example::

		// Without an offset
		%ai.setAimObject(%target);
		
		// With an offset
		// Cause our AI object to aim at the target
		// offset (0, 0, 1) so you dont aim at the targets feet
		%ai.setAimObject(%target, "0 0 1");

.. cpp:function:: void AIPlayer::setMoveDestination(Point3F goal, bool slowDown)

	Tells the AI to move to the location provided.

	:param goal: Coordinates in world space representing location to move to.
	:param slowDown: A boolean value. If set to true, the bot will slow down when it gets within 5-meters of its move destination. If false, the bot will stop abruptly when it reaches the move destination. By default, this is true.

.. cpp:function:: void AIPlayer::setMoveSpeed(float speed)

	Sets the move speed for an AI object.

	:param speed: A speed multiplier between 0.0 and 1.0. This is multiplied by the AIPlayer's base movement rates (as defined in its PlayerData datablock)

.. cpp:function:: void AIPlayer::stop()

	Tells the AIPlayer to stop moving.

Fields
------

.. cpp:member:: float  AIPlayer::mMoveTolerance

	Distance from destination before stopping. When the AIPlayer is moving to a given destination it will move to within this distance of the destination and then stop. By providing this tolerance it helps the AIPlayer from never reaching its destination due to minor obstacles, rounding errors on its position calculation, etc. By default it is set to 0.25.

.. cpp:member:: int  AIPlayer::moveStuckTestDelay

	The number of ticks to wait before testing if the AIPlayer is stuck. When the AIPlayer is asked to move, this property is the number of ticks to wait before the AIPlayer starts to check if it is stuck. This delay allows the AIPlayer to accelerate to full speed without its initial slow start being considered as stuck.

.. cpp:member:: float  AIPlayer::moveStuckTolerance

	Distance tolerance on stuck check. When the AIPlayer is moving to a given destination, if it ever moves less than this tolerance during a single tick, the AIPlayer is considered stuck. At this point the onMoveStuck() callback is called on the datablock.
