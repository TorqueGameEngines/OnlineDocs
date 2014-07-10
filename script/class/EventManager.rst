EventManager
============

The EventManager class is a wrapper for the standard messaging system.

Inherit:
	:doc:`SimObject`

Description
-----------

It provides functionality for management of event queues, events, and subscriptions. Creating an EventManager is as simple as calling new EventManager and specifying a queue name.

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


.. cpp:function:: void EventManager::dumpEvents()

	Print all registered events to the console.

.. cpp:function:: void EventManager::dumpSubscribers(String event)

	Print all subscribers to an event to the console.

	:param event: The event whose subscribers are to be printed. If this parameter isn't specified, all events will be dumped.

.. cpp:function:: bool EventManager::isRegisteredEvent(String event)

	Check if an event is registered or not.

	:param event: The event to check.

	:return: Whether or not the event exists. 

.. cpp:function:: bool EventManager::postEvent(String event, String data)

	~Trigger an event.

	:param event: The event to trigger.
	:param data: The data associated with the event.

	:return: Whether or not the event was dispatched successfully. 

.. cpp:function:: bool EventManager::registerEvent(String event)

	Register an event with the event manager.

	:param event: The event to register.

	:return: Whether or not the event was registered successfully. 

.. cpp:function:: void EventManager::remove(SimObject listener, String event)

	Remove a listener from an event.

	:param listener: The listener to remove.
	:param event: The event to be removed from.

.. cpp:function:: void EventManager::removeAll(SimObject listener)

	Remove a listener from all events.

	:param listener: The listener to remove.

.. cpp:function:: bool EventManager::subscribe(SimObject listener, String event, String callback)

	Subscribe a listener to an event.

	:param listener: The listener to subscribe.
	:param event: The event to subscribe to.
	:param callback: Optional method name to receive the event notification. If this is not specified, "on[event]" will be used.

	:return: Whether or not the subscription was successful. 

.. cpp:function:: void EventManager::unregisterEvent(String event)

	Remove an event from the EventManager .

	:param event: The event to remove.

Fields
------


.. cpp:member:: string  EventManager::queue

	List of events currently waiting.
