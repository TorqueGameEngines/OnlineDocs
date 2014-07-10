Debris
======

datablock for properties of individual debris objects.

Inherit:
	:doc:`GameBase`

Description
-----------

Base debris class. Uses the DebrisData datablock for properties of individual debris objects.

Debris is typically made up of a shape and up to two particle emitters. In most cases Debris objects are not created directly. They are usually produced automatically by other means, such as through the Explosion class. When an explosion goes off, its ExplosionData datablock determines what Debris to emit.

Example::

	datablock ExplosionData(GrenadeLauncherExplosion)
	{
	   // Assiging debris data
	   debris = GrenadeDebris;
	
	   // Adjust how debris is ejected
	   debrisThetaMin = 10;
	   debrisThetaMax = 60;
	   debrisNum = 4;
	   debrisNumVariance = 2;
	   debrisVelocity = 25;
	   debrisVelocityVariance = 5;
	
	   // Note: other ExplosionData properties are not listed for this example
	};


Methods
-------


.. cpp:function:: bool Debris::init(string inputPosition, string inputVelocity)

	Manually set this piece of debris at the given position with the given velocity. Usually you do not manually create Debris objects as they are generated through other means, such as an Explosion . This method exists when you do manually create a Debris object and want to have it start moving.

	:param inputPosition: Position to place the debris.
	:param inputVelocity: Velocity to move the debris after it has been placed.

	:return: Always returns true. 

	Example::

		// Define the position
		%position = "1.0 1.0 1.0";
		
		// Define the velocity
		%velocity = "1.0 0.0 0.0";
		
		// Inform the debris object of its new position and velocity
		%debris.init(%position,%velocity);

Fields
------


.. cpp:member:: float  Debris::lifetime

	Length of time for this debris object to exist. When expired, the object will be deleted. The initial lifetime value comes from the DebrisData datablock.
