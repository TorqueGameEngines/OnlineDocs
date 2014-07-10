FileDialog
==========

Base class responsible for displaying an OS file browser.

Inherit:
	:doc:`SimObject`

Description
-----------

FileDialog is a platform agnostic dialog interface for querying the user for file locations. It is designed to be used through the exposed scripting interface.

FileDialog is the base class for Native File Dialog controls in Torque. It provides these basic areas of functionality:

FileDialog is *not* intended to be used directly in script and is only exposed to script to expose generic file dialog attributes.

This base class is usable in TorqueScript, but is does not specify what functionality is intended (open or save?). Its children, OpenFileDialog and SaveFileDialog, do make use of DialogStyle flags and do make use of specific funcationality. These are the preferred classes to use

However, the FileDialog base class does contain the key properties and important method for file browing. The most important function is Execute(). This is used by both SaveFileDialog and OpenFileDialog to initiate the browser.

Example::

	// NOTE: This is not he preferred class to use, but this still works
	// Create the file dialog
	%baseFileDialog = newFileDialog()
	{
	   // Allow browsing of all file typesfilters = "*.*";
	
	   // No default filedefaultFile = ;
	
	   // Set default path relative to projectdefaultPath = "./";
	
	   // Set the titletitle = "Durpa";
	
	   // Allow changing of path you are browsingchangePath = true;
	};
	
	 // Launch the file dialog
	 %baseFileDialog.Execute();
	 
	 // Dont forget to cleanup
	 %baseFileDialog.delete();


Methods
-------

.. cpp:function:: bool FileDialog::Execute()

	Launches the OS file browser. After an Execute() call, the chosen file name and path is available in one of two areas. If only a single file selection is permitted, the results will be stored in the fileName attribute. If multiple file selection is permitted, the results will be stored in the files array. The total number of files in the array will be stored in the fileCount attribute.

	:return: True if the file was selected was successfully found (opened) or declared (saved). 

	Example::

		// NOTE: This is not he preferred class to use, but this still works
		// Create the file dialog
		%baseFileDialog = newFileDialog()
		{
		   // Allow browsing of all file typesfilters = "*.*";
		
		   // No default filedefaultFile = ;
		
		   // Set default path relative to projectdefaultPath = "./";
		
		   // Set the titletitle = "Durpa";
		
		   // Allow changing of path you are browsingchangePath = true;
		};
		
		 // Launch the file dialog
		 %baseFileDialog.Execute();
		 
		 // Dont forget to cleanup
		 %baseFileDialog.delete();
		
		
		 // A better alternative is to use the 
		 // derived classes which are specific to file open and save
		 // Create a dialog dedicated to opening files
		 %openFileDlg = newOpenFileDialog()
		 {
		    // Look for jpg image files
		    // First part is the descriptor|second part is the extension
		    Filters = "Jepg Files|*.jpg";
		    // Allow browsing through other folders
		    ChangePath = true;
		
		    // Only allow opening of one file at a time
		    MultipleFiles = false;
		 };
		
		 // Launch the open file dialog
		 %result = %openFileDlg.Execute();
		
		 // Obtain the chosen file name and pathif ( %result )
		 {
		    %seletedFile = %openFileDlg.file;
		 }
		 else
		 {
		    %selectedFile = "";
		 }
		 // Cleanup
		 %openFileDlg.delete();
		
		
		 // Create a dialog dedicated to saving a file
		 %saveFileDlg = newSaveFileDialog()
		 {
		    // Only allow for saving of COLLADA files
		    Filters = "COLLADA Files (*.dae)|*.dae|";
		
		    // Default save path to where the WorldEditor last saved
		    DefaultPath = $pref::WorldEditor::LastPath;
		
		    // No default file specified
		    DefaultFile = "";
		
		    // Do not allow the user to change to a new directory
		    ChangePath = false;
		
		    // Prompt the user if they are going to overwrite an existing file
		    OverwritePrompt = true;
		 };
		
		 // Launch the save file dialog
		 %result = %saveFileDlg.Execute();
		
		 // Obtain the file name
		 %selectedFile = "";
		 if ( %result )
		    %selectedFile = %saveFileDlg.file;
		
		 // Cleanup
		 %saveFileDlg.delete();

Fields
------

.. cpp:member:: bool  FileDialog::changePath

	True/False whether to set the working directory to the directory returned by the dialog.

.. cpp:member:: string  FileDialog::defaultFile

	The default file path when the dialog is shown.

.. cpp:member:: string  FileDialog::defaultPath

	The default directory path when the dialog is shown.

.. cpp:member:: string  FileDialog::fileName

	The default file name when the dialog is shown.

.. cpp:member:: string  FileDialog::filters

	The filter string for limiting the types of files visible in the dialog. It makes use of the pipe symbol '|' as a delimiter. For example: 'All Files|*.*' 'Image Files|*.png;*.jpg|Png Files|*.png|Jepg Files|*.jpg'

.. cpp:member:: string  FileDialog::title

	The title for the dialog.
