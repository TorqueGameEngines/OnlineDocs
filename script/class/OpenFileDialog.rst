OpenFileDialog
==============

Derived from FileDialog, this class is responsible for opening a file browser with the intention of opening a file.

Inherit:
	:doc:`FileDialog`

Description
-----------

The core usage of this dialog is to locate a file in the OS and return the path and name. This does not handle the actual file parsing or data manipulation. That functionality is left up to the FileObject class.

Example::

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


Fields
------

.. cpp:member:: bool  OpenFileDialog::MultipleFiles

	True/False whether multiple files may be selected and returned or not.

.. cpp:member:: bool  OpenFileDialog::MustExist

	True/False whether the file returned must exist or not.
