Precipitation
=============

The Torque 3D World Editor allows you to quickly add different types of precipitation to your level. However, Precipitation is used as a general term meaning any type of particle moving downward. The ability to quickly add rain, snow, or even a sandstorm to your level is built into the editor. 

Adding Precipitation
--------------------

To add Precipitation to a level, switch to the Library tab in the Scene Tree panel. Click on the Level tab amd double-click the Environment folder. Locate the Precipitation entry.

.. image:: precipitation/PrecipLibrary.jpg

Double-click the Precipitation entry.The Create Object dialog will appear.

.. image:: precipitation/NamePrecipRain.jpg

Enter a name for your Precipitation object. The Precipitation data field allows you to choose a datablock to start with as the basis for your new object. Click the drop down box for a list of available datablocks.

.. image:: precipitation/UseHeavyRainDB.jpg

For the Full template, your only choice is HeavyRain so select it then click Create New. Your new Precipitation object will be added to your level, and rain will start falling automatically. The stock datablock for HeavyRain simulates a light shower, so you may not see much rain falling:

.. image:: precipitation/PrecipAdded.jpg

The HeavyRain datablock is located in the game/art/datablocks/environment.cs file. Its initial data contains the following::

	datablock PrecipitationData(HeavyRain)
	{
	   soundProfile = "HeavyRainSound";

	   dropTexture = "art/environment/precipitation/rain";
	   splashTexture = "art/environment/precipitation/water_splash";
	   dropSize = 0.35;
	   splashSize = 0.1;
	   useTrueBillboards = false;
	   splashMS = 500;
	};

We will get into manipulating the datablock later.

Precipitation Properties
------------------------

Additional properties can be changed with the Inspector pane. To change a Precipitation objects properties using the Inspector Pane click the Scene tab, then click the name of your new Precipitation object. The Inspector pane will update to display the current properties of your new sun.

Inspector
~~~~~~~~~

name
	TypeName. Optional global name of this object.

id
	TypeCaseString. SimObjectId of this object. Read Only.

Source Class
	TypeCaseString. Source code class of this object. Read Only.

Transform
~~~~~~~~~

position
	MatrixPosition. Object world position.

rotation
	MatrixOrientation. Object world orientation.

scale
	Point3F. Object world scale.

Precipitation
~~~~~~~~~~~~~

numDrops
	TypeS32. Number of drops allowed to exists in the precipitation box at any one time.

boxWidth
	TypeF32. Width of precipitation box.

boxHeight
	TypeF32. Height of precipitation box.

Rendering
~~~~~~~~~

dropSize
	TypeF32. Size of each drop of precipitation. This will scale the texture.

splashSize
	TypeF32. Size of each splash animation for when a drop collides.

splashMS
	TypeS32. Life of splashes in milliseconds.

animateSplashes
	TypeS32. Check to enable splash animation on collision.

dropAnimateMS
	TypeS32. If greater than zero, will animate the drops from the frames in the texture.

fadeDist
	TypeF32. The distance at which fading of the drops begins.

fadeDistEnd
	TypeF32. The distance at which fading of the particles ends.

useTrueBillboards
	TypeBool. Check to make drops true (non axis-aligned) billboards.

useLighting
	TypeBool. Check to enable shading of the drops and splashes by the sun color.

glowIntensity
	TypeColorF. Set to 0 to disable the glow or or use it to control the intensity of each channel.

reflect
	TypeBool. This enables the precipitation to be rendered during reflection passes. This is expensive.

rotateWithCamVel
	TypeBool. Enables drops to rotate to face camera.

Collision
~~~~~~~~~

doCollision
	TypeBool. Allow collision with world objects.

hitPlayers
	TypeBool. Allow collision on player objects.

hitVehicles
	TypeBool. Allow collision on vechiles.

Movement
~~~~~~~~

followCam
	TypeBool. Enables system to follow the camera or stay where it is placed.

useWind
	TypeBool. Check to have the Sky property windSpeed affect precipitation.

minSpeed
	TypeF32. Minimum speed that a drop will fall.

maxSpeed
	TypeF32. Maximum speed that a drop will fall.

minMass
	TypeF32. Minimum mass of a drop.

mMaxMass
	TypeF32. Maximum mass of a drop.

Turbulence
~~~~~~~~~~

useTurbulence
	TypeBool. Check to enable turubulence. This causes precipitation drops to spiral while falling.

maxTurbulence
	TypeF32. Radius at which precipitation drops spiral when turbulence is enabled.

turbulenceSpeed
	TypeF32. Speed at which precipitation drops spiral when turbulence is enabled.

Game
~~~~

dataBlock
	TypeGameBaseData. Script datablock used for game objects.
