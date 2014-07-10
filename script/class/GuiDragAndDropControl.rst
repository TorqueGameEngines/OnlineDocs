GuiDragAndDropControl
=====================

A container control that can be used to implement drag&drop behavior.

Inherit:
	:doc:`GuiControl`

Description
-----------

GuiDragAndDropControl is a special control that can be used to allow drag&drop behavior to be implemented where GuiControls may be dragged across the canvas and the dropped on other GuiControls.

To start a drag operation, construct a GuiDragAndDropControl and add the control that should be drag&dropped as a child to it. Note that this must be a single child control. To drag multiple controls, wrap them in a new GuiControl object as a temporary container.

Then, to initiate the drag, add the GuiDragAndDropControl to the canvas and call startDragging(). You can optionally supply an offset to better position the GuiDragAndDropControl on the mouse cursor.

As the GuiDragAndDropControl is then moved across the canvas, it will call the onControlDragEnter(), onControlDragExit(), onControlDragged(), and finally onControlDropped() callbacks on the visible topmost controls that it moves across. onControlDropped() is called when the mouse button is released and the drag operation thus finished.

Example::

	// The following example implements drag&drop behavior for GuiSwatchButtonCtrl so that// one color swatch may be dragged over the other to quickly copy its color.//// This code is taken from the stock scripts.//---------------------------------------------------------------------------------------------// With this method, we start the operation when the mouse is click-dragged away from a color swatch.
	function GuiSwatchButtonCtrl::onMouseDragged( %this )
	{
	   // First we construct a new temporary swatch button that becomes the payload for our// drag operation and give it the properties of the swatch button we want to copy.
	
	   %payload = newGuiSwatchButtonCtrl();
	   %payload.assignFieldsFrom( %this );
	   %payload.position = "0 0";
	   %payload.dragSourceControl = %this; // Remember where the drag originated from so that we dont copy a color swatch onto itself.// Calculate the offset of the GuiDragAndDropControl from the mouse cursor.  Here we center// it on the cursor.
	
	   %xOffset = getWord( %payload.extent, 0 ) / 2;
	   %yOffset = getWord( %payload.extent, 1 ) / 2;
	
	   // Compute the initial position of the GuiDragAndDrop control on the cavas based on the current// mouse cursor position.
	
	   %cursorpos = Canvas.getCursorPos();
	   %xPos = getWord( %cursorpos, 0 ) - %xOffset;
	   %yPos = getWord( %cursorpos, 1 ) - %yOffset;
	
	   // Create the drag control.
	
	   %ctrl = newGuiDragAndDropControl()
	   {
	      canSaveDynamicFields    = "0";
	      Profile                 = "GuiSolidDefaultProfile";
	      HorizSizing             = "right";
	      VertSizing              = "bottom";
	      Position                = %xPos SPC %yPos;
	      extent                  = %payload.extent;
	      MinExtent               = "4 4";
	      canSave                 = "1";
	      Visible                 = "1";
	      hovertime               = "1000";
	
	      // Let the GuiDragAndDropControl delete itself on mouse-up.  When the drag is aborted,// this not only deletes the drag control but also our payload.
	      deleteOnMouseUp         = true;
	
	      // To differentiate drags, use the namespace hierarchy to classify them.// This will allow a color swatch drag to tell itself apart from a file drag, for example.class                   = "GuiDragAndDropControlType_ColorSwatch";
	   };
	
	   // Add the temporary color swatch to the drag control as the payload.
	   %ctrl.add( %payload );
	
	   // Start drag by adding the drag control to the canvas and then calling startDragging().
	
	   Canvas.getContent().add( %ctrl );
	   %ctrl.startDragging( %xOffset, %yOffset );
	}
	
	//---------------------------------------------------------------------------------------------// This method receives the drop when the mouse button is released over a color swatch control// during a drag operation.
	function GuiSwatchButtonCtrl::onControlDropped( %this, %payload, %position )
	{
	   // Make sure this is a color swatch drag operation.if( !%payload.parentGroup.isInNamespaceHierarchy( "GuiDragAndDropControlType_ColorSwatch" ) )
	      return;
	
	   // If dropped on same button whence we came from,// do nothing.if( %payload.dragSourceControl == %this )
	      return;
	
	   // If a swatch button control is dropped onto this control,// copy its color.if( %payload.isMemberOfClass( "GuiSwatchButtonCtrl" ) )
	   {
	      // If the swatch button is part of a color-type inspector field,// remember the inspector field so we can later set the color// through it.if( %this.parentGroup.isMemberOfClass( "GuiInspectorTypeColorI" ) )
	         %this.parentGroup.apply( ColorFloatToInt( %payload.color ) );
	      elseif( %this.parentGroup.isMemberOfClass( "GuiInspectorTypeColorF" ) )
	         %this.parentGroup.apply( %payload.color );
	      else
	         %this.setColor( %payload.color );
	   }
	}

Methods
-------

.. cpp:function:: void GuiDragAndDropControl::startDragging(int x, int y)

	Start the drag operation.

	:param x: X coordinate for the mouse pointer offset which the drag control should position itself.
	:param y: Y coordinate for the mouse pointer offset which the drag control should position itself.

Fields
------

.. cpp:member:: bool  GuiDragAndDropControl::deleteOnMouseUp

	If true, the control deletes itself when the left mouse button is released. If at this point, the drag amp drop control still contains its payload, it will be deleted along with the control.
