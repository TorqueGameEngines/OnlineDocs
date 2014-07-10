SFXState
========

A boolean switch used to modify playlist behavior.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

Sound system states are used to allow playlist controllers to make decisions based on global state. This is useful, for example, to couple audio playback to gameplay state. Certain states may, for example, represent different locations that the listener can be in, like underwater, in open space, or indoors. Other states could represent moods of the current gameplay situation, like, for example, an aggressive mood during combat.

By activating and deactivating sound states according to gameplay state, a set of concurrently running playlists may react and adapt to changes in the game.

Activation and Deactivation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

At any time, a given state can be either active or inactive. Calling activate() on a state increases an internal counter and calling deactivate() decreases the counter. Only when the count reaches zero will the state be deactivated.

In addition to the activation count, states also maintain a disabling count. Calling disable() increases this count and calling enable() decreases it. As long as this count is greater than zero, a given state will not be activated even if its activation count is non-zero. Calling disable() on an active state will not only increase the disabling count but also deactivate the state. Calling enable() on a state with a positive activation count will re-activate the state when the disabling count reaches zero.

State Dependencies
~~~~~~~~~~~~~~~~~~

By listing other states in in its includedStates and excludedStates fields, a state may automatically trigger the activation or disabling of other states in the sytem when it is activated. This allows to form dependency chains between individual states.

Example::

	// State indicating that the listener is submerged.
	singleton SFXState( AudioLocationUnderwater )
	{
	   parentGroup = AudioLocation;
	   // AudioStateExclusive is a class defined in the core scripts that will automatically// ensure for a state to deactivate all the sibling SFXStates in its parentGroup when it// is activated.className = "AudioStateExclusive";
	};
	
	// State suitable e.g. for combat.
	singleton SFXState( AudioMoodAggressive )
	{
	   parentGroup = AudioMood;
	   className = "AudioStateExclusive";
	};

Methods
-------

.. cpp:function:: void SFXState::activate()

	Increase the activation count on the state. If the state isn't already active and it is not disabled, the state will be activated.

.. cpp:function:: void SFXState::deactivate()

	Decrease the activation count on the state. If the count reaches zero and the state was not disabled, the state will be deactivated.

.. cpp:function:: void SFXState::disable()

	Increase the disabling count of the state. If the state is currently active, it will be deactivated.

.. cpp:function:: void SFXState::enable()

	Decrease the disabling count of the state. If the disabling count reaches zero while the activation count is still non-zero, the state will be reactivated again.

.. cpp:function:: bool SFXState::isActive()

	Test whether the state is currently active. This is true when the activation count is gt 0 and the disabling count is =0.

	:return: True if the state is currently active. 

.. cpp:function:: bool SFXState::isDisabled()

	Test whether the state is currently disabled. This is true when the disabling count of the state is non-zero.

	:return: True if the state is disabled.

.. cpp:function:: void SFXState::onActivate()

	Called when the state goes from inactive to active.

.. cpp:function:: void SFXState::onDeactivate()

	called when the state goes from active to deactive.

Fields
------

.. cpp:member:: SFXState SFXState::excludedStates [4]

	States that will automatically be disabled when this state is activated. Activation and Deactivation

.. cpp:member:: SFXState SFXState::includedStates [4]

	States that will automatically be activated when this state is activated. Activation and Deactivation
