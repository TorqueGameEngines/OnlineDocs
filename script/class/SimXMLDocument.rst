SimXMLDocument
==============

File I/O object used for creating, reading, and writing XML documents.

Inherit:
	:doc:`SimObject`

Description
-----------

A SimXMLDocument is a container of various XML nodes. The Document level may contain a header (sometimes called a declaration), comments and child Elements. Elements may contain attributes, data (or text) and child Elements.

You build new Elements using addNewElement(). This makes the new Element the current one you're working with. You then use setAttribute() to add attributes to the Element. You use addData() or addText() to write to the text area of an Element.

Example::

	// Thanks to Rex Hiebert for this example
	// Given the following XML
	// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
	// <DataTables>
	//   <table tableName="2DShapes">
	//      <rec id="1">Triangle</rec>
	//      <rec id="2">Square</rec><rec id="3">Circle</rec>
	//    </table>
	//   <table tableName="3DShapes">
	//      <rec id="1">Pyramid</rec>
	//      <rec id="2">Cube</rec>
	//      <rec id="3">Sphere</rec>
	//   </table>
	// </DataTables>

	// Using SimXMLDocument by itself
	function readXmlExample(%filename)
	{
	   %xml = newSimXMLDocument() {};
	   %xml.loadFile(%filename);
	
	   %xml.pushChildElement("DataTables");
	   %xml.pushFirstChildElement("table");
	   while(true)
	   {
	     echo("TABLE:" SPC %xml.attribute("tableName"));
	     %xml.pushFirstChildElement("rec");
	     while (true)
	     {
	       %id = %xml.attribute("id");
	       %desc = %xml.getData();
	       echo("  Shape" SPC %id SPC %desc);
	       if (!%xml.nextSiblingElement("rec")) break;
	     }
	     %xml.popElement();
	     if (!%xml.nextSiblingElement("table")) break;
	   }
	}
	
	// Thanks to Scott Peal for this example
	// Using FileObject in conjunction with SimXMLDocument
	// This example uses an XML file with a format of:
	// <Models>
	//    <Model category="" name="" path="" />
	// </Models>
	function getModelsInCatagory()
	{
	   %file = "./Catalog.xml";
	   %fo = newFileObject();
	   %text = "";
	
	   if(%fo.openForRead(%file))
	   {
	     while(!%fo.isEOF())
	     {
	       %text = %text @ %fo.readLine();
	       if (!%fo.isEOF()) %text = %text @ "\n";
	     }
	   }
	   else
	   {
	     echo("Unable to locate the file: " @ %file);
	   }
	
	   %fo.delete();
	
	   %xml = newSimXMLDocument() {};
	   %xml.parse(%text);
	   // "Get" inside of the root element, "Models".
	   %xml.pushChildElement(0);
	
	   // "Get" into the first child element
	   if (%xml.pushFirstChildElement("Model"))
	   {
	     while (true)
	     {
	       // Here, i read the elements attributes.
	       // You might want to save these values in an array or call the %xml.getElementValue()
	       // if you have a different XML structure.
	
	       %catagory = %xml.attribute("catagory");
	       %name = %xml.attribute("name");
	       %path = %xml.attribute("path");
	
	       // now, read the next "Model"
	       if (!%xml.nextSiblingElement("Model")) break;
	     }
	   }
	}


Methods
-------

.. cpp:function:: void SimXMLDocument::addComment(string comment)

	Add the given comment as a child of the document.

	:param comment: String containing the comment.

	Example::

		// Create a new XML document with a header, a comment and single element.
		%x = newSimXMLDocument();
		%x.addHeader();
		%x.addComment("This is a test comment");
		%x.addNewElement("NewElement");
		%x.saveFile("test.xml");
		
		// Produces the following file:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <!--This is a test comment-->
		// <NewElement />

.. cpp:function:: void SimXMLDocument::addData(string text)

	Add the given text as a child of current Element. Use getData() to retrieve any text from the current Element. addData() and addText() may be used interchangeably. As there is no difference between data and text, you may also use removeText() to clear any data from the current Element.

	:param text: String containing the text.

	Example::

		// Create a new XML document with a header and single element// with some added data.
		%x = newSimXMLDocument();
		%x.addHeader();
		%x.addNewElement("NewElement");
		%x.addData("Some text");
		%x.saveFile("test.xml");
		
		// Produces the following file:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <NewElement>Some text</NewElement>

.. cpp:function:: void SimXMLDocument::addHeader()

	Add a XML header to a document. Sometimes called a declaration, you typically add a standard header to the document before adding any elements. SimXMLDocument always produces the following header: lt ?xml version="1.0" encoding="utf-8" standalone="yes" ? gt

	Example::

		// Create a new XML document with just a header and single element.
		%x = newSimXMLDocument();
		%x.addHeader();
		%x.addNewElement("NewElement");
		%x.saveFile("test.xml");
		
		// Produces the following file:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <NewElement />

.. cpp:function:: void SimXMLDocument::addNewElement(string name)

	Create a new element with the given name as child of current Element's parent and push it onto the Element stack making it the current one.

	:param name: XML tag for the new Element.

.. cpp:function:: void SimXMLDocument::addText(string text)

	Add the given text as a child of current Element. Use getText() to retrieve any text from the current Element and removeText() to clear any text. addText() and addData() may be used interchangeably.

	:param text: String containing the text.

	Example::

		// Create a new XML document with a header and single element// with some added text.
		%x = newSimXMLDocument();
		%x.addHeader();
		%x.addNewElement("NewElement");
		%x.addText("Some text");
		%x.saveFile("test.xml");
		
		// Produces the following file:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <NewElement>Some text</NewElement>

.. cpp:function:: string SimXMLDocument::attribute(string attributeName)

	Get a string attribute from the current Element on the stack.

	:param attributeName: Name of attribute to retrieve.

	:return: The attribute string if found. Otherwise returns an empty string. 

.. cpp:function:: bool SimXMLDocument::attributeExists(string attributeName)

	Tests if the requested attribute exists.

	:param attributeName: Name of attribute being queried for.

	:return: True if the attribute exists. 

.. cpp:function:: float SimXMLDocument::attributeF32(string attributeName)

	Get float attribute from the current Element on the stack.

	:param attributeName: Name of attribute to retrieve.

	:return: The value of the given attribute in the form of a float. 

.. cpp:function:: int SimXMLDocument::attributeS32(string attributeName)

	Get int attribute from the current Element on the stack.

	:param attributeName: Name of attribute to retrieve.

	:return: The value of the given attribute in the form of an integer. 

.. cpp:function:: void SimXMLDocument::clear()

	Set this document to its default state. Clears all Elements from the documents. Equivalent to using reset()

.. cpp:function:: void SimXMLDocument::clearError()

	Clear the last error description.

.. cpp:function:: string SimXMLDocument::elementValue()

	Get the Element's value if it exists. Usually returns the text from the Element.

	:return: The value from the Element, or an empty string if none is found. 

.. cpp:function:: string SimXMLDocument::firstAttribute()

	Obtain the name of the current Element's first attribute.

	:return: String containing the first attribute's name, or an empty string if none is found.

.. cpp:function:: string SimXMLDocument::getData()

	Gets the text from the current Element. Use addData() to add text to the current Element. getData() and getText() may be used interchangeably. As there is no difference between data and text, you may also use removeText() to clear any data from the current Element.

	:return: String containing the text in the current Element.

	Example::

		// Using the following test.xml file as an example:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <NewElement>Some data</NewElement>
		// Load in the file
		%x = newSimXMLDocument();
		%x.loadFile("test.xml");
		
		// Make the first Element the current one
		%x.pushFirstChildElement("NewElement");
		
		// Store the current Elements data (Some data in this example)
		// into result
		%result = %x.getData();
		echo( %result );

.. cpp:function:: string SimXMLDocument::getErrorDesc()

	Get last error description.

	:return: A string of the last error message. 

.. cpp:function:: string SimXMLDocument::getText()

	Gets the text from the current Element. Use addText() to add text to the current Element and removeText() to clear any text. getText() and getData() may be used interchangeably.

	:return: String containing the text in the current Element.

	Example::

		// Using the following test.xml file as an example:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <NewElement>Some text</NewElement>
		// Load in the file
		%x = newSimXMLDocument();
		%x.loadFile("test.xml");
		
		// Make the first Element the current one
		%x.pushFirstChildElement("NewElement");
		
		// Store the current Elements text (Some text in this example)
		// into result
		%result = %x.getText();
		echo( %result );

.. cpp:function:: string SimXMLDocument::lastAttribute()

	Obtain the name of the current Element's last attribute.

	:return: String containing the last attribute's name, or an empty string if none is found.

.. cpp:function:: bool SimXMLDocument::loadFile(string fileName)

	Load in given filename and prepare it for use.

	:param fileName: Name and path of XML document

	:return: True if the file was loaded successfully. 

.. cpp:function:: string SimXMLDocument::nextAttribute()

	Get the name of the next attribute for the current Element after a call to firstAttribute() .

	:return: String containing the next attribute's name, or an empty string if none is found.

.. cpp:function:: bool SimXMLDocument::nextSiblingElement(string name)

	Put the next sibling Element with the given name on the stack, making it the current one.

	:param name: String containing name of the next sibling.

	:return: True if the Element was found and made the current one. 

.. cpp:function:: void SimXMLDocument::parse(string xmlString)

	Create a document from a XML string.

	:param xmlString: Valid XML to parse and store as a document.

.. cpp:function:: void SimXMLDocument::popElement()

	Pop the last Element off the stack.

.. cpp:function:: string SimXMLDocument::prevAttribute()

	Get the name of the previous attribute for the current Element after a call to lastAttribute() .

	:return: String containing the previous attribute's name, or an empty string if none is found.

.. cpp:function:: bool SimXMLDocument::pushChildElement(int index)

	Push the child Element at the given index onto the stack, making it the current one.

	:param index: Numerical index of Element being pushed.

	:return: True if the Element was found and made the current one. 

.. cpp:function:: bool SimXMLDocument::pushFirstChildElement(string name)

	Push the first child Element with the given name onto the stack, making it the current Element.

	:param name: String containing name of the child Element.

	:return: True if the Element was found and made the current one. 

	Example::

		// Using the following test.xml file as an example:
		// <?xml version="1.0" encoding="utf-8" standalone="yes" ?>
		// <NewElement>Some text</NewElement>
		// Load in the file
		%x = newSimXMLDocument();
		%x.loadFile("test.xml");
		
		// Make the first Element the current one
		%x.pushFirstChildElement("NewElement");
		
		// Store the current Elements text (Some text in this example)
		// into result
		%result = %x.getText();
		echo( %result );

.. cpp:function:: void SimXMLDocument::pushNewElement(string name)

	Create a new element with the given name as child of current Element and push it onto the Element stack making it the current one.

	:param name: XML tag for the new Element.

.. cpp:function:: string SimXMLDocument::readComment(int index)

	Gives the comment at the specified index, if any. Unlike addComment() that only works at the document level, readComment() may read comments from the document or any child Element. The current Element (or document if no Elements have been pushed to the stack) is the parent for any comments, and the provided index is the number of comments in to read back.

	:param index: Comment index number to query from the current Element stack

	:return: String containing the comment, or an empty string if no comment is found.

.. cpp:function:: void SimXMLDocument::removeText()

	Remove any text on the current Element. Use getText() to retrieve any text from the current Element and addText() to add text to the current Element. As getData() and addData() are equivalent to getText() and addText() , removeText() will also remove any data from the current Element.

.. cpp:function:: void SimXMLDocument::reset()

	Set this document to its default state. Clears all Elements from the documents. Equivalent to using clear()

.. cpp:function:: bool SimXMLDocument::saveFile(string fileName)

	Save document to the given file name.

	:param fileName: Path and name of XML file to save to.

	:return: True if the file was successfully saved. 

.. cpp:function:: void SimXMLDocument::setAttribute(string attributeName, string value)

	Set the attribute of the current Element on the stack to the given value.

	:param attributeName: Name of attribute being changed
	:param value: New value to assign to the attribute

.. cpp:function:: void SimXMLDocument::setObjectAttributes(string objectID)

	Add the given SimObject's fields as attributes of the current Element on the stack.

	:param objectID: ID of SimObject being copied.
