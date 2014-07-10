SaveFileDialog
==============

Derived from FileDialog, this class is responsible for opening a file browser with the intention of saving a file.

Inherit:
	:doc:`FileDialog`

Description
-----------

The core usage of this dialog is to locate a file in the OS and return the path and name. This does not handle the actual file writing or data manipulation. That functionality is left up to the FileObject class.

Example::

	// Create a dialog dedicated to opening file
	 %saveFileDlg = newSaveFileDialog()
	 {
	    // Only allow for saving of COLLADA files
	    Filters        = "COLLADA Files (*.dae)|*.dae|";
	
	    // Default save path to where the WorldEditor last saved
	    DefaultPath    = $pref::WorldEditor::LastPath;
	
	    // No default file specified
	    DefaultFile    = "";
	
	    // Do not allow the user to change to a new directory
	    ChangePath     = false;
	
	    // Prompt the user if they are going to overwrite an existing file
	    OverwritePrompt   = true;
	 };
	
	 // Launch the save file dialog
	 %saveFileDlg.Execute();
	
	 if ( %result )
	 {
	    %seletedFile = %openFileDlg.file;
	 }
	 else
	 {
	    %selectedFile = "";
	 }
	
	 // Cleanup
	 %saveFileDlg.delete();


Fields
------

.. cpp:member:: bool  SaveFileDialog::OverwritePrompt

	True/False whether the dialog should prompt before accepting an existing file name.
