Localization
============

Localization of games to multiple languages.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/LangTable

Description
-----------

Localizing large applications can be an extremely time consuming and aggravating process. This manual is intended to guide you through the changes made to Torque to support localization and help you reduce the ongoing headaches in day-to-day development in a localized codebase. This manual assumes you are at least familiar with Torque Script. C++ and localization experience is not necessary.

Languages and String Tables
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lets say you want to print some text to the console. From script, you’d usually just write something like:

echo("Hello, World!");
This is all well and good, if all you care about is English. What do you do if the user wants your game to talk French? You could do something like the following::

	switch($Pref::Language)
	{
	   case $ENGLISH:
	      echo("Hello, World!");
	   case $FRENCH:
	      echo("Salut, Monde!");
	... other languages here ...
	}

Sure, this works. It's also a complete pain in the backside to keep up to date, let alone that you'd have to repeat the switch for every string you use. In the C++ code alone there is upwards of 4000 strings that are candidates for localization, so this method is clearly not even close to an option.

String tables are the answer to this problem. A string table is an array of strings that you can reference based on an ID instead of specifying the string directly in the source code. Changing which language the string is displayed in is simply a matter of using a string table that contains the strings in the language you wish to display. The above example can be reduced down to the following::

	echo(L($STR_HELLO_WORLD));

The code is not much different to how you wrote it before, but the string will now be displayed in the correct language based on the user's selection. This does come with a price, however. You now have to create and maintain string tables for all the languages you support, which can be a big headache. Torque tries to make this as simple as possible, and some tips for creating and maintaining these string tables are given later.

Script Interface
~~~~~~~~~~~~~~~~

Torque contains a lot of strings, not just in the C++ code but in the script code too. For example, all your GUIs are created in script and must also be localized. To further complicate matters the scripts are contained in mod directories, each of which is a separate entity.

Strings in Script
~~~~~~~~~~~~~~~~~

It would be cumbersome and difficult to maintain one string table for all the strings, so Torque doesn't try. Each mod has it's own string table, as well as the core C++ code. You would be forgiven for thinking that this leads to having to write code as follows::

	echo(L($StarterFPSTable, $STR_HELLO_WORLD));

I don't know about you, but I'm a lazy programmer and that's just too much typing for me to put up with every time I want to display a string. Instead, you just use::

	echo(L($STR_HELLO_WORLD));

Torque takes care of the rest: the correct table will be used based on which mod the code is executed from.

Loading strings and specifying languages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The new LangTable class, accessible in script as well as in C++, provides the code necessary to handle the low level management of the string tables and obtaining the correct strings from them. One LangTable is created for each mod, as well as one for the C++ code.

An important portion of the localization system is implemented in script. This support code is responsible for managing the language tables and provides you with a simpler API than would be the case using LangTable directly. To provide this API, a new mod called "lang" has been added. The lang mod works a little like the common mod in that it just provides code needed by all mods. As the localization code is needed very early in the initialisation code, adding it to the common mod was not possible.

To ease loading of language tables, language maps are provided. These map the displayed name of the language to a string table on disk and are used to provide automatic loading across all mods. You specify the language map in the lang/languages.cs script, for example::

	addLanguageMap("English", "english.lso");
	addLanguageMap("Pony", "pony.lso");

The first argument to addLanguageMap() is the name of the language as it will be displayed to the user, and the second is the filename of the language. The filename will be concatenated onto the mod path to find the actual filename name of the table to load.

To load the language tables for the current mod, in the onStart() function for the mod, before any other code, use the following::

	table = loadModLangTables("starter.fps/lang/tables");
	setModLangTable(table);
	loadModLangTables() loads the tables from the specified directory based on the information in the language map. setModLangTable() tells the C++ code to use the specified table for the current mod. This is usually done in the mod's onStart() function. After loading the tables, the current language will be set to English.

	 // setup localization:
	   $I18N::starter.fps = new LangTable();
	   exec("starter.fps/lang/tables/German.cs");
	   exec("starter.fps/lang/tables/English.cs");
	   $I18N::starter.fps.addLanguage("starter.fps/lang/tables/German.lso", "German");
	   $I18N::starter.fps.addLanguage("starter.fps/lang/tables/English.lso", "English");
	   $I18N::starter.fps.setDefaultLanguage(0); // German is default here
	   $I18N::starter.fps.setCurrentLanguage(0); // German is current
	$I18N::starter.fps.setCurrentLanguage(1); // this would set the current language to english

Handling user language preferences
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the Torque demo, the user is provided two ways to change their language settings. If they have not already chosen a language, for example the first time they run the game, a dialog will pop up after the splash screens asking them to choose a language. The language can also be changed at any time from the options dialog. Note that some strings will not be in the new language until the game is restarted. There will be further discussion on this topic in later chapters.

When the language is changed, the onChangeLanguage() function is called. This should be overriden for each mod in the same way as onStart(). The following code can be used for all mods::

	function onChangeLanguage()
	{
	   setCurrentLanguage(getModLangTable(), $pref::I18N::language);
	   Parent::onChangeLanguage();
	}

To change the language for all mods, you can simply use the setLanguage() function. setLanguage() takes one argument, the display name of the language to switch to.

Localizing the GUI
~~~~~~~~~~~~~~~~~~

The GUI provides some interesting challenges for localization. Since GUI files are just script files that create the objects for the GUI, text is specified as a member field of the object. For example::

	new GuiButtonCtrl() {
	      text = "Quit!";
	... other fields ...
	};

As this is just a script, you can localize it easily by using the L() function in the same way you would with other scripts, for example::

	new GuiButtonCtrl() {
	      text = L($STR_QUIT);
	... other fields ...
	};

Unfortunately, this is not a viable solution. If you save that GUI from the GUI editor, the call to L() will be replaced with the text it returned when creating the GUI, reverting it to the first example. The only way around that is to edit all your GUIs by hand, which is not a particularly pleasant option when you have an editor to do it for you.

In order to sensibly support editing of GUIs, most of the GUI controls that support the text field now also support a textID field. This is the name of the ID variable for the string, for example::

	new GuiButtonCtrl() {
	      textID = "STR_QUIT";
	... other fields ...
	};

In addition, a setTextID() method was added to all controls that expose a setText() method to allow you to set the text at run time. It functions the same as the setText() method, except it works with IDs::

	obj.setTextID("STR_ABOUT");

The only caveat is you must specify the name of the variable as a string, and not the variable itself. If you used the variable, for example obj.setText($STR_ABOUT), then the textID field would get set to the numeric ID, and the GUI control would be looking for a variable called, for example, 45.

If you don't specify an ID, or the ID you do specify is invalid for whatever reason, then the control will simply use the text field as before.

Specifying the language table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Unfortunately, there is not enough context available in the GUI system to determine which mod the control was defined in, so the tricks used to make the L() function work cannot be used in the GUI.

To work around the problem, a field was added to GuiControl to specify the table to use, called langTableMod, which is simply the name of the mod to get the language table from. Usually, this will be the same as the mod that the .gui file resides in.

To avoid having to specify the table for every control that needs it, a crude form of inheritance was implemented. If langTableMod is not specified for a control, the control's parent will be checked. This means you only have to specify the table in the root control for the GUI. However, you could also specify a different table on a per-control basis if needed, for example if you wanted to use a string from the language table for common. The following example GUI illustrates this better::

	// The value that you set langTableMod to is the same as name after "$I18N::". 
	// If you use "$I18N::bob" then langTableMod = "bob".
	new GuiChunkedBitmapCtrl(MainMenuGui) 
	{
	   profile = "GuiContentProfile";
	   horizSizing = "width";
	   vertSizing = "height";
	   position = "0 0";
	   extent = "640 480";
	   minExtent = "8 8";
	   visible = "1";
	   langTableMod = "starter.fps";
	   bitmap = "./background";
	   useVariable = "0";
	   tile = "0";
	   helpTag = "0";
	   new GuiButtonCtrl() {
	      profile = "GuiButtonProfile";
	      horizSizing = "right";
	      vertSizing = "top";
	      position = "36 413";
	      extent = "110 20";
	      minExtent = "8 8";
	      visible = "1";
	      command = "quit();";
	      textID = "STR_QUIT";
	      groupNum = "-1";
	      buttonType = "PushButton";
	         helpTag = "0";
	   };
	};

Refreshing the GUI
~~~~~~~~~~~~~~~~~~

When the user has chosen a new language, it would be nice to be able to get the GUI to refresh without forcing them to restart the game. One nice side effect of the updates to the GUI system is that we can do that.

The way the textID field was implemented is it checks for a valid ID, then if it has one it passes the string directly to setText(). The initial update of the text field is done on onWake(), so to get the control to update you only have to cause it to get an onWake() event.

It turns out that you can trick Torque into resending onWake() events quite simply, without having to write a ton of code. For the main canvas, you can simply do::

	if(isObject(Canvas))
	Canvas.setContent(Canvas.getContent());

When implementing the options dialog, I found that this wont refresh the dialogs. To work around that, when you click apply the script will pop the dialog then re-push it, as follows::

	Canvas.popDialog(optionsDlg);
	Canvas.pushDialog(optionsDlg);

Of course, some things will not be possible to update when you change the language. It may be worth considering requiring users to restart the game for language changes to take effect for the sake of consistency.

C++ Interface
~~~~~~~~~~~~~

The C++ interface is largely in flux at the moment pending fixing the string extractor to cope with multi-line strings. In terms of how you reference strings, it will be largely the same as the script interface.

Caveats
~~~~~~~

This will have caveats for the localization thingy.

The Localization Tools
~~~~~~~~~~~~~~~~~~~~~~

The current toolset consists of the command line language compiler, called langc, which is used to compile a language file into the various formats needed by the engine.

Language Files
~~~~~~~~~~~~~~

Language files are simple text files containing the identifiers and strings. An example follows::

	TEST_STR_1=This is a test
	TEST_STR_2=and so is this!

The string definitions are similar to variable definitions in C++ and Torque Script, except you do not need quotes or a semicolon. The "variable" becomes the ID as it will be referred to in the game code.

If you need the string to span multiple lines, you can use the usual as you would in C++. Note that currently you can't use a trailing \ on the line to continue to the next line. (Note: this should be fixed)

You can use any amount of white space on either side of the equals sign. Two options control how the compiler handles whitespace. By default, any whitespace after the equals (leading spaces) will be stripped and any space on the end of the string (trailing spaces) will be left alone. Two options control this behaviour:

S
  Strip leading space. When this option is specified, any space after the = sign will become part of the string.

T
  Strip trailing space. When specified, space on the end of the string will be stripped.

Comments may be inserted in the language file at the beginning of a line only. You can use #, ; or // to delimit comments. For example::

	# This is a comment
	; So is this
	And this

Compiling Language Files
~~~~~~~~~~~~~~~~~~~~~~~~

Before a language file can be used in the engine, it has to be compiled into a .lso file. As the process is slightly different depending on whether you are compiling the default english language file or a translation, it is not possible to do this automatically, as is done with scripts.

The default language is usually English. There is no hard and fast restriction on which language is the default, but for the purposes of documentation it will be assumed that English is your default language. It is worth pointing out that because strings that are missing from a particular language will use the default language, and some strings (particularly in the C++ code) are not localized, not using English for the default language may cause inconsistencies.

Language files are compiled with the langc tool, found in the tools directory. Like other Torque tools, langc must be compiled before you can use it.

langc can also produce some other related files, for example header files for the IDs and templates for translations.

In its simplest usage, langc requires the name of the language file to compile and an output basename, for example::

	> langc english.lang english

The first argument is the name of the language file and the second is the basename for output files. langc can create a number of different files, so rather then force you to specify the filename of each one explicitly, you only have to specify the first part of the filename. The relevant extension will be added automatically.

If you were to run the above example, english.lang would be compiled, but no output files will be generated. This can be useful for checking if there are any errors in the file, but most of the time you'll want to produce some output files.

To compile the language to an lso, you use the -l option, as follows::

	> langc -l english.lang english

This will compile english.lang and, assuming there were no errors, will produce english.lso, ready to load into the engine.

Identifiers
~~~~~~~~~-~

Earlier in this manual, global variables were used as identifiers for the strings, but there was no mention of where they came from. Because these are a pain in the backside to maintain, langc does the job for you. When you compile the english language file, you can also generate a script file containing global variables for each string ID in the language file.

To generate the script, simply use the -s option. For example::

	> langc -s english.lang english

This will generate a file called english.cs. Using the earlier example .lang file, the generated script would look something like this::

	// Automatically generated. DO NOT EDIT
	This is a test
	$TEST_STR_1 = 0;
	and so is this!
	$TEST_STR_2 = 1;

If you'd like to save some time, you can specify multiple options at once, as in the following example::

	> langc -ls english.lang english

This will create both english.lso and english.cs.

Compiling Translations
~~~~~~~~~~~~~~~~~~~~~~

Although translations compile to the same lso files as the default language, the process is slightly more involved. This is because the identifiers must come from the default english file to ensure they are correct.

You can create a template for a new translation, based on the english file, as follows::

	> langc -r english.lang french

This will generate a file called french.tran, the format of which is identical to the .lang files described earlier::

	# Automatically generated.
	# [TEST_STR_1:0] This is a test
	TEST_STR_1=
	# [TEST_STR_2:1] and so is this!
	TEST_STR_2=

The comments preceding each string definition are intended to tell the translator what the original english string was. The actual string definitions are left blank so that langc will issue a warning for empty, and thus untranslated, strings.

Compiling a translation requires a few more options then compiling the english file::

	> langc -tl -e english.lang french.tran french

Here, -t tells langc you want to compile a translation, -e english.lang specifies the filename of the english translation and, as before, -l causes the .lso file to be compiled.

When the translation is loaded into the engine, any strings that are left empty will automatically fall back to the english version of them. By default, langc will issue a warning when compiling the file if a string is empty. This is useful while compiling translations to determine which strings have not been translated. However, it's less useful when compiling the english file, so these warnings may be turned off with the -W option. It is not recommended to use -W when compiling translations.

Other langc options
~~~~~~~~~~~~~~~~~~~

Aside from the above, langc provides a few additional options that you may find useful. These were purposefully not mentioned before as they are not particularly useful at this time.

A complete list of current langc options may be obtained by running langc with no arguments, as follows::

	> langc
	Usage: langc [options] <filename> <outbasename>
	Where options is one or more of:
	 -l    Write Language File              -h    Write C++ Header
	 -s    Write Script                     -d    Write C++ Defaults
	 -t    Compile a translation            -r    Write translation file
	 -e <filename>   Specify english file when compiling translations
	 -S    Don't strip leading spaces       -T    Strip trailing spaces
	 -I    Don't warn for invalid chars     -W    Don't warn for empty identifiers
	 -q    Quiet mode, no warnings at all

Of particular note are the options -h and -d, used when building files for the C++ localization. The -h option generates a C++ header file in the same way as the -s option does for scripts. The -d option writes a C++ source file that provides a big array of default strings. This is intended to be used as an extra fallback when a string can't be found in the language table (or when there is no language table), which allows the same executable to be used whether localization is active or not.

Identifiers must be valid variable names, as they are used directly both as script variables and C++ defines. By default, langc will warn you if an invalid character is used in an identifier. The -I option prevents this.

The -q option is simply a shortcut to disable all warnings at once. If any errors occur, they will still be displayed.

Functions
---------

.. cpp:function:: int getCoreLangTable()

	Gets the primary LangTable used by the game.

	:returns: ID of the core LangTable

.. cpp:function:: void setCoreLangTable(string LangTable)

	Sets the primary LangTable used by the game.

	:param LangTable: ID of the core LangTable
