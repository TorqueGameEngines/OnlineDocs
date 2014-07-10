RadialImpulseEvent
==================

Creates a physics-based impulse effect from a defined central point and magnitude.

Description
-----------

Creates a physics-based impulse effect from a defined central point and magnitude.

Methods
-------

.. cpp:function:: static void RadialImpulseEvent::send(string inPosition, float radius, float magnitude)

	Applies a radial impulse to any SceneObjects within the area of effect. This event is performed both server and client-side.

	:param position: Center point for this radial impulse.
	:param radius: Distance from the position for this radial impulse to affect.
	:param magnitude: The force applied to objects within the radius from the position of this radial impulse effect.

	Example::

		// Define the Position
		%position = "10.0 15.0 10.0";
		
		// Define the Radius
		%radius = "25.0";
		
		// Define the Magnitude
		%magnitude = "30.0"
		// Create a globalRadialImpulse physics effect.
		RadialImpulseEvent::send(%position,%radius,%magnitude);
