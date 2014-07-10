GuiObjectView
=============

GUI control which displays a 3D model.

Inherit:
	:doc:`GuiTSCtrl`

Description
-----------

GUI control which displays a 3D model.

Model displayed in the control can have other objects mounted onto it, and the light settings can be adjusted.

Example::

	newGuiObjectView(ObjectPreview)
	   {
	      shapeFile = "art/shapes/items/kit/healthkit.dts";
	      mountedNode = "mount0";
	      lightColor = "1 1 1 1";
	      lightAmbient = "0.5 0.5 0.5 1";
	      lightDirection = "0 0.707 -0.707";
	      orbitDiststance = "2";
	      minOrbitDiststance = "0.917688";
	      maxOrbitDiststance = "5";
	      cameraSpeed = "0.01";
	      cameraZRot = "0";
	      forceFOV = "0";
	      reflectPriority = "0";
	   };


Methods
-------


.. cpp:function:: float GuiObjectView::getCameraSpeed()

	Return the current multiplier for camera zooming and rotation.

	:return:  zooming / rotation multiplier value.

	Example::

		// Request the current camera zooming and rotation multiplier value
		%multiplier = %thisGuiObjectView.getCameraSpeed();

.. cpp:function:: string GuiObjectView::getModel()

	Return the model displayed in this view.

	:return: Name of the displayed model.

	Example::

		// Request the displayed model name from the GuiObjectView object.
		%modelName = %thisGuiObjectView.getModel();

.. cpp:function:: string GuiObjectView::getMountedModel()

	Return the name of the mounted model.

	:return: Name of the mounted model.

	Example::

		// Request the name of the mounted model from the GuiObjectView object
		%mountedModelName = %thisGuiObjectView.getMountedModel();

.. cpp:function:: string GuiObjectView::getMountSkin(int param1, int param2)

	Return the name of skin used on the mounted model.

	:return: Name of the skin used on the mounted model.

	Example::

		// Request the skin name from the model mounted on to the main model in the control
		%mountModelSkin = %thisGuiObjectView.getMountSkin();

.. cpp:function:: float GuiObjectView::getOrbitDistance()

	Return the current distance at which the camera orbits the object.

	:return: The distance at which the camera orbits the object.

	Example::

		// Request the current orbit distance
		%orbitDistance = %thisGuiObjectView.getOrbitDistance();

.. cpp:function:: string GuiObjectView::getSkin()

	Return the name of skin used on the primary model.

	:return: Name of the skin used on the primary model.

	Example::

		// Request the name of the skin used on the primary model in the control
		%skinName = %thisGuiObjectView.getSkin();

.. cpp:function:: void GuiObjectView::onMouseEnter()

	Called whenever the mouse enters the control.

	Example::

		// The mouse has entered the control, causing the callback to occurGuiObjectView::onMouseEnter(%this)
		   {
		      // Code to run when the mouse enters this control
		   }

.. cpp:function:: void GuiObjectView::onMouseLeave()

	Called whenever the mouse leaves the control.

	Example::

		// The mouse has left the control, causing the callback to occurGuiObjectView::onMouseLeave(%this)
		   {
		      // Code to run when the mouse leaves this control
		   }

.. cpp:function:: void GuiObjectView::setCameraSpeed(float factor)

	Sets the multiplier for the camera rotation and zoom speed.

	:param factor: Multiplier for camera rotation and zoom speed.

	Example::

		// Set the factor value
		%factor = "0.75";
		
		// Inform the GuiObjectView object to set the camera speed.
		%thisGuiObjectView.setCameraSpeed(%factor);

.. cpp:function:: void GuiObjectView::setLightAmbient(ColorF color)

	Set the light ambient color on the sun object used to render the model.

	:param color: Ambient color of sunlight.

	Example::

		// Define the sun ambient color value
		%color = "1.0 0.4 0.6";
		
		// Inform the GuiObjectView object to set the sun ambient color to the requested value
		%thisGuiObjectView.setLightAmbient(%color);

.. cpp:function:: void GuiObjectView::setLightColor(ColorF color)

	Set the light color on the sun object used to render the model.

	:param color: Color of sunlight.

	Example::

		// Set the color value for the sun
		%color = "1.0 0.4 0.5";
		
		// Inform the GuiObjectView object to change the sun color to the defined value
		%thisGuiObjectView.setLightColor(%color);

.. cpp:function:: void GuiObjectView::setLightDirection(Point3F direction)

	Set the light direction from which to light the model.

	:param direction: XYZ direction from which the light will shine on the model

	Example::

		// Set the light direction
		%direction = "1.0 0.2 0.4"// Inform the GuiObjectView object to change the light direction to the defined value
		%thisGuiObjectView.setLightDirection(%direction);

.. cpp:function:: void GuiObjectView::setModel(string shapeName)

	Sets the model to be displayed in this control.

	:param shapeName: Name of the model to display.

	Example::

		// Define the model we want to display
		%shapeName = "gideon.dts";
		
		// Tell the GuiObjectView object to display the defined model
		%thisGuiObjectView.setModel(%shapeName);

.. cpp:function:: void GuiObjectView::setMount(string shapeName, string mountNodeIndexOrName)

	Mounts the given model to the specified mount point of the primary model displayed in this control. Detailed description

	:param shapeName: Name of the model to mount.
	:param mountNodeIndexOrName: Index or name of the mount point to be mounted to. If index, corresponds to "mountN" in your shape where N is the number passed here.

	Example::

		// Set the shapeName to mount
		%shapeName = "GideonGlasses.dts"// Set the mount node of the primary model in the control to mount the new shape at
		%mountNodeIndexOrName = "3";
		//OR:
		%mountNodeIndexOrName = "Face";
		
		// Inform the GuiObjectView object to mount the shape at the specified node.
		%thisGuiObjectView.setMount(%shapeName,%mountNodeIndexOrName);

.. cpp:function:: void GuiObjectView::setMountedModel(string shapeName)

	Sets the model to be mounted on the primary model.

	:param shapeName: Name of the model to mount.

	Example::

		// Define the model name to mount
		%modelToMount = "GideonGlasses.dts";
		
		// Inform the GuiObjectView object to mount the defined model to the existing model in the control
		%thisGuiObjectView.setMountedModel(%modelToMount);

.. cpp:function:: void GuiObjectView::setMountSkin(string skinName)

	Sets the skin to use on the mounted model.

	:param skinName: Name of the skin to set on the model mounted to the main model in the control

	Example::

		// Define the name of the skin
		%skinName = "BronzeGlasses";
		
		// Inform the GuiObjectView Control of the skin to use on the mounted model
		%thisGuiObjectViewCtrl.setMountSkin(%skinName);

.. cpp:function:: void GuiObjectView::setOrbitDistance(float distance)

	Sets the distance at which the camera orbits the object. Clamped to the acceptable range defined in the class by min and max orbit distances. Detailed description

	:param distance: The distance to set the orbit to (will be clamped).

	Example::

		// Define the orbit distance value
		%orbitDistance = "1.5";
		
		// Inform the GuiObjectView object to set the orbit distance to the defined value
		%thisGuiObjectView.setOrbitDistance(%orbitDistance);

.. cpp:function:: void GuiObjectView::setSeq(string indexOrName)

	Sets the animation to play for the viewed object.

	:param indexOrName: The index or name of the animation to play.

	Example::

		// Set the animation index value, or animation sequence name.
		%indexVal = "3";
		//OR:
		%indexVal = "idle";
		
		// Inform the GuiObjectView object to set the animation sequence of the object in the control.
		%thisGuiObjectVew.setSeq(%indexVal);

.. cpp:function:: void GuiObjectView::setSkin(string skinName)

	Sets the skin to use on the model being displayed.

	:param skinName: Name of the skin to use.

	Example::

		// Define the skin we want to apply to the main model in the control
		%skinName = "disco_gideon";
		
		// Inform the GuiObjectView control to update the skin the to defined skin
		%thisGuiObjectView.setSkin(%skinName);

Fields
------


.. cpp:member:: string  GuiObjectView::animSequence

	The animation sequence to play on the model.

.. cpp:member:: Point3F  GuiObjectView::cameraRotation

	Set the camera rotation.

.. cpp:member:: float  GuiObjectView::cameraSpeed

	Multiplier for mouse camera operations.

.. cpp:member:: ColorF  GuiObjectView::lightAmbient

	Ambient color of the sunlight used to render the model.

.. cpp:member:: ColorF  GuiObjectView::lightColor

	Diffuse color of the sunlight used to render the model.

.. cpp:member:: Point3F  GuiObjectView::lightDirection

	Direction from which the model is illuminated.

.. cpp:member:: float  GuiObjectView::maxOrbitDiststance

	Minimum distance below which the camera will not zoom in further.

.. cpp:member:: float  GuiObjectView::minOrbitDiststance

	Maxiumum distance to which the camera can be zoomed out.

.. cpp:member:: string  GuiObjectView::mountedNode

	Name of node on primary model to which to mount the secondary shape.

.. cpp:member:: filename  GuiObjectView::mountedShapeFile

	Optional shape file to mount on the primary model (e.g. weapon).

.. cpp:member:: string  GuiObjectView::mountedSkin

	Skin name used on mounted shape file.

.. cpp:member:: float  GuiObjectView::orbitDiststance

	Distance from which to render the model.

.. cpp:member:: filename  GuiObjectView::shapeFile

	The object model shape file to show in the view.

.. cpp:member:: string  GuiObjectView::skin

	The skin to use on the object model.
