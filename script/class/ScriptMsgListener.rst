ScriptMsgListener
=================

Script accessible version of Dispatcher::IMessageListener. Often used in conjunction with EventManager.

Inherit:
	:doc:`SimObject`

Description
-----------

The main use of ScriptMsgListener is to allow script to listen formessages. You can subclass ScriptMsgListener in script to receivethe Dispatcher::IMessageListener callbacks.

Alternatively, you can derive from it in C++ instead of SimObject toget an object that implements Dispatcher::IMessageListener with scriptcallbacks. If you need to derive from something other then SimObject,then you will need to implement the Dispatcher::IMessageListenerinterface yourself.

Example::

	// Create the EventManager.
	$MyEventManager = newEventManager() { queue = "MyEventManager"; };
	
	// Create an event.
	$MyEventManager.registerEvent( "SomeCoolEvent" );
	
	// Create a listener and subscribe.
	$MyListener = newScriptMsgListener() { class = MyListener; };
	$MyEventManager.subscribe( $MyListener, "SomeCoolEvent" );
	
	function MyListener::onSomeCoolEvent( %this, %data )
	{
	   echo( "onSomeCoolEvent Triggered" );
	}
	
	// Trigger the event.
	$MyEventManager.postEvent( "SomeCoolEvent", "Data" );


Methods
-------


.. cpp:function:: void ScriptMsgListener::onAdd()

	Script callback when a listener is first created and registered.

	Example::

		function ScriptMsgListener::onAdd(%this)
		{
		   // Perform on add code here
		}

.. cpp:function:: void ScriptMsgListener::onAddToQueue(string queue)

	Callback for when the listener is added to a queue. The default implementation of onAddToQueue() and onRemoveFromQueue() provide tracking of the queues this listener is added to through the mQueues member. Overrides of onAddToQueue() or onRemoveFromQueue() should ensure they call the parent implementation in any overrides.

	:param queue: The name of the queue that the listener added to

.. cpp:function:: bool ScriptMsgListener::onMessageObjectReceived(string queue, Message msg)

	Called when a message object (not just the message data) is passed to a listener.

	:param queue: The name of the queue the message was dispatched to
	:param msg: The message object

	:return: false to prevent other listeners receiving this message, true otherwise 

.. cpp:function:: bool ScriptMsgListener::onMessageReceived(string queue, string event, string data)

	Called when the listener has received a message.

	:param queue: The name of the queue the message was dispatched to
	:param event: The name of the event (function) that was triggered
	:param data: The data (parameters) for the message

	:return: false to prevent other listeners receiving this message, true otherwise 

.. cpp:function:: void ScriptMsgListener::onRemove()

	Script callback when a listener is deleted.

	Example::

		function ScriptMsgListener::onRemove(%this)
		{
		   // Perform on remove code here
		}

.. cpp:function:: void ScriptMsgListener::onRemoveFromQueue(string queue)

	Callback for when the listener is removed from a queue. The default implementation of onAddToQueue() and onRemoveFromQueue() provide tracking of the queues this listener is added to through the mQueues member. Overrides of onAddToQueue() or onRemoveFromQueue() should ensure they call the parent implementation in any overrides.

	:param queue: The name of the queue that the listener was removed from
