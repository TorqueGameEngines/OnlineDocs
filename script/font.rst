Font
====

Various helpers for working with fonts from script.

Functions
---------

.. cpp:function:: void dumpFontCacheStatus()

	Dumps to the console a full description of all cached fonts, along with info on the codepoints each contains.

.. cpp:function:: void duplicateCachedFont(string oldFontName, int oldFontSize, string newFontName)

	Copy the specified old font to a new name. The new copy will not have a platform font backing it, and so will never have characters added to it. But this is useful for making copies of fonts to add postprocessing effects to via exportCachedFont.

	:param oldFontName: The name of the font face to copy.
	:param oldFontSize: The size of the font to copy.
	:param newFontName: The name of the new font face.

.. cpp:function:: void exportCachedFont(string faceName, int fontSize, string fileName, int padding, int kerning)

	Export specified font to the specified filename as a PNG. The image can then be processed in Photoshop or another tool and reimported using importCachedFont. Characters in the font are exported as one long strip.

	:param faceName: The name of the font face.
	:param fontSize: The size of the font in pixels.
	:param fileName: The file name and path for the output PNG.
	:param padding: The padding between characters.
	:param kerning: The kerning between characters.

.. cpp:function:: void importCachedFont(string faceName, int fontSize, string fileName, int padding, int kerning)

	Import an image strip from exportCachedFont. Call with the same parameters you called exportCachedFont.

	:param faceName: The name of the font face.
	:param fontSize: The size of the font in pixels.
	:param fileName: The file name and path for the input PNG.
	:param padding: The padding between characters.
	:param kerning: The kerning between characters.

.. cpp:function:: void populateAllFontCacheRange(int rangeStart, int rangeEnd)

	Populate the font cache for all fonts with Unicode code points in the specified range.

	:param rangeStart: The start Unicode point.
	:param rangeEnd: The end Unicode point.

.. cpp:function:: void populateAllFontCacheString(string string)

	Populate the font cache for all fonts with characters from the specified string.

.. cpp:function:: void populateFontCacheRange(string faceName, int fontSize, int rangeStart, int rangeEnd)

	Populate the font cache for the specified font with Unicode code points in the specified range.

	:param faceName: The name of the font face.
	:param fontSize: The size of the font in pixels.
	:param rangeStart: The start Unicode point.
	:param rangeEnd: The end Unicode point.

.. cpp:function:: void populateFontCacheString(string faceName, int fontSize, string string)

	Populate the font cache for the specified font with characters from the specified string.

	:param faceName: The name of the font face.
	:param fontSize: The size of the font in pixels.
	:param string: The string to populate.

.. cpp:function:: void writeFontCache()

	Force all cached fonts to serialize themselves to the cache.
