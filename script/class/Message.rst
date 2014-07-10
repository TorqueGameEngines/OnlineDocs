Message
=======

Base class for messages.

Inherit:
	:doc:`SimObject`

Description
-----------

Message is the base class for C++ defined messages, and may also be used in script for script defined messages if no C++ subclass is appropriate.

Messages are reference counted and will be automatically deleted when their reference count reaches zero. When you dispatch a message, a reference will be added before the dispatch and freed after the dispatch. This allows for temporary messages with no additional code. If you want to keep the message around, for example to dispatch it to multiple queues, call addReference() before dispatching it and freeReference() when you are done with it. Never delete a Message object directly unless addReference() has not been called or the message has not been dispatched.

Message IDs are pooled similarly to datablocks, with the exception that IDs are reused. If you keep a message for longer than a single dispatch, then you should ensure that you clear any script variables that refer to it after the last freeReference(). If you don't, then it is probable that the object ID will become valid again in the future and could cause hard to track down bugs.

Messages have a unique type to simplify message handling code. For object messages, the type is defined as either the script defined class name or the C++ class name if no script class was defined. The message type may be obtained through the getType() method.

By convention, any data for the message is held in script accessible fields. Messages that need to be handled in C++ as well as script provide the relevant data through persistent fields in a subclass of Message to provide best performance on the C++ side. Script defined messages usually their through dynamic fields, and may be accessed in C++ using the SimObject::getDataField() method.


Methods
-------


.. cpp:function:: void Message::addReference()

	Increment the reference count for this message.

.. cpp:function:: void Message::freeReference()

	Decrement the reference count for this message.

.. cpp:function:: string Message::getType()

	Get message type (script class name or C++ class name if no script defined class).

.. cpp:function:: void Message::onAdd()

	Script callback when a message is first created and registered.

	Example::

		function Message::onAdd(%this)
		{
		   // Perform on add code here
		}

.. cpp:function:: void Message::onRemove()

	Script callback when a message is deleted.

	Example::

		function Message::onRemove(%this)
		{
		   // Perform on remove code here
		}
