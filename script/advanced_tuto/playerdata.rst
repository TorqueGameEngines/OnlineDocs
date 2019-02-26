Player Datablock
*****************

Detailed Description
=====================
Defines properties for a Player object.

**See also:**
	Player 

Member Function Documentation
==============================
.. cpp:function:: void PlayerData::animationDone 	(	Player	*obj*	)  	

    Called on the server when a scripted animation completes.

    :param obj:	The Player object

**See also:**
    ``Player::setActionThread()`` for setting a scripted animation and its 'hold' parameter to determine if this callback is used. 

.. cpp:function:: void PlayerData::doDismount 	(	Player	*obj*	)  	

    Called when attempting to dismount the player from a vehicle.

    It is up to the ``doDismount()`` method to actually perform the dismount. Often there are some conditions that prevent this, such as the vehicle moving too fast.

    :param obj: The Player object

.. cpp:function:: void PlayerData::onEnterLiquid ( Player obj, float coverage, string type ) 			

    Called when the player enters a liquid.

    :param obj: The Player object
    :param coverage: Percentage of the player's bounding box covered by the liquid
    :param type: The type of liquid the player has entered

.. cpp:function:: void PlayerData::onEnterMissionArea ( Player obj )  	

    Called when the player enters the mission area.

    :param obj: The Player object

**See also:**
    MissionArea 

.. cpp:function:: void PlayerData::onLeaveLiquid 	( Player obj, string type ) 			

    Called when the player leaves a liquid.

    :param obj: The Player object
    :param type: The type of liquid the player has left

.. cpp:function:: void PlayerData::onLeaveMissionArea 	( 	Player  	obj 	 )  	

    Called when the player leaves the mission area.

    :param obj 	The Player object

**See also:**
    MissionArea 

.. cpp:function:: void PlayerData::onPoseChange ( Player obj, string oldPose, string newPose ) 			

    Called when the player changes poses.

    :param obj: The Player object
    :param oldPose: The pose the player is switching from.
    :param newPose: The pose the player is switching to.

.. cpp:function:: void PlayerData::onStartSprintMotion ( Player obj )  	

    Called when the player starts moving while in a Sprint pose.

    :param obj: The Player object

.. cpp:function:: void PlayerData::onStartSwim ( Player obj )  	

    Called when the player starts swimming.

    :param obj: The Player object

.. cpp:function:: void PlayerData::onStopSprintMotion 	( 	Player  	obj 	 )  	

    Called when the player stops moving while in a Sprint pose.

    :param obj: The Player object

.. cpp:function:: void PlayerData::onStopSwim 	( Player obj )  	

    Called when the player stops swimming.

    :param obj: The Player object 

Member Data Documentation
==========================

.. cpp:function:: float PlayerData::airControl

    Amount of movement control the player has when in the air.

    This is applied as a multiplier to the player's x and y motion.
    
.. cpp:function:: bool PlayerData::allowImageStateAnimation

    Allow mounted images to request a sequence be played on the Player.

    When true a new thread is added to the player to allow for mounted images to request a sequence be played on the player through the image's state machine. It is only optional so that we don't create a TSThread on the player if we don't need to.

.. cpp:function:: Point3F PlayerData::boundingBox

    Size of the bounding box used by the player for collision.

    Dimensions are given as "width depth height".
    
.. cpp:function:: float PlayerData::boxHeadBackPercentage

    Percentage of the player's bounding box depth that represents the back side of the head.

    Used when computing the damage location.

    **See also:** Player::getDamageLocation 

.. cpp:function:: float PlayerData::boxHeadFrontPercentage

    Percentage of the player's bounding box depth that represents the front side of the head.
    Used when computing the damage location.

    **See also:** Player::getDamageLocation 

.. cpp:function:: float PlayerData::boxHeadLeftPercentage

    Percentage of the player's bounding box width that represents the left side of the head.
    Used when computing the damage location.

    **See also:** Player::getDamageLocation 

.. cpp:function:: float PlayerData::boxHeadPercentage

    Percentage of the player's bounding box height that represents the head.
    Used when computing the damage location.

    **See also:** Player::getDamageLocation 

.. cpp:function:: float PlayerData::boxHeadRightPercentage

    Percentage of the player's bounding box width that represents the right side of the head.
    Used when computing the damage location.

    **See also:** Player::getDamageLocation 

.. cpp:function:: float PlayerData::boxTorsoPercentage

    Percentage of the player's bounding box height that represents the torso.
    Used when computing the damage location.

    **See also:** Player::getDamageLocation 

.. cpp:function:: float PlayerData::bubbleEmitTime

    Time in seconds to generate bubble particles after entering the water.\

.. cpp:function:: Point3F PlayerData::crouchBoundingBox

    Collision bounding box used when the player is crouching.

    **See also:** boundingBox 

.. cpp:function:: float PlayerData::crouchForce

    Force used to accelerate the player when crouching.
    
.. cpp:function:: DecalData PlayerData::DecalData

    Decal to place on the ground for player footsteps.

.. cpp:function:: float PlayerData::decalOffset

    Distance from the center of the model to the right foot.

    While this defines the distance to the right foot, it is also used to place the left foot decal as well. Just on the opposite side of the player.
    
.. cpp:function:: ParticleEmitterData PlayerData::dustEmitter

    Emitter used to generate dust particles.

.. note:: Currently unused. 

.. cpp:function:: SFXTrack PlayerData::exitingWater

    Sound to play when exiting the water with velocity >= exitSplashSoundVelocity.

    **See also:** exitSplashSoundVelocity 

.. cpp:function:: float PlayerData::exitSplashSoundVelocity

    Minimum velocity when leaving the water for the exitingWater sound to play.

    **See also:** exitingWater 

.. cpp:function:: float PlayerData::fallingSpeedThreshold

    Downward speed at which we consider the player falling.

.. cpp:function:: SFXTrack PlayerData::FootBubblesSound

    Sound to play when walking in water and coverage equals 1.0 (fully underwater).

.. cpp:function:: SFXTrack PlayerData::FootHardSound

    Sound to play when walking on a surface with Material footstepSoundId 1.

.. cpp:function:: SFXTrack PlayerData::FootMetalSound

    Sound to play when walking on a surface with Material footstepSoundId 2.

.. cpp:function:: ParticleEmitterData PlayerData::footPuffEmitter

    Particle emitter used to generate footpuffs (particles created as the player walks along the ground).

.. note:: The generation of foot puffs requires the appropriate triggeres to be defined in the player's animation sequences. Without these, no foot puffs will be generated. 

.. cpp:function:: int PlayerData::footPuffNumParts

    Number of footpuff particles to generate each step.

    Each foot puff is randomly placed within the defined foot puff radius. This includes having footPuffNumParts set to one.

    **See also:** footPuffRadius 

.. cpp:function:: float PlayerData::footPuffRadius

    Particle creation radius for footpuff particles.

    This is applied to each foot puff particle, even if footPuffNumParts is set to one. So set this value to zero if you want a single foot puff placed at exactly the same location under the player each time.

.. cpp:function:: SFXTrack PlayerData::FootShallowSound

    Sound to play when walking in water and coverage is less than footSplashHeight.

    **See also:** footSplashHeight 

.. cpp:function:: SFXTrack PlayerData::FootSnowSound

    Sound to play when walking on a surface with Material footstepSoundId 3.

.. cpp:function:: SFXTrack PlayerData::FootSoftSound

    Sound to play when walking on a surface with Material footstepSoundId 0.

.. cpp:function:: float PlayerData::footstepSplashHeight

    Water coverage level to choose between FootShallowSound and FootWadingSound.

**See also:** 
    * FootShallowSound 
    * FootWadingSound 

.. cpp:function:: SFXTrack PlayerData::FootUnderwaterSound

    Sound to play when walking in water and coverage equals 1.0 (fully underwater).

.. cpp:function:: SFXTrack PlayerData::FootWadingSound

    Sound to play when walking in water and coverage is less than 1, but > footSplashHeight.

    **See also:** footSplashHeight 

.. cpp:function:: float PlayerData::groundImpactMinSpeed

    Minimum falling impact speed to apply damage and initiate the camera shaking effect.

.. cpp:function:: Point3F PlayerData::groundImpactShakeAmp

    Amplitude of the camera shake effect after falling.

    This is how much to shake the camera.

.. cpp:function:: float PlayerData::groundImpactShakeDuration

    Duration (in seconds) of the camera shake effect after falling.

    This is how long to shake the camera.

.. cpp:function:: float PlayerData::groundImpactShakeFalloff

    Falloff factor of the camera shake effect after falling.

    This is how to fade the camera shake over the duration.

.. cpp:function:: Point3F PlayerData::groundImpactShakeFreq

    Frequency of the camera shake effect after falling.

    This is how fast to shake the camera.

.. cpp:function:: float PlayerData::hardSplashSoundVelocity

    Minimum velocity when entering the water for choosing between the impactWaterMedium and impactWaterHard sound to play.

**See also:**
    * impactWaterMedium 
    * impactWaterHard 

.. cpp:function:: float PlayerData::horizMaxSpeed

    Maximum horizontal speed.

.. note:: This limit is only enforced if the player's horizontal speed exceeds horizResistSpeed. 

**See also:**
    * horizResistSpeed 
    * horizResistFactor 

.. cpp:function:: float PlayerData::horizResistFactor

    Factor of resistence once horizResistSpeed has been reached.

**See also:**
    * horizMaxSpeed 
    * horizResistSpeed 

.. cpp:function:: float PlayerData::horizResistSpeed

    Horizontal speed at which resistence will take place.

**See also:**
    * horizMaxSpeed 
    * horizResistFactor 

.. cpp:function:: caseString PlayerData::imageAnimPrefix

    Optional prefix to all mounted image animation sequences in third person.

    This defines a prefix that will be added when looking up mounted image animation sequences while in third person. It allows for the customization of a third person image based on the type of player.

.. cpp:function:: caseString PlayerData::imageAnimPrefixFP

    Optional prefix to all mounted image animation sequences in first person.

    This defines a prefix that will be added when looking up mounted image animation sequences while in first person. It allows for the customization of a first person image based on the type of player.

.. cpp:function:: SFXTrack PlayerData::impactHardSound

    Sound to play after falling on a surface with Material footstepSoundId 1.

.. cpp:function:: SFXTrack PlayerData::impactMetalSound

    Sound to play after falling on a surface with Material footstepSoundId 2.

.. cpp:function:: SFXTrack PlayerData::impactSnowSound

    Sound to play after falling on a surface with Material footstepSoundId 3.

.. cpp:function:: SFXTrack PlayerData::impactSoftSound

    Sound to play after falling on a surface with Material footstepSoundId 0.
    
.. cpp:function:: SFXTrack PlayerData::impactWaterEasy

    Sound to play when entering the water with velocity < mediumSplashSoundVelocity.

    **See also:** mediumSplashSoundVelocity 

.. cpp:function:: SFXTrack PlayerData::impactWaterHard

    Sound to play when entering the water with velocity >= hardSplashSoundVelocity.

    **See also:** hardSplashSoundVelocity 

.. cpp:function:: SFXTrack PlayerData::impactWaterMedium

    Sound to play when entering the water with velocity >= mediumSplashSoundVelocity and < hardSplashSoundVelocity.

**See also:**
    * mediumSplashSoundVelocity 
    * hardSplashSoundVelocity 

.. cpp:function:: float PlayerData::jetJumpEnergyDrain

    Energy level drained each time the player jet jumps.

    **See also:** jetMinJumpEnergy
    
.. note:: Setting this to zero will disable any energy drain 

.. cpp:function:: float PlayerData::jetJumpForce

    Force used to accelerate the player when a jet jump is initiated.

.. cpp:function:: float PlayerData::jetJumpSurfaceAngle

    Angle from vertical (in degrees) where the player can jet jump.

.. cpp:function:: float PlayerData::jetMaxJumpSpeed

    Maximum vertical speed before the player can no longer jet jump.

.. cpp:function:: float PlayerData::jetMinJumpEnergy

    Minimum energy level required to jet jump.

    **See also:** jetJumpEnergyDrain 

.. cpp:function:: float PlayerData::jetMinJumpSpeed

    Minimum speed needed to jet jump.

    If the player's own z velocity is greater than this, then it is used to scale the jet jump speed, up to jetMaxJumpSpeed.

    **See also:** jetMaxJumpSpeed 

.. cpp:function:: int PlayerData::jumpDelay

    Delay time in number of ticks ticks between jumps.

.. cpp:function:: float PlayerData::jumpEnergyDrain

    Energy level drained each time the player jumps.

    **See also:** minJumpEnergy 

.. note:: Setting this to zero will disable any energy drain 

.. cpp:function:: float PlayerData::jumpForce

    Force used to accelerate the player when a jump is initiated.

.. cpp:function:: float PlayerData::jumpSurfaceAngle

    Angle from vertical (in degrees) where the player can jump.

.. cpp:function:: bool PlayerData::jumpTowardsNormal

    Controls the direction of the jump impulse.

    When false, jumps are always in the vertical (+Z) direction. When true jumps are in the direction of the ground normal so long as the player is not directly facing the surface. If the player is directly facing the surface, then they will jump straight up.

.. cpp:function:: float PlayerData::landSequenceTime

    Time of land sequence play back when using new recover system.

    If greater than 0 then the legacy fall recovery system will be bypassed in favour of just playing the player's land sequence. The time to recover from a fall then becomes this parameter's time and the land sequence's playback will be scaled to match.

    **See also:** transitionToLand 

.. cpp:function:: float PlayerData::maxBackwardSpeed

    Maximum backward speed when running.

.. cpp:function:: float PlayerData::maxCrouchBackwardSpeed

    Maximum backward speed when crouching.

.. cpp:function:: float PlayerData::maxCrouchForwardSpeed

    Maximum forward speed when crouching.

.. cpp:function:: float PlayerData::maxCrouchSideSpeed

    Maximum sideways speed when crouching.

.. cpp:function:: float PlayerData::maxForwardSpeed

    Maximum forward speed when running.

.. cpp:function:: float PlayerData::maxFreelookAngle

    Defines the maximum left and right angles (in radians) the player can look in freelook mode.

.. cpp:function:: float PlayerData::maxJumpSpeed

    Maximum vertical speed before the player can no longer jump.

.. cpp:function:: float PlayerData::maxLookAngle

    Highest angle (in radians) the player can look.

.. note:: An angle of zero is straight ahead, with positive up and negative down. 

.. cpp:function:: float PlayerData::maxProneBackwardSpeed

    Maximum backward speed when prone (laying down).

.. cpp:function:: float PlayerData::maxProneForwardSpeed

    Maximum forward speed when prone (laying down).

.. cpp:function:: float PlayerData::maxProneSideSpeed

    Maximum sideways speed when prone (laying down).

.. cpp:function:: float PlayerData::maxSideSpeed

    Maximum sideways speed when running.

.. cpp:function:: float PlayerData::maxSprintBackwardSpeed

    Maximum backward speed when sprinting.

.. cpp:function:: float PlayerData::maxSprintForwardSpeed

    Maximum forward speed when sprinting.

.. cpp:function:: float PlayerData::maxSprintSideSpeed

    Maximum sideways speed when sprinting.

.. cpp:function:: float PlayerData::maxStepHeight

    Maximum height the player can step up.

    The player will automatically step onto changes in ground height less than maxStepHeight. The player will collide with ground height changes greater than this.

.. cpp:function:: float PlayerData::maxTimeScale

    Maximum time scale for action animations.

    If an action animation has a defined ground frame, it is automatically scaled to match the player's ground velocity. This field limits the maximum time scale used even if the player's velocity exceeds it.

.. cpp:function:: float PlayerData::maxUnderwaterBackwardSpeed

    Maximum backward speed when underwater.

.. cpp:function:: float PlayerData::maxUnderwaterForwardSpeed

    Maximum forward speed when underwater.

.. cpp:function:: float PlayerData::maxUnderwaterSideSpeed

    Maximum sideways speed when underwater.

.. cpp:function:: float PlayerData::mediumSplashSoundVelocity

    Minimum velocity when entering the water for choosing between the impactWaterEasy and impactWaterMedium sounds to play.

**See also:**
    * impactWaterEasy 
    * impactWaterMedium 

.. cpp:function:: float PlayerData::minImpactSpeed

    Minimum impact speed to apply falling damage.

    This field also sets the minimum speed for the onImpact callback to be invoked.

    **See also:** ShapeBaseData::onImpact() 

.. cpp:function:: float PlayerData::minJumpEnergy

    Minimum energy level required to jump.

    **See also:** jumpEnergyDrain 

.. cpp:function:: float PlayerData::minJumpSpeed

    Minimum speed needed to jump.

    If the player's own z velocity is greater than this, then it is used to scale the jump speed, up to maxJumpSpeed.

    **See also:** maxJumpSpeed 

.. cpp:function:: float PlayerData::minLateralImpactSpeed

    Minimum impact speed to apply non-falling damage.

    This field also sets the minimum speed for the onLateralImpact callback to be invoked.

    **See also:** ShapeBaseData::onLateralImpact() 

.. cpp:function:: float PlayerData::minLookAngle

    Lowest angle (in radians) the player can look.

.. note:: An angle of zero is straight ahead, with positive up and negative down. 

.. cpp:function:: float PlayerData::minRunEnergy

    Minimum energy level required to run or swim.

    **See also:** runEnergyDrain 

.. cpp:function:: float PlayerData::minSprintEnergy

    Minimum energy level required to sprint.

    **See also:** sprintEnergyDrain 

.. cpp:function:: SFXTrack PlayerData::movingBubblesSound

    Sound to play when in water and coverage equals 1.0 (fully underwater).

    Note that unlike ``FootUnderwaterSound``, this sound plays even if the player is not moving around in the water.

.. cpp:function:: string PlayerData::physicsPlayerType

    Specifies the type of physics used by the player.

    This depends on the physics module used. An example is 'Capsule'.

.. note:: Not current used. 

.. cpp:function:: float PlayerData::pickupRadius

    Radius around the player to collide with Items in the scene (on server).

    Internally the pickupRadius is added to the larger side of the initial bounding box to determine the actual distance, to a maximum of 2 times the bounding box size. The initial bounding box is that used for the root pose, and therefore doesn't take into account the change in pose.

.. cpp:function:: Point3F PlayerData::proneBoundingBox

    Collision bounding box used when the player is prone (laying down).

    **See also:** boundingBox 

.. cpp:function:: float PlayerData::proneForce

    Force used to accelerate the player when prone (laying down).

.. cpp:function:: int PlayerData::recoverDelay

    Number of ticks for the player to recover from falling.

.. cpp:function:: float PlayerData::recoverRunForceScale

    Scale factor applied to runForce while in the recover state.

    This can be used to temporarily slow the player's movement after a fall, or prevent the player from moving at all if set to zero.

.. cpp:function:: bool PlayerData::renderFirstPerson

    Flag controlling whether to render the player shape in first person view.

.. cpp:function:: float PlayerData::runEnergyDrain

    Energy value drained each tick that the player is moving.

    The player will not be able to move when his energy falls below minRunEnergy.

    **See also:** minRunEnergy 

.. note:: Setting this to zero will disable any energy drain. 

.. cpp:function:: float PlayerData::runForce

    Force used to accelerate the player when running.

.. cpp:function:: float PlayerData::runSurfaceAngle

    Maximum angle from vertical (in degrees) the player can run up.

.. cpp:function:: filename PlayerData::shapeNameFP[4]

    File name of this player's shape that will be used in conjunction with the corresponding mounted image.

    These optional parameters correspond to each mounted image slot to indicate a shape that is rendered in addition to the mounted image shape. Typically these are a player's arms (or arm) that is animated along with the mounted image's state animation sequences.

.. cpp:function:: SplashData PlayerData::Splash

    SplashData datablock used to create splashes when the player moves through water.

.. cpp:function:: float PlayerData::splashAngle

    Maximum angle (in degrees) from pure vertical movement in water to generate splashes.

.. cpp:function:: ParticleEmitterData PlayerData::splashEmitter[3]

    Particle emitters used to generate splash particles.

.. cpp:function:: float PlayerData::splashFreqMod

    Multipled by speed to determine the number of splash particles to generate.

.. cpp:function:: float PlayerData::splashVelEpsilon

    Minimum speed to generate splash particles.

.. cpp:function:: float PlayerData::splashVelocity

    Minimum velocity when moving through water to generate splashes.

.. cpp:function:: bool PlayerData::sprintCanJump

    Can the player jump while sprinting.

.. cpp:function:: float PlayerData::sprintEnergyDrain

    Energy value drained each tick that the player is sprinting.

    The player will not be able to move when his energy falls below sprintEnergyDrain.

    **See also:** minSprintEnergy
    
.. note:: Setting this to zero will disable any energy drain. 


.. cpp:function:: float PlayerData::sprintForce

    Force used to accelerate the player when sprinting.

.. cpp:function:: float PlayerData::sprintPitchScale

    Amount to scale pitch motion while sprinting.

.. cpp:function:: float PlayerData::sprintStrafeScale

    Amount to scale strafing motion vector while sprinting.

.. cpp:function:: float PlayerData::sprintYawScale

    Amount to scale yaw motion while sprinting.

.. cpp:function:: Point3F PlayerData::swimBoundingBox

    Collision bounding box used when the player is swimming.

    **See also:** boundingBox 

.. cpp:function:: float PlayerData::swimForce

    Force used to accelerate the player when swimming.

.. cpp:function:: bool PlayerData::transitionToLand

    When going from a fall to a land, should we transition between the two.

    **See also:** landSequenceTime
    
.. note:: Only takes affect when landSequenceTime is greater than 0. 

.. cpp:function:: float PlayerData::upMaxSpeed

    Maximum upwards speed.

**See also:**
    * upResistSpeed 
    * upResistFactor

.. note:: This limit is only enforced if the player's upward speed exceeds upResistSpeed. 

.. cpp:function:: float PlayerData::upResistFactor

    Factor of resistence once upResistSpeed has been reached.

**See also:**
    * upMaxSpeed 
    * upResistSpeed 

.. cpp:function:: float PlayerData::upResistSpeed

    Upwards speed at which resistence will take place.

**See also:**
    * upMaxSpeed 
    * upResistFactor 

.. cpp:function:: SFXTrack PlayerData::waterBreathSound

    Sound to play when in water and coverage equals 1.0 (fully underwater).

    Note that unlike ``FootUnderwaterSound``, this sound plays even if the player is not moving around in the water.

