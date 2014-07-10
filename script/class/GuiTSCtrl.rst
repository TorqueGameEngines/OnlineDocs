GuiTSCtrl
=========

Abstract base class for controls that render 3D scenes.

Inherit:
	:doc:`GuiContainer`

Description
-----------

GuiTSCtrl is the base class for controls that render 3D camera views in Torque. The class itself does not implement a concrete scene rendering. Use GuiObjectView to display invidiual shapes in the Gui and GameTSCtrl to render full scenes.


Methods
-------


.. cpp:function:: float GuiTSCtrl::calculateViewDistance(float radius)

	Given the camera's current FOV, get the distance from the camera's viewpoint at which the given radius will fit in the render area.

	:param radius: Radius in world-space units which should fit in the view.

	:return: The distance from the viewpoint at which the given radius would be fully visible. 

.. cpp:function:: Point2F GuiTSCtrl::getWorldToScreenScale()

	Get the ratio between world-space units and pixels.

	:return: The amount of world-space units covered by the extent of a single pixel. 

.. cpp:function:: Point3F GuiTSCtrl::project(Point3F worldPosition)

	Transform world-space coordinates to screen-space (x, y, depth) coordinates.

	:param worldPosition: The world-space position to transform to screen-space.

	:return: The 

.. cpp:function:: Point3F GuiTSCtrl::unproject(Point3F screenPosition)

	Transform 3D screen-space coordinates (x, y, depth) to world space. This method can be, for example, used to find the world-space position relating to the current mouse cursor position.

	:param screenPosition: The x/y position on the screen plus the depth from the screen-plane outwards.

	:return: The world-space position corresponding to the given screen-space coordinates. 

Fields
------


.. cpp:member:: float  GuiTSCtrl::cameraZRot

	Z rotation angle of camera.

.. cpp:member:: float  GuiTSCtrl::forceFOV

	The vertical field of view in degrees or zero to use the normal camera FOV.

.. cpp:member:: float  GuiTSCtrl::reflectPriority

	The share of the per-frame reflection update work this control's rendering should run. The reflect update priorities of all visible GuiTSCtrls are added together and each control is assigned a share of the per-frame reflection update time according to its percentage of the total priority value.

.. cpp:member:: GuiTSRenderStyles GuiTSCtrl::renderStyle

	Indicates how this control should render its contents.
