GuiTreeViewCtrl
===============

Hierarchical list of text items with optional icons.

Inherit:
	:doc:`GuiArrayCtrl`

Description
-----------

Can also be used to inspect SimObject hierarchies, primarily within editors.

GuiTreeViewCtrls can either display arbitrary user-defined trees or can be used to display SimObject hierarchies where each parent node in the tree is a SimSet or SimGroup and each leaf node is a SimObject.

Each item in the tree has a text and a value. For trees that display SimObject hierarchies, the text for each item is automatically derived from objects while the value for each item is the ID of the respective SimObject. For trees that are not tied to SimObjects, both text and value of each item are set by the user.

Additionally, items in the tree can have icons.

Each item in the tree has a distinct numeric ID that is unique within its tree. The ID of the root item, which is always present on a tree, is 0.

Example::

	newGuiTreeViewCtrl(DatablockEditorTree)
	{
	   tabSize = "16";
	   textOffset = "2";
	   fullRowSelect = "0";
	   itemHeight = "21";
	   destroyTreeOnSleep = "0";
	   MouseDragging = "0";
	   MultipleSelections = "1";
	   DeleteObjectAllowed = "1";
	   DragToItemAllowed = "0";
	   ClearAllOnSingleSelection = "1";
	   showRoot = "1";
	   internalNamesOnly = "0";
	   objectNamesOnly = "0";
	   compareToObjectID = "0";
	   Profile = "GuiTreeViewProfile";
	   tooltipprofile = "GuiToolTipProfile";
	   hovertime = "1000";
	};


Methods
-------


.. cpp:function:: void GuiTreeViewCtrl::addSelection(int id, bool isLastSelection)

	Add an item/object to the current selection.

	:param id: ID of item/object to add to the selection.
	:param isLastSelection: Whether there are more pending items/objects to be added to the selection. If false, the control will defer refreshing the tree and wait until addSelection() is called with this parameter set to true.

.. cpp:function:: bool GuiTreeViewCtrl::buildIconTable()
	
	Builds an icon table.

.. cpp:function:: bool GuiTreeViewCtrl::canRenameObject(SimObject object)


.. cpp:function:: void GuiTreeViewCtrl::clear()

	Empty tree.

.. cpp:function:: void GuiTreeViewCtrl::clearFilterText()

	Clear the current item filtering pattern.

.. cpp:function:: void GuiTreeViewCtrl::clearSelection()

	Unselect all currently selected items.

.. cpp:function:: void GuiTreeViewCtrl::deleteSelection()

	Delete all items/objects in the current selection.

.. cpp:function:: bool GuiTreeViewCtrl::editItem(TreeItemId item, string newText, string newValue)


.. cpp:function:: bool GuiTreeViewCtrl::expandItem(TreeItemId item, bool expand)


.. cpp:function:: int GuiTreeViewCtrl::findChildItemByName(int parentId, string childName)

	Get the child item of the given parent item whose text matches childName .

	:param parentId: Item ID of the parent in which to look for the child.
	:param childName: Text of the child item to find.

	:return: .

.. cpp:function:: int GuiTreeViewCtrl::findItemByName(string text)

	Get the ID of the item whose text matches the given text .

	:param text: Item text to match.

	:return: ID of the item or -1 if no item matches the given text. 

.. cpp:function:: int GuiTreeViewCtrl::findItemByObjectId(int id)
	
	Find item by object id and returns the mId

.. cpp:function:: int GuiTreeViewCtrl::findItemByValue(string value)

	Get the ID of the item whose value matches value .

	:param value: Value text to match.

	:return: ID of the item or -1 if no item has the given value. 

.. cpp:function:: int GuiTreeViewCtrl::getChild(TreeItemId item)


.. cpp:function:: string GuiTreeViewCtrl::getFilterText()

	Get the current filter expression. Only tree items whose text matches this expression are displayed. By default, the expression is empty and all items are shown.

	:return: The current filter pattern or an empty string if no filter pattern is currently active.

.. cpp:function:: string GuiTreeViewCtrl::getItemText(TreeItemId item)


.. cpp:function:: string GuiTreeViewCtrl::getItemValue(TreeItemId item)


.. cpp:function:: int GuiTreeViewCtrl::getNextSibling(TreeItemId item)


.. cpp:function:: int GuiTreeViewCtrl::getParent(TreeItemId item)


.. cpp:function:: int GuiTreeViewCtrl::getPrevSibling(TreeItemId item)


.. cpp:function:: int GuiTreeViewCtrl::getSelectedItem(int index)

	Return the selected item at the given index.

.. cpp:function:: int GuiTreeViewCtrl::getSelectedObject(int index)

	Return the currently selected SimObject at the given index in inspector mode or -1.

.. cpp:function:: string GuiTreeViewCtrl::getTextToRoot(TreeItemId item, Delimiter  = ,  none)

	gets the text from the current node to the root, concatenating at each branch upward, with a specified delimiter optionally

.. cpp:function:: bool GuiTreeViewCtrl::handleRenameObject(string newName, SimObject object)


.. cpp:function:: void GuiTreeViewCtrl::hideSelection(bool state)

	Call SimObject::setHidden ( state ) on all objects in the current selection.

	:param state: Visibility state to set objects in selection to.

.. cpp:function:: int GuiTreeViewCtrl::insertItem(int parentId, string text, string value, string icon, int normalImage, int expandedImage)

	Add a new item to the tree.

	:param parentId: Item ID of parent to which to add the item as a child. 0 is root item.
	:param text: Text to display on the item in the tree.
	:param value: Behind-the-scenes value of the item.
	:param icon: 
	:param normalImage: 
	:param expandedImage: 

	:return: The ID of the newly added item. 

.. cpp:function:: bool GuiTreeViewCtrl::isItemSelected(int id)

	Check whether the given item is currently selected in the tree.

	:param id: Item/object ID.

	:return: True if the given item/object is currently selected in the tree. 

.. cpp:function:: bool GuiTreeViewCtrl::isParentItem(int id)

	Returns true if the given item contains child items.

.. cpp:function:: bool GuiTreeViewCtrl::isValidDragTarget(int id, string value)


.. cpp:function:: void GuiTreeViewCtrl::lockSelection(bool lock)

	Set whether the current selection can be changed by the user or not.

	:param lock: If true, the current selection is frozen and cannot be changed. If false, the selection may be modified.

.. cpp:function:: bool GuiTreeViewCtrl::markItem(TreeItemId item, bool mark)


.. cpp:function:: void GuiTreeViewCtrl::moveItemDown(TreeItemId item)


.. cpp:function:: void GuiTreeViewCtrl::moveItemUp(TreeItemId item)


.. cpp:function:: void GuiTreeViewCtrl::onAddGroupSelected(SimGroup group)


.. cpp:function:: void GuiTreeViewCtrl::onAddMultipleSelectionBegin()


.. cpp:function:: void GuiTreeViewCtrl::onAddMultipleSelectionEnd()


.. cpp:function:: void GuiTreeViewCtrl::onAddSelection(int itemOrObjectId, bool isLastSelection)


.. cpp:function:: void GuiTreeViewCtrl::onBeginReparenting()


.. cpp:function:: void GuiTreeViewCtrl::onClearSelection()


.. cpp:function:: void GuiTreeViewCtrl::onDefineIcons()


.. cpp:function:: bool GuiTreeViewCtrl::onDeleteObject(SimObject object)


.. cpp:function:: void GuiTreeViewCtrl::onDeleteSelection()


.. cpp:function:: void GuiTreeViewCtrl::onDragDropped()


.. cpp:function:: void GuiTreeViewCtrl::onEndReparenting()


.. cpp:function:: void GuiTreeViewCtrl::onInspect(int itemOrObjectId)


.. cpp:function:: void GuiTreeViewCtrl::onKeyDown(int modifier, int keyCode)


.. cpp:function:: void GuiTreeViewCtrl::onMouseDragged()


.. cpp:function:: void GuiTreeViewCtrl::onMouseUp(int hitItemId, int mouseClickCount)


.. cpp:function:: void GuiTreeViewCtrl::onObjectDeleteCompleted()


.. cpp:function:: void GuiTreeViewCtrl::onRemoveSelection(int itemOrObjectId)


.. cpp:function:: void GuiTreeViewCtrl::onReparent(int itemOrObjectId, int oldParentItemOrObjectId, int newParentItemOrObjectId)


.. cpp:function:: void GuiTreeViewCtrl::onRightMouseDown(int itemId, Point2I mousePos, SimObject object)


.. cpp:function:: void GuiTreeViewCtrl::onRightMouseUp(int itemId, Point2I mousePos, SimObject object)


.. cpp:function:: void GuiTreeViewCtrl::onSelect(int itemOrObjectId)


.. cpp:function:: void GuiTreeViewCtrl::onUnselect(int itemOrObjectId)


.. cpp:function:: void GuiTreeViewCtrl::open(SimSet obj, bool okToEdit)

	Set the root of the tree view to the specified object, or to the root set.

.. cpp:function:: bool GuiTreeViewCtrl::removeItem(TreeItemId item)


.. cpp:function:: void GuiTreeViewCtrl::removeSelection()
	
	Deselects an item.

.. cpp:function:: void GuiTreeViewCtrl::scrollVisible(TreeItemId item)


.. cpp:function:: int GuiTreeViewCtrl::scrollVisibleByObjectId(int id)
	
	Show item by object id.returns true if sucessful.

.. cpp:function:: bool GuiTreeViewCtrl::selectItem(TreeItemId item, bool select)


.. cpp:function:: void GuiTreeViewCtrl::setDebug(bool value)

	Enable/disable debug output.

.. cpp:function:: void GuiTreeViewCtrl::setFilterText(string pattern)

	Set the pattern by which to filter items in the tree. Only items in the tree whose text matches this pattern are displayed.

	:param pattern: New pattern based on which visible items in the tree should be filtered. If empty, all items become visible.

.. cpp:function:: void GuiTreeViewCtrl::setItemImages(int id, int normalImage, int expandedImage)

	Sets the normal and expanded images to show for the given item.

.. cpp:function:: void GuiTreeViewCtrl::setItemTooltip(int id, string text)

	Set the tooltip to show for the given item.

.. cpp:function:: void GuiTreeViewCtrl::showItemRenameCtrl(TreeItemId id)

	Show the rename text field for the given item (only one at a time).

.. cpp:function:: void GuiTreeViewCtrl::sort(int parent, bool traverseHierarchy, bool parentsFirst, bool caseSensitive)

	Sorts all items of the given parent (or root). With 'hierarchy', traverses hierarchy.

.. cpp:function:: void GuiTreeViewCtrl::toggleHideSelection()

	Toggle the hidden state of all objects in the current selection.

.. cpp:function:: void GuiTreeViewCtrl::toggleLockSelection()

	Toggle the locked state of all objects in the current selection.

Fields
------


.. cpp:member:: void  GuiTreeViewCtrl::addChildSelectionByValue

	addChildSelectionByValue(TreeItemId parent, value)

.. cpp:member:: void  GuiTreeViewCtrl::buildVisibleTree

	Build the visible tree.

.. cpp:member:: void  GuiTreeViewCtrl::cancelRename

	For internal use.

.. cpp:member:: bool  GuiTreeViewCtrl::canRenameObjects

	If true clicking on a selected item ( that is an object and not the root ) will allow you to rename it.

.. cpp:member:: bool  GuiTreeViewCtrl::clearAllOnSingleSelection


.. cpp:member:: bool  GuiTreeViewCtrl::compareToObjectID


.. cpp:member:: bool  GuiTreeViewCtrl::deleteObjectAllowed


.. cpp:member:: bool  GuiTreeViewCtrl::destroyTreeOnSleep

	If true, the entire tree item hierarchy is deleted when the control goes to sleep.

.. cpp:member:: bool  GuiTreeViewCtrl::dragToItemAllowed


.. cpp:member:: bool  GuiTreeViewCtrl::fullRowSelect


.. cpp:member:: int  GuiTreeViewCtrl::getFirstRootItem

	Get id for root item.

.. cpp:member:: int  GuiTreeViewCtrl::getItemCount


.. cpp:member:: string  GuiTreeViewCtrl::getSelectedItemList

	returns a space seperated list of mulitple item ids

.. cpp:member:: int  GuiTreeViewCtrl::getSelectedItemsCount


.. cpp:member:: string  GuiTreeViewCtrl::getSelectedObjectList

	Returns a space sperated list of all selected object ids.

.. cpp:member:: int  GuiTreeViewCtrl::itemHeight


.. cpp:member:: bool  GuiTreeViewCtrl::mouseDragging


.. cpp:member:: bool  GuiTreeViewCtrl::multipleSelections

	If true, multiple items can be selected concurrently.

.. cpp:member:: void  GuiTreeViewCtrl::onRenameValidate

	For internal use.

.. cpp:member:: void  GuiTreeViewCtrl::removeAllChildren

	removeAllChildren(TreeItemId parent)

.. cpp:member:: void  GuiTreeViewCtrl::removeChildSelectionByValue

	removeChildSelectionByValue(TreeItemId parent, value)

.. cpp:member:: bool  GuiTreeViewCtrl::renameInternal

	If true then object renaming operates on the internalName rather than the object name.

.. cpp:member:: bool  GuiTreeViewCtrl::showClassNameForUnnamedObjects

	If true, class names will be used as object names for unnamed objects.

.. cpp:member:: bool  GuiTreeViewCtrl::showClassNames

	If true, item text labels for objects will include class names.

.. cpp:member:: bool  GuiTreeViewCtrl::showInternalNames

	If true, item text labels for obje ts will include internal names.

.. cpp:member:: bool  GuiTreeViewCtrl::showObjectIds

	If true, item text labels for objects will include object IDs.

.. cpp:member:: bool  GuiTreeViewCtrl::showObjectNames

	If true, item text labels for objects will include object names.

.. cpp:member:: bool  GuiTreeViewCtrl::showRoot

	If true, the root item is shown in the tree.

.. cpp:member:: int  GuiTreeViewCtrl::tabSize


.. cpp:member:: int  GuiTreeViewCtrl::textOffset


.. cpp:member:: bool  GuiTreeViewCtrl::tooltipOnWidthOnly


.. cpp:member:: bool  GuiTreeViewCtrl::useInspectorTooltips

