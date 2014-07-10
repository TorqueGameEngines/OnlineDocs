GuiControlProfile
=================

Inherit:
	:doc:`SimObject`

Description
-----------

A collection of properties that determine control behavior and rendering.


Methods
-------


.. cpp:function:: int GuiControlProfile::getStringWidth()


Fields
------


.. cpp:member:: bool  GuiControlProfile::autoSizeHeight

	Automatically adjust height of control to fit contents.

.. cpp:member:: bool  GuiControlProfile::autoSizeWidth

	Automatically adjust width of control to fit contents.

.. cpp:member:: ColorI  GuiControlProfile::bevelColorHL


.. cpp:member:: ColorI  GuiControlProfile::bevelColorLL


.. cpp:member:: filename  GuiControlProfile::bitmap

	Texture to use for rendering control.

.. cpp:member:: int  GuiControlProfile::border

	Border type (0=no border).

.. cpp:member:: ColorI  GuiControlProfile::borderColor

	Color to draw border with.

.. cpp:member:: ColorI  GuiControlProfile::borderColorHL


.. cpp:member:: ColorI  GuiControlProfile::borderColorNA


.. cpp:member:: int  GuiControlProfile::borderThickness

	Thickness of border in pixels.

.. cpp:member:: bool  GuiControlProfile::canKeyFocus

	Whether the control can have the keyboard focus.

.. cpp:member:: string  GuiControlProfile::category

	Category under which the profile will appear in the editor.

.. cpp:member:: ColorI  GuiControlProfile::cursorColor

	Color to use for the text cursor.

.. cpp:member:: ColorI  GuiControlProfile::fillColor


.. cpp:member:: ColorI  GuiControlProfile::fillColorHL


.. cpp:member:: ColorI  GuiControlProfile::fillColorNA


.. cpp:member:: ColorI  GuiControlProfile::fillColorSEL


.. cpp:member:: GuiFontCharset GuiControlProfile::fontCharset


.. cpp:member:: ColorI  GuiControlProfile::fontColor

	Font color for normal text (same as fontColors[0]).

.. cpp:member:: ColorI  GuiControlProfile::fontColorHL

	Font color for highlighted text (same as fontColors[1]).

.. cpp:member:: ColorI  GuiControlProfile::fontColorLink

	Font color for links in text (same as fontColors[4]).

.. cpp:member:: ColorI  GuiControlProfile::fontColorLinkHL

	Font color for highlighted links in text (same as fontColors[5]).

.. cpp:member:: ColorI  GuiControlProfile::fontColorNA

	Font color when control is not active/disabled (same as fontColors[2]).

.. cpp:member:: ColorI  GuiControlProfile::fontColors [10]

	Font colors to use for different text types/states.

.. cpp:member:: ColorI  GuiControlProfile::fontColorSEL

	Font color for selected text (same as fontColors[3]).

.. cpp:member:: int  GuiControlProfile::fontSize

	Font size in points.

.. cpp:member:: string  GuiControlProfile::fontType

	Name of font family and typeface (e.g. "Arial Bold").

.. cpp:member:: bool  GuiControlProfile::hasBitmapArray

	If true, 'bitmap' is an array of images.

.. cpp:member:: GuiAlignmentType GuiControlProfile::justify

	Horizontal alignment for text.

.. cpp:member:: bool  GuiControlProfile::modal


.. cpp:member:: bool  GuiControlProfile::mouseOverSelected


.. cpp:member:: bool  GuiControlProfile::numbersOnly

	Whether control should only accept numerical data ( GuiTextEditCtrl ).

.. cpp:member:: bool  GuiControlProfile::opaque


.. cpp:member:: string  GuiControlProfile::profileForChildren


.. cpp:member:: bool  GuiControlProfile::returnTab

	Whether to add automatic tab event when return is pressed so focus moves on to next control ( GuiTextEditCtrl ).

.. cpp:member:: SFXTrack GuiControlProfile::soundButtonDown

	Sound to play when mouse has been pressed on control.

.. cpp:member:: SFXTrack GuiControlProfile::soundButtonOver

	Sound to play when mouse is hovering over control.

.. cpp:member:: bool  GuiControlProfile::tab


.. cpp:member:: Point2I  GuiControlProfile::textOffset

