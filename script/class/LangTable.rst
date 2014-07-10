LangTable
=========

Provides the code necessary to handle the low level management of the string tables for localization.

Inherit:
	:doc:`SimObject`

Description
-----------

One LangTable is created for each mod, as well as one for the C++ code. LangTable is responsible for obtaining the correct strings from each and relaying it to the appropriate controls.

Methods
-------

.. cpp:function:: int LangTable::addLanguage(string filename)

	Adds a language to the table.

	:param filename: Name and path to the language file
	:param languageName: Optional name to assign to the new language entry

	:return: True If file was successfully found and language created 

.. cpp:function:: int LangTable::getCurrentLanguage()

	Get the ID of the current language table.

	:return: Numerical ID of the current language table 

.. cpp:function:: string LangTable::getLangName(int language)

	Return the readable name of the language table.

	:param language: Numerical ID of the language table to access

	:return: String containing the name of the table, NULL if ID was invalid or name was never specified 

.. cpp:function:: int LangTable::getNumLang()

	Used to find out how many languages are in the table.

	:return: Size of the vector containing the languages, numerical 

.. cpp:function:: string LangTable::getString(string filename)

	Grabs a string from the specified table. If an invalid is passed, the function will attempt to to grab from the default table

	:param filename: Name of the language table to access

	:return: Text from the specified language table, "" if ID was invalid and default table is not set 

.. cpp:function:: void LangTable::setCurrentLanguage(int language)

	Sets the current language table for grabbing text.

	:param language: ID of the table

.. cpp:function:: void LangTable::setDefaultLanguage(int language)

	Sets the default language table.

	:param language: ID of the table
