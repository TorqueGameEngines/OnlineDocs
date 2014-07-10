Marker
======

A single joint, or knot, along a path.

Inherit:
	:doc:`SceneObject`

Description
-----------

A single joint, or knot, along a path. Should be stored inside a Path container object. A path markers can be one of three primary movement types: "normal", "Position Only", or "Kink".

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


Fields
------


.. cpp:member:: int  Marker::msToNext

	Milliseconds to next marker in sequence.

.. cpp:member:: int  Marker::seqNum

	Marker position in sequence of markers on this path.

.. cpp:member:: MarkerSmoothingType Marker::smoothingType

	Path smoothing at this marker/knot. "Linear" means no smoothing, while "Spline" means to smooth.

.. cpp:member:: MarkerKnotType Marker::type

	Type of this marker/knot. A "normal" knot will have a smooth camera translation/rotation effect. "Position Only" will do the same for translations, leaving rotation un-touched. Lastly, a "Kink" means the rotation will take effect immediately for an abrupt rotation change.
