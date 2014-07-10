GuiDirectoryFileListCtrl
========================

A control that displays a list of files from within a single directory in the game file system.

Inherit:
	:doc:`GuiListBoxCtrl`

Description
-----------

A control that displays a list of files from within a single directory in the game file system.

Example::

	newGuiDirectoryFileListCtrl()
	{
	   filePath = "art/shapes";
	   fileFilter = "*.dts" TAB "*.dae";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: string GuiDirectoryFileListCtrl::getSelectedFile()

	Get the currently selected filename.

	:return: The filename of the currently selected file 

.. cpp:function:: string GuiDirectoryFileListCtrl::getSelectedFiles()

	Get the list of selected files.

	:return: A space separated list of selected files 

.. cpp:function:: void GuiDirectoryFileListCtrl::reload()

	Update the file list.

.. cpp:function:: void GuiDirectoryFileListCtrl::setFilter(string filter)

	Set the file filter.

	:param filter: Tab-delimited list of file name patterns. Only matched files will be displayed.

.. cpp:function:: bool GuiDirectoryFileListCtrl::setPath(string path, string filter)

	Set the search path and file filter.

	:param path: Path in game directory from which to list files.
	:param filter: Tab-delimited list of file name patterns. Only matched files will be displayed.

Fields
------


.. cpp:member:: string  GuiDirectoryFileListCtrl::fileFilter

	Tab-delimited list of file name patterns. Only matched files will be displayed.

.. cpp:member:: string  GuiDirectoryFileListCtrl::filePath

	Path in game directory from which to list files.
