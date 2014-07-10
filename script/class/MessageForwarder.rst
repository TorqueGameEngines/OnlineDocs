MessageForwarder
================

Forward messages from one queue to another.

Inherit:
	:doc:`ScriptMsgListener`

Description
-----------

MessageForwarder is a script class that can be used to forward messages from one queue to another.

Example::

	%fwd = newMessageForwarder()
	{
	   toQueue = "QueueToSendTo";
	};
	
	registerMessageListener("FromQueue", %fwd);

Where "QueueToSendTo" is the queue you want to forward to, and "FromQueue" is the queue you want to forward from.

Fields
------

.. cpp:member:: caseString  MessageForwarder::toQueue

	Name of queue to forward to.
