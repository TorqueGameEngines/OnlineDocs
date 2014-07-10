TimeOfDay
=========

Environmental object that triggers a day/night cycle in level.

Inherit:
	:doc:`SceneObject`

Description
-----------

Environmental object that triggers a day/night cycle in level.

Example::

	newTimeOfDay(tod)
	{
	   axisTilt = "23.44";
	   dayLength = "120";
	   startTime = "0.15";
	   time = "0.15";
	   play = "0";
	   azimuthOverride = "572.958";
	   dayScale = "1";
	   nightScale = "1.5";
	   position = "598.399 550.652 196.297";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	   canSave = "1";
	   canSaveDynamicFields = "1";
	};


Methods
-------


.. cpp:function:: void TimeOfDay::addTimeOfDayEvent(float elevation, string identifier)


.. cpp:function:: void TimeOfDay::animate(float elevation, float degreesPerSecond)


.. cpp:function:: void TimeOfDay::setDayLength(float seconds)


.. cpp:function:: void TimeOfDay::setPlay(bool enabled)


.. cpp:function:: void TimeOfDay::setTimeOfDay(float time)


Fields
------


.. cpp:member:: float  TimeOfDay::axisTilt

	The angle in degrees between global equator and tropic.

.. cpp:member:: float  TimeOfDay::azimuthOverride


.. cpp:member:: float  TimeOfDay::dayLength

	The length of a virtual day in real world seconds.

.. cpp:member:: float  TimeOfDay::dayScale

	Scalar applied to time that elapses while the sun is up.

.. cpp:member:: float  TimeOfDay::nightScale

	Scalar applied to time that elapses while the sun is down.

.. cpp:member:: bool  TimeOfDay::play

	True when the TimeOfDay object is operating.

.. cpp:member:: float  TimeOfDay::startTime


.. cpp:member:: float  TimeOfDay::time

	Current time of day.
