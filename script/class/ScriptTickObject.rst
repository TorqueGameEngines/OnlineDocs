ScriptTickObject
================

A ScriptObject that responds to tick and frame events.

Inherit:
	:doc:`ScriptObject`

Description
-----------

ScriptTickObject is a ScriptObject that adds callbacks for tick and frame events. Use setProcessTicks() to enable or disable the onInterpolateTick() and onProcessTick() callbacks. The callOnAdvanceTime property determines if the onAdvanceTime() callback is called.


Methods
-------


.. cpp:function:: bool ScriptTickObject::isProcessingTicks()

	Is this object wanting to receive tick notifications. If this object is set to receive tick notifications then its onInterpolateTick() and onProcessTick() callbacks are called.

	:return: True if object wants tick notifications 

.. cpp:function:: void ScriptTickObject::onAdvanceTime(float timeDelta)

	This is called every frame regardless if the object is set to process ticks, but only if the callOnAdvanceTime property is set to true.

	:param timeDelta: The time delta for this frame.

.. cpp:function:: void ScriptTickObject::onInterpolateTick(float delta)

	This is called every frame, but only if the object is set to process ticks.

	:param delta: The time delta for this frame.

.. cpp:function:: void ScriptTickObject::onProcessTick()

	Called once every 32ms if this object is set to process ticks.

.. cpp:function:: void ScriptTickObject::setProcessTicks(bool tick)

	Sets this object as either tick processing or not.

	:param tick: This object's onInterpolateTick() and onProcessTick() callbacks are called if set to true.

Fields
------


.. cpp:member:: bool  ScriptTickObject::callOnAdvanceTime

	Call the onAdvaceTime() callback.
