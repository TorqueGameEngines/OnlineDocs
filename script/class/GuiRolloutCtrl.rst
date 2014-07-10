GuiRolloutCtrl
==============

A container that shows a single child with an optional header bar that can be used to collapse and expand the rollout.

Inherit:
	:doc:`GuiControl`

Description
-----------

A rollout is a container that can be collapsed and expanded using smooth animation. By default, rollouts will display a header with a caption along the top edge of the control which can be clicked by the user to toggle the collapse state of the rollout.

Rollouts will automatically size themselves to exactly fit around their child control. They will also automatically position their child control in their upper left corner below the header (if present).


Methods
-------


.. cpp:function:: void GuiRolloutCtrl::collapse()

	Collapse the rollout if it is currently expanded. This will make the rollout's child control invisible.

.. cpp:function:: void GuiRolloutCtrl::expand()

	Expand the rollout if it is currently collapsed. This will make the rollout's child control visible.

.. cpp:function:: void GuiRolloutCtrl::instantCollapse()

	Instantly collapse the rollout without animation. To smoothly slide the rollout to collapsed state, use collapse() .

.. cpp:function:: void GuiRolloutCtrl::instantExpand()

	Instantly expand the rollout without animation. To smoothly slide the rollout to expanded state, use expand() .

.. cpp:function:: bool GuiRolloutCtrl::isExpanded()

	Determine whether the rollout is currently expanded, i.e. whether the child control is visible. Reimplemented from SimObject .

	:return: True if the rollout is expanded, false if not. 

.. cpp:function:: void GuiRolloutCtrl::onCollapsed()

	Called when the rollout is collapsed.

.. cpp:function:: void GuiRolloutCtrl::onExpanded()

	Called when the rollout is expanded.

.. cpp:function:: void GuiRolloutCtrl::onHeaderRightClick()

	Called when the user right-clicks on the rollout's header. This is useful for implementing context menus for rollouts.

.. cpp:function:: void GuiRolloutCtrl::sizeToContents()

	Resize the rollout to exactly fit around its child control. This can be used to manually trigger a recomputation of the rollout size.

.. cpp:function:: void GuiRolloutCtrl::toggleCollapse()

	Toggle the current collapse state of the rollout. If it is currently expanded, then collapse it. If it is currently collapsed, then expand it.

.. cpp:function:: void GuiRolloutCtrl::toggleExpanded(bool instantly)

	Toggle the current expansion state of the rollout If it is currently expanded, then collapse it. If it is currently collapsed, then expand it.

	:param instant: If true, the rollout will toggle its state without animation. Otherwise, the rollout will smoothly slide into the opposite state.

Fields
------


.. cpp:member:: bool  GuiRolloutCtrl::autoCollapseSiblings

	Whether to automatically collapse sibling rollouts. If this is true, the rollout will automatically collapse all sibling rollout controls when it is expanded. If this is false, the auto-collapse behavior can be triggered by CTRL (CMD on MAC) clicking the rollout header. CTRL/CMD clicking also works if this is false, in which case the auto-collapsing of sibling controls will be temporarily deactivated.

.. cpp:member:: string  GuiRolloutCtrl::caption

	Text label to display on the rollout header.

.. cpp:member:: bool  GuiRolloutCtrl::clickCollapse

	Whether the rollout can be collapsed by clicking its header.

.. cpp:member:: int  GuiRolloutCtrl::defaultHeight

	Default height of the client area. This is used when no child control has been added to the rollout.

.. cpp:member:: bool  GuiRolloutCtrl::expanded

	The current rollout expansion state.

.. cpp:member:: bool  GuiRolloutCtrl::hideHeader

	Whether to render the rollout header.

.. cpp:member:: RectI  GuiRolloutCtrl::margin

	Margin to put around child control.
