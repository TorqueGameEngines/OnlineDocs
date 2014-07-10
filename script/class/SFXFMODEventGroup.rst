SFXFMODEventGroup
=================

A group of events in an imported FMOD Designer project.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

A group of events in an imported FMOD Designer project.


Methods
-------


.. cpp:function:: void SFXFMODEventGroup::freeData()

	Release the resource data for this group and its subgroups.

.. cpp:function:: bool SFXFMODEventGroup::isDataLoaded()

	Test whether the resource data for this group has been loaded.

	:return: True if the resource data for this group is currently loaded. 

.. cpp:function:: bool SFXFMODEventGroup::loadData(bool loadStreams, bool loadSamples)

	Load the resource data for this group, if it has not already been loaded (either directly or indirectly through a parent group). This method works recursively and thus data for direct and indirect child groups to this group will be loaded as well.

	:param loadStreams: Whether to open streams.
	:param loadSamples: Whether to load sample banks.

	:return: True if the data has been successfully loaded; false otherwise.

Fields
------


.. cpp:member:: SFXFMODEventGroup SFXFMODEventGroup::fmodGroup

	DO NOT MODIFY!!

.. cpp:member:: string  SFXFMODEventGroup::fmodName

	DO NOT MODIFY!!

.. cpp:member:: SFXFMODProject SFXFMODEventGroup::fmodProject

	DO NOT MODIFY!!
