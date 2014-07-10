Datablock Editor
================

The configuration properties that describe dynamic objects in Torque 3D are stored in information structures called datablocks. The T3D Datablock Editor is used to quickly and easily change any parameter of any datablock from within the world Editor.

Interface
---------

To switch to the Datablock Editor press the :kbd:`F6` key or from the main menu select Editors > Datablock Editor. Or alternately click the Datablock icon from the World Editor toolbar.

.. image:: datablockeditor/DatablockEditor.jpg

The Datablock editor has two components: the Datablock Library pane and the Datablock properties pane. These panes appear at the right of the screen whenever the Datablock Editor is active. The Datablock Library pane is further divided into two tabs. The first, labelled Existing, contains a categorized list of all the existing datablocks. The second, labelled New, is used to create new instances of those datablocks.

.. image:: datablockeditor/Data_toollib1.jpg

Clicking any existing datablock will cause the Datablock properties pane to update to display the current properties of that datablock.

The image below shows the selection of the DefaultCar datablock, under the WheeledVehicleData category. This datablock contains variables related to vehicle performance.

.. image:: datablockeditor/Data_toolprop1.jpg

Creating a new Datablock
------------------------

Creating a new datablock can be done by creating a copy from an already existing datablock. To do so first select the New tab in the Datablock Library pane.

Then choose the type of datablock you wish to create from the list. Then press the New icon.

.. image:: datablockeditor/Data_new2.jpg

You will be presented with a new window giving you the option to name the new datablock and to copy values from one of the existing instances of the datablock type, if you want to. For example, in this scenario the DefaultCar datablock would be available in the dropdown box because it already exists at the time when creating a new datablock.

After clicking the Create button a new copy of the datablock will be added to the library, under the datablock type you first selected. In this example, you will create a new WheeledVehicleData datablock and name the new version "raceCar". This new version can now be found in the Library, under the Existing tab, in the WheeledVehicleData section.

Saving a Datablock
------------------

After editing the new datablock or any other datablock, you will need to save it. You will see a small "*" in the header of the properties right after the Datablock label if the datablock needs saving.

Click the small floppy disk icon to save your datablock changes.

.. image:: datablockeditor/Data_save1.jpg

.. note::

	 Any new datablock which has been saved will be added into the managedDatablocks.cs document which can be found at the location: project\game\art\datablocks\ for your scripters to access later.

Deleting a Datablock
--------------------

If you no longer need a datablock you can easily delete it by selecting the Delete icon.

.. image:: datablockeditor/Data_dal1.jpg

After pressing this icon you will get a notification window stating that the datablock has been removed. The World Builder will need to be restarted to completely remove the file.

Conclusion
----------

This article has covered the Datablock Editor and how it can be used to speed up your project development by adjusting object properties from within the Torque 3D World Editor. You can now make in-game adjustments on-the-fly without resorting to scripting.
