GameTSCtrl
==========

The main 3D viewport for a Torque 3D game.

Inherit:
	:doc:`GuiTSCtrl`

Description
-----------

The main 3D viewport for a Torque 3D game.

With the exception of a few very niche genres, the bulk of your 3D game viewing will occur in a GameTSCtrl. You typically only need a single GameTSCtrl, unless you are implementing a very complex interface system. In the demos, you can find our example named "PlayGui".

It is recommended that any game GUIs that are not pushed and popped constantly, be contained within your GameTSCtrl. Examples include targeting reticle, standard healthbar, ammo count, etc. This is mostly a design decision, but the way Torque 3D's GUI system works somewhat encourages you to group the controls in this manner::

    // Example of a GameTSCtrl
    // PlayGui is the main TSControl through which the game is viewed
    // Also contains a Guis for:
    // - A lag icon
    // - Showing other shape names
    // - Crossahir
    %guiContent = new GameTSCtrl(PlayGui)
    {
      cameraZRot = "0";
      forceFOV = "0";
      reflectPriority = "1";
      Profile = "GuiContentProfile";
      HorizSizing = "right";
      VertSizing = "bottom";
      position = "0 0";
      Extent = "1024 768";
      
      new GuiBitmapCtrl(LagIcon)
      {
         bitmap = "art/gui/lagIcon.png";
         // Note: Rest of fields hidden for this example
      };
   
      new GuiShapeNameHud()
      {
         fillColor = "0 0 0 0.25";
         frameColor = "0 1 0 1";
         textColor = "0 1 0 1";
         showFill = "0";
         showFrame = "0";
      
         // Note: Rest of fields hidden for this example
      };
      
      new GuiCrossHairHud(Reticle)
      {
         damageFillColor = "0 1 0 1";
         damageFrameColor = "1 0.6 0 1";
         damageRect = "50 4";
         damageOffset = "0 10";
         bitmap = "art/gui/weaponHud/blank.png";
         // Note: Rest of fields hidden for this example
      };
    };