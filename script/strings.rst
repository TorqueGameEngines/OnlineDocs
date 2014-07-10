Strings
=======

Functions for dealing with string values. Since in TorqueScript any value is implicitly also a string, these functions can be used with all values.

Functions
---------

.. cpp:function:: string collapseEscape(string text)

	Replace all escape sequences in text with their respective character codes. This function replaces all escape sequences (\n, \t, etc) in the given string with the respective characters they represent. The primary use of this function is for converting strings from their literal form into their compiled/translated form, as is normally done by the TorqueScript compiler.

	:param text: A string.

	:return:  with all escape sequences replaced by their respective character codes.

	Example::

		// Print:
		//    str
		//    ing
		// to the console.  Note how the backslash in the string must be escaped here
		// in order to prevent the TorqueScript compiler from collapsing the escape
		// sequence in the resulting string.
		echo( collapseEscape( "str\ning" ) );

.. cpp:function:: void dumpStringMemStats()

	Dumps information about String memory usage.

.. cpp:function:: bool endsWith(string str, string suffix, bool caseSensitive)

	Test whether the given string ends with the given suffix.

	:param str: The string to test.
	:param suffix: The potential suffix of str.
	:param caseSensitive: If true, the comparison will be case-sensitive; if false, differences in casing will not be taken into account.

	:return: True if the last characters in str match the complete contents of suffix; false otherwise.

	Example::

		startsWith( "TEST123", "123" ) // Returns true.

.. cpp:function:: string expandEscape(string text)

	Replace all characters in text that need to be escaped for the string to be a valid string literal with their respective escape sequences. All characters in text that cannot appear in a string literal will be replaced by an escape sequence (\n, \t, etc). The primary use of this function is for converting strings suitable for being passed as string literals to the TorqueScript compiler. expandEscape( "str" NL "ing" ) // Returns "str\ning".

	:param text: A string

	:return: A duplicate of the text parameter with all unescaped characters that cannot appear in string literals replaced by their respective escape sequences.

.. cpp:function:: string getSubStr(string str, int start, int numChars)

	Return a substring of str starting at start and continuing either through to the end of str (if numChars is -1) or for numChars characters (except if this would exceed the actual source string length).

	:param str: The string from which to extract a substring.
	:param start: The offset at which to start copying out characters.
	:param numChars: Optional argument to specify the number of characters to copy. If this is -1, all characters up the end of the input string are copied.

	:return: A string that contains the given portion of the input string.

	Example::

		getSubStr( "foobar", 1, 2 ) // Returns "oo".

.. cpp:function:: int getTrailingNumber(string str)

	Get the numeric suffix of the given input string.

	:param str: The string from which to read out the numeric suffix.

	:return: The numeric value of the number suffix of str or -1 if str has no such suffix.

	Example::

		getTrailingNumber( "test123" ) // Returns 123.

.. cpp:function:: bool isalnum(string str, int index)

	Test whether the character at the given position is an alpha-numeric character. Alpha-numeric characters are characters that are either alphabetic (a-z, A-Z) or numbers (0-9).

	:param str: The string to test.
	:param index: The index of a character in str.

	:return:  True if the character at the given index in str is an alpha-numeric character; false otherwise.

.. cpp:function:: bool isspace(string str, int index)

	Test whether the character at the given position is a whitespace character. Characters such as tab, space, or newline are considered whitespace.

	:param str: The string to test.
	:param index: The index of a character in str.

	:return:  True if the character at the given index in str is a whitespace character; false otherwise.

.. cpp:function:: string ltrim(string str)

	Remove leading whitespace from the string.

	:param str: A string.

	:return:  A string that is the same as str but with any leading (i.e. leftmost) whitespace removed.

	Example::

		ltrim( "   string  " ); // Returns "string  ".

.. cpp:function:: string nextToken(string str, string token, string delimiters)

	Tokenize a string using a set of delimiting characters. This function first skips all leading charaters in str that are contained in delimiters . From that position, it then scans for the next character in str that is contained in delimiters and stores all characters from the starting position up to the first delimiter in a variable in the current scope called token . Finally, it skips all characters in delimiters after the token and then returns the remaining string contents in str . To scan out all tokens in a string, call this function repeatedly by passing the result it returns each time as the new str until the function returns "".

	:param str: A string.
	:param token: The name of the variable in which to store the current token. This variable is set in the scope in which nextToken is called.
	:param delimiters: A string of characters. Each character is considered a delimiter.

	:return: The remainder of str after the token has been parsed out or "" if no more tokens were found in str.

	Example::

		// Prints:
		// a
		// b
		// c
		%str = "a   b c";
		while ( %str !$= "" )
		{
		   // First time, stores "a" in the variable %token and sets %str to "b c".
		   %str = nextToken( %str, "token", "" );
		   echo( %token );
		}

.. cpp:function:: string rtrim(string str)

	Remove trailing whitespace from the string.

	:param str: A string.

	:return:  A string that is the same as str but with any trailing (i.e. rightmost) whitespace removed.

	Example::

		rtrim( "   string  " ); // Returns "   string".

.. cpp:function:: bool startsWith(string str, string prefix, bool caseSensitive)

	Test whether the given string begins with the given prefix.

	:param str: The string to test.
	:param prefix: The potential prefix of str.
	:param caseSensitive: If true, the comparison will be case-sensitive; if false, differences in casing will not be taken into account.

	:return: True if the first characters in str match the complete contents of prefix; false otherwise.

	Example::

		startsWith( "TEST123", "test" ) // Returns true.

.. cpp:function:: int strasc(string chr)

	Return the integer character code value corresponding to the first character in the given string.

	:param chr: a (one-character) string.

	:return: The UTF32 code value for the first character in the given string. 

.. cpp:function:: string strchr(string str, string chr)

	Find the first occurrence of the given character in str .

	:param str: The string to search.
	:param chr: The character to search for. Only the first character from the string is taken.

	:return: The remainder of the input string starting with the given character or the empty string if the character could not be found.

.. cpp:function:: int strchrpos(string str, string chr, int start)

	Find the first occurrence of the given character in the given string.

	:param str: The string to search.
	:param chr: The character to look for. Only the first character of this string will be searched for.
	:param start: The index into str at which to start searching for the given character.

	:return:  The index of the first occurrence of chr in str or -1 if str does not contain the given character.

	Example::

		strchrpos( "test", "s" ) // Returns 2.

.. cpp:function:: int strcmp(string str1, string str2)

	Compares two strings using case- sensitive comparison.

	:param str1: The first string.
	:param str2: The second string.

	:return: 0 if both strings are equal, a value <0 if the first character different in str1 has a smaller character code value than the character at the same position in str2, and a value >1 otherwise.

	Example::

		if( strcmp( %var, "foobar" ) == 0 )
		   echo( "%var is equal to foobar" );

.. cpp:function:: string strformat(string format, string value)

	Format the given value as a string using printf-style formatting.

	:param format: A printf-style format string.
	:param value: The value argument matching the given format string.

	Example::

		// Convert the given integer value to a string in a hex notation.
		%hex = strformat( "%x", %value );

.. cpp:function:: int stricmp(string str1, string str2)

	Compares two strings using case- insensitive comparison.

	:param str1: The first string.
	:param str2: The second string.

	:return: 0 if both strings are equal, a value <0 if the first character different in str1 has a smaller character code value than the character at the same position in str2, and a value >0 otherwise.

	Example::

		if( stricmp( "FOObar", "foobar" ) == 0 )
		   echo( "this is always true" );

.. cpp:function:: int strinatcmp(string str1, string str2)

	Compares two strings using "natural order" case-insensitive comparison. Natural order means that rather than solely comparing single character code values, strings are ordered in a natural way. For example, the string "hello10" is considered greater than the string "hello2" even though the first numeric character in "hello10" actually has a smaller character value than the corresponding character in "hello2". However, since 10 is greater than 2, strnatcmp will put "hello10" after "hello2".

	:param str1: The first string.
	:param str2: The second string.

	:return:  0 if the strings are equal, a value >0 if str1 comes after str2 in a natural order, and a value <0 if str1 comes before str2 in a natural order.

	Example::

		// Bubble sort 10 elements of %array using natural orderdo
		{
		   %swapped = false;
		   for( %i = 0; %i < 10 - 1; %i ++ )
		      if( strnatcmp( %array[ %i ], %array[ %i + 1 ] ) > 0 )
		      {
		         %temp = %array[ %i ];
		         %array[ %i ] = %array[ %i + 1 ];
		         %array[ %i + 1 ] = %temp;
		         %swapped = true;
		      }
		}
		while( %swapped );

.. cpp:function:: string stripChars(string str, string chars)

	Remove all occurrences of characters contained in chars from str .

	:param str: The string to filter characters out from.
	:param chars: A string of characters to filter out from str.

	:return: A version of str with all occurrences of characters contained in chars filtered out.

	Example::

		stripChars( "teststring", "se" ); // Returns "tttring".

.. cpp:function:: String stripTrailingNumber(string str)

	Strip a numeric suffix from the given string.

	:param str: The string from which to strip its numeric suffix.

	:return:  The string str without its number suffix or the original string str if it has no such suffix.

	Example::

		stripTrailingNumber( "test123" ) // Returns "test".

.. cpp:function:: bool strIsMatchExpr(string pattern, string str, bool caseSensitive)

	Match a pattern against a string.

	:param pattern: The wildcard pattern to match against. The pattern can include characters, '*' to match any number of characters and '?' to match a single character.
	:param str: The string which should be matched against pattern.
	:param caseSensitive: If true, characters in the pattern are matched in case-sensitive fashion against this string. If false, differences in casing are ignored.

	:return: True if str matches the given pattern.

	Example::

		strIsMatchExpr( "f?o*R", "foobar" ) // Returns true.

.. cpp:function:: bool strIsMatchMultipleExpr(string patterns, string str, bool caseSensitive)

	Match a multiple patterns against a single string.

	:param patterns: A tab-separated list of patterns. Each pattern can include charaters, '*' to match any number of characters and '?' to match a single character. Each of the patterns is tried in turn.
	:param str: The string which should be matched against patterns.
	:param caseSensitive: If true, characters in the pattern are matched in case-sensitive fashion against this string. If false, differences in casing are ignored.

	:return: True if str matches any of the given patterns.

	Example::

		strIsMatchMultipleExpr( "*.cs *.gui *.mis", "mymission.mis" ) // Returns true.

.. cpp:function:: int strlen(string str)

	Get the length of the given string in bytes.

	:param str: A string.

	:return: The length of the given string in bytes. 

.. cpp:function:: string strlwr(string str)

	Return an all lower-case version of the given string.

	:param str: A string.

	:return:  A version of str with all characters converted to lower-case.

	Example::

		strlwr( "TesT1" ) // Returns "test1"

.. cpp:function:: int strnatcmp(string str1, string str2)

	Compares two strings using "natural order" case-sensitive comparison. Natural order means that rather than solely comparing single character code values, strings are ordered in a natural way. For example, the string "hello10" is considered greater than the string "hello2" even though the first numeric character in "hello10" actually has a smaller character value than the corresponding character in "hello2". However, since 10 is greater than 2, strnatcmp will put "hello10" after "hello2".

	:param str1: The first string.
	:param str2: The second string.

	:return:  0 if the strings are equal, a value >0 if str1 comes after str2 in a natural order, and a value <0 if str1 comes before str2 in a natural order.

	Example::

		// Bubble sort 10 elements of %array using natural orderdo
		{
		   %swapped = false;
		   for( %i = 0; %i < 10 - 1; %i ++ )
		      if( strnatcmp( %array[ %i ], %array[ %i + 1 ] ) > 0 )
		      {
		         %temp = %array[ %i ];
		         %array[ %i ] = %array[ %i + 1 ];
		         %array[ %i + 1 ] = %temp;
		         %swapped = true;
		      }
		}
		while( %swapped );

.. cpp:function:: int strpos(string haystack, string needle, int offset)

	Find the start of needle in haystack searching from left to right beginning at the given offset.

	:param haystack: The string to search.
	:param needle: The string to search for.

	:return:  The index at which the first occurrence of needle was found in haystack or -1 if no match was found.

	Example::

		strpos( "b ab", "b", 1 ) // Returns 3.

.. cpp:function:: string strrchr(string str, string chr)

	Find the last occurrence of the given character in str .

	:param str: The string to search.
	:param chr: The character to search for. Only the first character from the string is taken.

	:return: The remainder of the input string starting with the given character or the empty string if the character could not be found.

.. cpp:function:: int strrchrpos(string str, string chr, int start)

	Find the last occurrence of the given character in the given string.

	:param str: The string to search.
	:param chr: The character to look for. Only the first character of this string will be searched for.
	:param start: The index into str at which to start searching for the given character.

	:return: The index of the last occurrence of chr in str or -1 if str does not contain the given character.

	Example::

		strrchrpos( "test", "t" ) // Returns 3.

.. cpp:function:: string strrepeat(string str, int numTimes, string delimiter)

	Return a string that repeats str numTimes number of times delimiting each occurrence with delimiter .

	:param str: The string to repeat multiple times.
	:param numTimes: The number of times to repeat str in the result string.
	:param delimiter: The string to put between each repetition of str.

	:return:  A string containing str repeated numTimes times.

	Example::

		strrepeat( "a", 5, "b" ) // Returns "ababababa".

.. cpp:function:: string strreplace(string source, string from, string to)

	Replace all occurrences of from in source with to .

	:param source: The string in which to replace the occurrences of from.
	:param from: The string to replace in source.
	:param to: The string with which to replace occurrences of .

	:return: A string with all occurrences of from in source replaced by to.

	Example::

		strreplace( "aabbccbb", "bb", "ee" ) // Returns "aaeeccee".

.. cpp:function:: int strstr(string string, string substring)

	Find the start of substring in the given string searching from left to right.

	:param string: The string to search.
	:param substring: The string to search for.

	:return: The index into string at which the first occurrence of substring was found or -1 if substring could not be found.

	Example::

		strstr( "abcd", "c" ) // Returns 2.

.. cpp:function:: string strupr(string str)

	Return an all upper-case version of the given string.

	:param str: A string.

	:return:  A version of str with all characters converted to upper-case.

	Example::

		strupr( "TesT1" ) // Returns "TEST1"

.. cpp:function:: string trim(string str)

	Remove leading and trailing whitespace from the string.

	:param str: A string.

	:return:  A string that is the same as str but with any leading (i.e. leftmost) and trailing (i.e. rightmost) whitespace removed.

	Example::

		trim( "   string  " ); // Returns "string".

Field Manipulators
------------------

Functions to deal with whitespace-separated lists of values in strings. TorqueScript extensively uses strings to represent lists of values. The functions in this group simplify working with these lists and allow to easily extract individual values from their strings.

The list strings are segregated into three groups according to the delimiters used to separate invididual values in the strings:

* Strings of words: Elements are separated by newlines (\n), spaces, or tabs (\t).
* Strings of fields: Elements are sepaerated by newlines (\n) or tabs (\t).
* Strings of records: Elements are separated by newlines (\n).

Aside from the functions here, another useful means to work with strings of words is TorqueScript's foreach$ statement.

Functions
~~~~~~~~~

.. cpp:function:: string firstWord(string text)

	Return the first word in text .

	:param text: A list of words separated by newlines, spaces, and/or tabs.

	:return:  The word at index 0 in text or "" if text is empty.

.. cpp:function:: string getField(string text, int index)

	Extract the field at the given index in the newline and/or tab separated list in text . Fields in text must be separated by newlines and/or tabs.

	:param text: A list of fields separated by newlines and/or tabs.
	:param index: The zero-based index of the field to extract.

	:return: The field at the given index or "" if the index is out of range.

	Example::

		getField( "a b" TAB "c d" TAB "e f", 1 ) // Returns "c d"

.. cpp:function:: int getFieldCount(string text)

	Return the number of newline and/or tab separated fields in text .

	:param text: A list of fields separated by newlines and/or tabs.

	:return: .

	Example::

		getFieldCount( "a b" TAB "c d" TAB "e f" ) // Returns 3

.. cpp:function:: string getFields(string text, int startIndex, int endIndex)

	Extract a range of fields from the given startIndex onwards thru endIndex . Fields in text must be separated by newlines and/or tabs.

	:param text: A list of fields separated by newlines and/or tabs.
	:param startIndex: The zero-based index of the first field to extract from text.
	:param endIndex: The zero-based index of the last field to extract from text. If this is -1, all fields beginning with startIndex are extracted from text.

	:return: The number of newline and/or tab sepearated elements in text.

	Example::

		getFields( "a b" TAB "c d" TAB "e f", 1 ) // Returns "c d" TAB "e f"

.. cpp:function:: string getRecord(string text, int index)

	Extract the record at the given index in the newline-separated list in text . Records in text must be separated by newlines.

	:param text: A list of records separated by newlines.
	:param index: The zero-based index of the record to extract.

	:return:  The record at the given index or "" if index is out of range.

	Example::

		getRecord( "a b" NL "c d" NL "e f", 1 ) // Returns "c d"

.. cpp:function:: int getRecordCount(string text)

	Return the number of newline-separated records in text .

	:param text: A list of records separated by newlines.

	:return: The number of newline-sepearated elements in text.

	Example::

		getRecordCount( "a b" NL "c d" NL "e f" ) // Returns 3

.. cpp:function:: string getRecords(string text, int startIndex, int endIndex)

	Extract a range of records from the given startIndex onwards thru endIndex . Records in text must be separated by newlines.

	:param text: A list of records separated by newlines.
	:param startIndex: The zero-based index of the first record to extract from text.
	:param endIndex: The zero-based index of the last record to extract from text. If this is -1, all records beginning with startIndex are extracted from text.

	:return: A string containing the specified range of records from text or "" if startIndex is out of range or greater than endIndex.

	Example::

		getRecords( "a b" NL "c d" NL "e f", 1 ) // Returns "c d" NL "e f"

.. cpp:function:: string getWord(string text, int index)

	Extract the word at the given index in the whitespace-separated list in text . Words in text must be separated by newlines, spaces, and/or tabs.

	:param text: A whitespace-separated list of words.
	:param index: The zero-based index of the word to extract.

	:return: The word at the given index or "" if the index is out of range.

	Example::

		getWord( "a b c", 1 ) // Returns "b"

.. cpp:function:: int getWordCount(string text)

	Return the number of whitespace-separated words in text . Words in text must be separated by newlines, spaces, and/or tabs.

	:param text: A whitespace-separated list of words.

	:return: .

	Example::

		getWordCount( "a b c d e" ) // Returns 5

.. cpp:function:: string getWords(string text, int startIndex, int endIndex)

	Extract a range of words from the given startIndex onwards thru endIndex . Words in text must be separated by newlines, spaces, and/or tabs.

	:param text: A whitespace-separated list of words.
	:param startIndex: The zero-based index of the first word to extract from text.
	:param endIndex: The zero-based index of the last word to extract from text. If this is -1, all words beginning with startIndex are extracted from text.

	:return: A string containing the specified range of words from text or "" if startIndex is out of range or greater than endIndex.

	Example::

		getWords( "a b c d", 1, 2, ) // Returns "b c"

.. cpp:function:: string removeField(string text, int index)

	Remove the field in text at the given index . Fields in text must be separated by newlines and/or tabs.

	:param text: A list of fields separated by newlines and/or tabs.
	:param index: The zero-based index of the field in text.

	:return:  A new string with the field at the given index removed or the original string if index is out of range.

	Example::

		removeField( "a b" TAB "c d" TAB "e f", 1 ) // Returns "a b" TAB "e f"

.. cpp:function:: string removeRecord(string text, int index)

	Remove the record in text at the given index . Records in text must be separated by newlines.

	:param text: A list of records separated by newlines.
	:param index: The zero-based index of the record in text.

	:return:  is out of range.

	Example::

		removeRecord( "a b" NL "c d" NL "e f", 1 ) // Returns "a b" NL "e f"

.. cpp:function:: string removeWord(string text, int index)

	Remove the word in text at the given index . Words in text must be separated by newlines, spaces, and/or tabs.

	:param text: A whitespace-separated list of words.
	:param index: The zero-based index of the word in text.

	:return:  A new string with the record at the given index removed or the original string if index is out of range.

	Example::

		removeWord( "a b c d", 2 ) // Returns "a b d"

.. cpp:function:: string restWords(string text)

	Return all but the first word in text .

	:param text: A list of words separated by newlines, spaces, and/or tabs.

	:return:  Text with the first word removed.

.. cpp:function:: string setField(string text, int index, string replacement)

	Replace the field in text at the given index with replacement . Fields in text must be separated by newlines and/or tabs.

	:param text: A list of fields separated by newlines and/or tabs.
	:param index: The zero-based index of the field to replace.
	:param replacement: The string with which to replace the field.

	:return:  is out of range.

	Example::

		setField( "a b" TAB "c d" TAB "e f", 1, "g h" ) // Returns "a b" TAB "g h" TAB "e f"

.. cpp:function:: string setRecord(string text, int index, string replacement)

	Replace the record in text at the given index with replacement . Records in text must be separated by newlines.

	:param text: A list of records separated by newlines.
	:param index: The zero-based index of the record to replace.
	:param replacement: The string with which to replace the record.

	:return:  A new string with the field at the given index replaced by replacement or the original string if index is out of range.

	Example::

		setRecord( "a b" NL "c d" NL "e f", 1, "g h" ) // Returns "a b" NL "g h" NL "e f"

.. cpp:function:: string setWord(string text, int index, string replacement)

	Replace the word in text at the given index with replacement . Words in text must be separated by newlines, spaces, and/or tabs.

	:param text: A whitespace-separated list of words.
	:param index: The zero-based index of the word to replace.
	:param replacement: The string with which to replace the word.

	:return:  A new string with the record at the given index replaced by replacement or the original string if index is out of range.

	Example::

		setWord( "a b c d", 2, "f" ) // Returns "a b f d"
