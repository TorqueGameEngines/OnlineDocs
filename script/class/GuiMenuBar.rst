GuiMenuBar
==========

GUI Control which displays a horizontal bar with individual drop-down menu items. Each menu item may also have submenu items.

Inherit:
	:doc:`GuiTickCtrl`

Description
-----------

GUI Control which displays a horizontal bar with individual drop-down menu items. Each menu item may also have submenu items.

Example::

	newGuiMenuBar(newMenuBar)
	{
	   Padding = "0";
	   //Properties not specific to this control have been omitted from this example.
	};
	
	// Add a menu to the menu bar
	newMenuBar.addMenu(0,"New Menu");
	
	// Add a menu item to the New Menu
	newMenuBar.addMenuItem(0,"New Menu Item",0,"n",-1);
	
	// Add a submenu item to the New Menu Item
	newMenuBar.addSubmenuItem(0,1,"New Submenu Item",0,"s",-1);


Methods
-------


.. cpp:function:: void GuiMenuBar::addMenu(string menuText, int menuId)

	Adds a new menu to the menu bar.

	:param menuText: Text to display for the new menu item.
	:param menuId: ID for the new menu item.

	Example::

		// Define the menu text
		%menuText = "New Menu";
		
		// Define the menu ID.
		%menuId = "2";
		
		// Inform the GuiMenuBar control to add the new menu
		%thisGuiMenuBar.addMenu(%menuText,%menuId);

.. cpp:function:: void GuiMenuBar::addMenuItem(string targetMenu, string menuItemText, int menuItemId, string accelerator, int checkGroup)

	Adds a menu item to the specified menu. The menu argument can be either the text of a menu or its id.

	:param menu: Menu name or menu Id to add the new item to.
	:param menuItemText: Text for the new menu item.
	:param menuItemId: Id for the new menu item.
	:param accelerator: Accelerator key for the new menu item.
	:param checkGroup: Check group to include this menu item in.

	Example::

		// Define the menu we wish to add the item to
		%targetMenu = "New Menu";  or  %menu = "4";
		
		// Define the text for the new menu item
		%menuItemText = "Menu Item";
		
		// Define the id for the new menu item
		%menuItemId = "3";
		
		// Set the accelerator key to toggle this menu item with
		%accelerator = "n";
		
		// Define the Check Group that this menu item will be in, if we want it to be in a check group. -1 sets it in no check group.
		%checkGroup = "4";
		
		// Inform the GuiMenuBar control to add the new menu item with the defined fields
		%thisGuiMenuBar.addMenuItem(%menu,%menuItemText,%menuItemId,%accelerator,%checkGroup);

.. cpp:function:: void GuiMenuBar::addSubmenuItem(string menuTarget, string menuItem, string submenuItemText, int submenuItemId, string accelerator, int checkGroup)

	Adds a menu item to the specified menu. The menu argument can be either the text of a menu or its id.

	:param menuTarget: Menu to affect a submenu in
	:param menuItem: Menu item to affect
	:param submenuItemText: Text to show for the new submenu
	:param submenuItemId: Id for the new submenu
	:param accelerator: Accelerator key for the new submenu
	:param checkGroup: Which check group the new submenu should be in, or -1 for none.

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or  %menuTarget = "3";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "5";
		
		// Define the text for the new submenu
		%submenuItemText = "New Submenu Item";
		
		// Define the id for the new submenu
		%submenuItemId = "4";
		
		// Define the accelerator key for the new submenu
		%accelerator = "n";
		
		// Define the checkgroup for the new submenu
		%checkgroup = "7";
		
		// Request the GuiMenuBar control to add the new submenu with the defined information
		%thisGuiMenuBar.addSubmenuItem(%menuTarget,%menuItem,%submenuItemText,%submenuItemId,%accelerator,%checkgroup);

.. cpp:function:: void GuiMenuBar::clearMenuItems(string menuTarget)

	Removes all the menu items from the specified menu.

	:param menuTarget: Menu to remove all items from

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Inform the GuiMenuBar control to clear all menu items from the defined menu
		%thisGuiMenuBar.clearMenuItems(%menuTarget);

.. cpp:function:: void GuiMenuBar::clearMenus(int param1, int param2)

	Clears all the menus from the menu bar.

	Example::

		// Inform the GuiMenuBar control to clear all menus from itself.
		%thisGuiMenuBar.clearMenus();

.. cpp:function:: void GuiMenuBar::clearSubmenuItems(string menuTarget, string menuItem)

	Removes all the menu items from the specified submenu.

	:param menuTarget: Menu to affect a submenu in
	:param menuItem: Menu item to affect

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "5";
		
		// Inform the GuiMenuBar to remove all submenu items from the defined menu item
		%thisGuiMenuBar.clearSubmenuItems(%menuTarget,%menuItem);

.. cpp:function:: void GuiMenuBar::onMenuItemSelect(string menuId, string menuText, string menuItemId, string menuItemText)

	Called whenever an item in a menu is selected.

	:param menuId: Index id of the menu which contains the selected menu item
	:param menuText: Text of the menu which contains the selected menu item
	:param menuItemId: Index id of the selected menu item
	:param menuItemText: Text of the selected menu item

	Example::

		// A menu item has been selected, causing the callback to occur.GuiMenuBar::onMenuItemSelect(%this,%menuId,%menuText,%menuItemId,%menuItemText)
		{
		   // Code to run when the callback occurs
		}

.. cpp:function:: void GuiMenuBar::onMenuSelect(string menuId, string menuText)

	Called whenever a menu is selected.

	:param menuId: Index id of the clicked menu
	:param menuText: Text of the clicked menu

	Example::

		// A menu has been selected, causing the callback to occur.GuiMenuBar::onMenuSelect(%this,%menuId,%menuText)
		{
		   // Code to run when the callback occurs
		}

.. cpp:function:: void GuiMenuBar::onMouseInMenu(bool isInMenu)

	Called whenever the mouse enters, or persists is in the menu.

	:param isInMenu: True if the mouse has entered the menu, otherwise is false.

	Example::

		// Mouse enters or persists within the menu, causing the callback to occur.GuiMenuBar::onMouseInMenu(%this,%hasLeftMenu)
		{
		   // Code to run when the callback occurs
		}

.. cpp:function:: void GuiMenuBar::onSubmenuSelect(string submenuId, string submenuText)

	Called whenever a submenu is selected.

	:param submenuId: Id of the selected submenu
	:param submenuText: Text of the selected submenu

	Example::

		GuiMenuBar::onSubmenuSelect(%this,%submenuId,%submenuText)
		{
		   // Code to run when the callback occurs
		}

.. cpp:function:: void GuiMenuBar::removeMenu(string menuTarget)

	Removes the specified menu from the menu bar.

	:param menuTarget: Menu to remove from the menu bar

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Inform the GuiMenuBar to remove the defined menu from the menu bar
		%thisGuiMenuBar.removeMenu(%menuTarget);

.. cpp:function:: void GuiMenuBar::removeMenuItem(string menuTarget, string menuItemTarget)

	Removes the specified menu item from the menu.

	:param menuTarget: Menu to affect the menu item in
	:param menuItem: Menu item to affect

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "5";
		
		// Request the GuiMenuBar control to remove the define menu item
		%thisGuiMenuBar.removeMenuItem(%menuTarget,%menuItem);

.. cpp:function:: void GuiMenuBar::setCheckmarkBitmapIndex(int bitmapindex)

	Sets the menu bitmap index for the check mark image.

	:param bitmapIndex: Bitmap index for the check mark image.

	Example::

		// Define the bitmap index
		%bitmapIndex = "2";
		
		// Inform the GuiMenuBar control of the proper bitmap index for the check mark image
		%thisGuiMenuBar.setCheckmarkBitmapIndex(%bitmapIndex);

.. cpp:function:: void GuiMenuBar::setMenuBitmapIndex(string menuTarget, int bitmapindex, bool bitmaponly, bool drawborder)

	Sets the bitmap index for the menu and toggles rendering only the bitmap.

	:param menuTarget: Menu to affect
	:param bitmapindex: Bitmap index to set for the menu
	:param bitmaponly: If true, only the bitmap will be rendered
	:param drawborder: If true, a border will be drawn around the menu.

	Example::

		// Define the menuTarget to affect
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Set the bitmap index
		%bitmapIndex = "5";
		
		// Set if we are only to render the bitmap or not
		%bitmaponly = "true";
		
		// Set if we are rendering a border or not
		%drawborder = "true";
		
		// Inform the GuiMenuBar of the bitmap and rendering changes
		%thisGuiMenuBar.setMenuBitmapIndex(%menuTarget,%bitmapIndex,%bitmapOnly,%drawBorder);

.. cpp:function:: void GuiMenuBar::setMenuItemBitmap(string menuTarget, string menuItemTarget, int bitmapIndex)

	Sets the specified menu item bitmap index in the bitmap array. Setting the item's index to -1 will remove any bitmap.

	:param menuTarget: Menu to affect the menuItem in
	:param menuItem: Menu item to affect
	:param bitmapIndex: Bitmap index to set the menu item to

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or  %menuTarget = "3";
		
		// Define the menuItem"
		%menuItem = "New Menu Item";  or %menuItem = "2";
		
		// Define the bitmapIndex
		%bitmapIndex = "6";
		
		// Inform the GuiMenuBar control to set the menu item to the defined bitmap
		%thisGuiMenuBar.setMenuItemBitmap(%menuTarget,%menuItem,%bitmapIndex);

.. cpp:function:: void GuiMenuBar::setMenuItemChecked(string menuTarget, string menuItemTarget, bool checked)

	Sets the menu item bitmap to a check mark, which by default is the first element in the bitmap array (although this may be changed with setCheckmarkBitmapIndex() ). Any other menu items in the menu with the same check group become unchecked if they are checked.

	:param menuTarget: Menu to work in
	:param menuItem: Menu item to affect
	:param checked: Whether we are setting it to checked or not

	:return: If not void, return value and description

.. cpp:function:: void GuiMenuBar::setMenuItemEnable(string menuTarget, string menuItemTarget, bool enabled)

	sets the menu item to enabled or disabled based on the enable parameter. The specified menu and menu item can either be text or ids. Detailed description

	:param menuTarget: Menu to work in
	:param menuItemTarget: The menu item inside of the menu to enable or disable
	:param enabled: Boolean enable / disable value.

	Example::

		// Define the menu
		%menu = "New Menu";  or  %menu = "4";
		
		// Define the menu item
		%menuItem = "New Menu Item";  or %menuItem = "2";
		
		// Define the enabled state
		%enabled = "true";
		
		// Inform the GuiMenuBar control to set the enabled state of the requested menu item
		%thisGuiMenuBar.setMenuItemEnable(%menu,%menuItme,%enabled);

.. cpp:function:: void GuiMenuBar::setMenuItemSubmenuState(string menuTarget, string menuItem, bool isSubmenu)

	Sets the given menu item to be a submenu.

	:param menuTarget: Menu to affect a submenu in
	:param menuItem: Menu item to affect
	:param isSubmenu: Whether or not the menuItem will become a subMenu or not

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "5";
		
		// Define whether or not the Menu Item is a sub menu or not
		%isSubmenu = "true";
		
		// Inform the GuiMenuBar control to set the defined menu item to be a submenu or not.
		%thisGuiMenuBar.setMenuItemSubmenuState(%menuTarget,%menuItem,%isSubmenu);

.. cpp:function:: void GuiMenuBar::setMenuItemText(string menuTarget, string menuItemTarget, string newMenuItemText)

	Sets the text of the specified menu item to the new string.

	:param menuTarget: Menu to affect
	:param menuItem: Menu item in the menu to change the text at
	:param newMenuItemText: New menu text

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or  %menuTarget = "4";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "2";
		
		// Define the new text for the menu item
		%newMenuItemText = "Very New Menu Item";
		
		// Inform the GuiMenuBar control to change the defined menu item with the new text
		%thisGuiMenuBar.setMenuItemText(%menuTarget,%menuItem,%newMenuItemText);

.. cpp:function:: void GuiMenuBar::setMenuItemVisible(string menuTarget, string menuItemTarget, bool isVisible)

	Brief Description. Detailed description

	:param menuTarget: Menu to affect the menu item in
	:param menuItem: Menu item to affect
	:param isVisible: Visible state to set the menu item to.

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or  %menuTarget = "3";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "2";
		
		// Define the visibility state
		%isVisible = "true";
		
		// Inform the GuiMenuBarControl of the visibility state of the defined menu item
		%thisGuiMenuBar.setMenuItemVisible(%menuTarget,%menuItem,%isVisible);

.. cpp:function:: void GuiMenuBar::setMenuMargins(int horizontalMargin, int verticalMargin, int bitmapToTextSpacing)

	Sets the menu rendering margins: horizontal, vertical, bitmap spacing. Detailed description

	:param horizontalMargin: Number of pixels on the left and right side of a menu's text.
	:param verticalMargin: Number of pixels on the top and bottom of a menu's text.
	:param bitmapToTextSpacing: Number of pixels between a menu's bitmap and text.

	Example::

		// Define the horizontalMargin
		%horizontalMargin = "5";
		
		// Define the verticalMargin
		%verticalMargin = "5";
		
		// Define the bitmapToTextSpacing
		%bitmapToTextSpacing = "12";
		
		// Inform the GuiMenuBar control to set its margins based on the defined values.
		%thisGuiMenuBar.setMenuMargins(%horizontalMargin,%verticalMargin,%bitmapToTextSpacing);

.. cpp:function:: void GuiMenuBar::setMenuText(string menuTarget, string newMenuText)

	Sets the text of the specified menu to the new string.

	:param menuTarget: Menu to affect
	:param newMenuText: New menu text

	Example::

		// Define the menu to affect%menu = "New Menu";  or %menu = "3";// Define the text to change the menu to
		%newMenuText = "Still a New Menu";
		
		// Inform the GuiMenuBar control to change the defined menu to the defined text
		%thisGuiMenuBar.setMenuText(%menu,%newMenuText);

.. cpp:function:: void GuiMenuBar::setMenuVisible(string menuTarget, bool visible)

	Sets the whether or not to display the specified menu.

	:param menuTarget: Menu item to affect
	:param visible: Whether the menu item will be visible or not

	Example::

		// Define the menu to work with
		%menuTarget = "New Menu";  or  %menuTarget = "4";
		
		// Define if the menu should be visible or not
		%visible = "true";
		
		// Inform the GuiMenuBar control of the new visibility state for the defined menu
		%thisGuiMenuBar.setMenuVisible(%menuTarget,%visible);

.. cpp:function:: void GuiMenuBar::setSubmenuItemChecked(string menuTarget, string menuItemTarget, string submenuItemText, bool checked)

	Sets the menu item bitmap to a check mark, which by default is the first element in the bitmap array (although this may be changed with setCheckmarkBitmapIndex() ). Any other menu items in the menu with the same check group become unchecked if they are checked.

	:param menuTarget: Menu to affect a submenu in
	:param menuItem: Menu item to affect
	:param submenuItemText: Text to show for submenu
	:param checked: Whether or not this submenu item will be checked.

	:return: If not void, return value and description

	Example::

		// Define the menuTarget
		%menuTarget = "New Menu";  or %menuTarget = "3";
		
		// Define the menuItem
		%menuItem = "New Menu Item";  or  %menuItem = "5";
		
		// Define the text for the new submenu
		%submenuItemText = "Submenu Item";
		
		// Define if this submenu item should be checked or not
		%checked = "true";
		
		// Inform the GuiMenuBar control to set the checked state of the defined submenu item
		%thisGuiMenuBar.setSubmenuItemChecked(%menuTarget,%menuItem,%submenuItemText,%checked);

Fields
------


.. cpp:member:: int  GuiMenuBar::padding

	Extra padding to add to the bounds of the control.
