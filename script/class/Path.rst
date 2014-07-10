Path
====

A spline along which various objects can move along.

Inherit:
	:doc:`SimGroup`

Description
-----------

A spline along which various objects can move along. The spline object acts like a container for Marker objects, which make up the joints, or knots, along the path. Paths can be assigned a speed, can be looping or non-looping. Each of a path's markers can be one of three primary movement types: "normal", "Position Only", or "Kink".

Example::

	new path()
	   {
	     isLooping = "1";
	
	     newMarker()
	      {
	         seqNum = "0";
	         type = "Normal";
	         msToNext = "1000";
	         smoothingType = "Spline";
	         position = "-0.054708 -35.0612 234.802";
	         rotation = "1 0 0 0";
	      };
	
	   };


Methods
-------


.. cpp:function:: int Path::getPathId()

	Returns the PathID (not the object ID) of this path.

	:return: PathID (not the object ID) of this path. 

	Example::

		// Acquire the PathID of this path object.
		%pathID = %thisPath.getPathId();

Fields
------


.. cpp:member:: bool  Path::isLooping

	If this is true, the loop is closed, otherwise it is open.
