Lightning
=========

An emitter for lightning bolts.

Inherit:
	:doc:`GameBase`

Description
-----------

An emitter for lightning bolts.

Lightning strike events are created on the server and transmitted to all clients to render the bolt. The strike may be followed by a random thunder sound. Player or Vehicle objects within the Lightning strike range can be hit and damaged by bolts.


Methods
-------


.. cpp:function:: void Lightning::applyDamage(Point3F hitPosition, Point3F hitNormal, SceneObject hitObject)

	Informs an object that it was hit by a lightning bolt and needs to take damage.

	:param hitPosition: World position hit by the lightning bolt.
	:param hitNormal: Surface normal at hitPosition.
	:param hitObject: Player or Vehicle object that was hit.

	Example::

		function Lightning::applyDamage( %this, %hitPosition, %hitNormal, %hitObject )
		{
		   // apply damage to the player
		   %hitObject.applyDamage( 25 );
		}

.. cpp:function:: void Lightning::strikeObject(int id)

	Creates a LightningStrikeEvent which strikes a specific object.

.. cpp:function:: void Lightning::strikeRandomPoint()

	Creates a LightningStrikeEvent which attempts to strike and damage a random object in range of the Lightning object.

	Example::

		// Generate a damaging lightning strike effect on all clients
		%lightning.strikeRandomPoint();

.. cpp:function:: void Lightning::warningFlashes()

	Creates a LightningStrikeEvent that triggers harmless lightning bolts on all clients. No objects will be damaged by these bolts.

	Example::

		// Generate a harmless lightning strike effect on all clients
		%lightning.warningFlashes();

Fields
------


.. cpp:member:: float  Lightning::boltStartRadius

	Radial distance from the center of the Lightning object for the start point of the bolt. The actual start point will be a random point within this radius.

.. cpp:member:: float  Lightning::chanceToHitTarget

	Percentage chance (0-1) that a given lightning bolt will hit something.

.. cpp:member:: ColorF  Lightning::color

	Color to blend the strike texture with.

.. cpp:member:: ColorF  Lightning::fadeColor

	Color to blend the strike texture with when the bolt is fading away. Bolts fade away automatically shortly after the strike occurs.

.. cpp:member:: float  Lightning::strikeRadius

	Horizontal size (XY plane) of the search box used to find and damage Player or Vehicle objects within range of the strike. Only the object at highest altitude with a clear line of sight to the bolt will be hit.

.. cpp:member:: int  Lightning::strikesPerMinute

	Number of lightning strikes to perform per minute. Automatically invokes strikeRandomPoint() at regular intervals.

.. cpp:member:: float  Lightning::strikeWidth

	Width of a lightning bolt.

.. cpp:member:: bool  Lightning::useFog

	Controls whether lightning bolts are affected by fog when they are rendered.
