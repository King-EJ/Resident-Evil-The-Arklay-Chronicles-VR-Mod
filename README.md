RETAC VR  -  VR mod for "Resident Evil: The Arklay Chronicles"
=====================================================================================================

Version 0.1.0 (first test build, tested in a Quest 3 headset with Virtual Desltop).

WHAT IT DOES
------------
* Full stereo VR through OpenXR (SteamVR, Oculus/Meta, Virtual Desktop, WMR... any OpenXR runtime).
* Over-the-shoulder gameplay becomes first person: your eyes sit in the character's head, the
  head and arms are hidden, and the direction you look is the direction the character looks.
* The equipped weapon is moved into your VR hand. Shots, tracers and muzzle flashes come out of
  the gun you are holding, and the bullet goes where the controller points.
* A laser sight appears while you aim.
* Menus, inventory, files/notes, the HUD and in-game videos are shown on a floating screen.
  Point at it with the gun hand and pull the trigger to click.
* Cutscenes and the title screen: the view follows the game's camera.
* Snap turn or smooth turn, headset-relative or controller-relative movement, left-handed mode.
* Sound comes from your head position.
* Controller vibration when you shoot or take damage.

INSTALL
-------
1. Copy EVERYTHING in this zip [RETAC-VR-Mod](<https://github.com/King-EJ/Resident-Evil-The-Arklay-Chronicles-VR-Mod/releases/tag/Resident.Evil.The.Arklay.Chronicles>) into the RETAC game folder (the folder that contains the game's
   .exe and its "_Data" folder). You should end up with winhttp.dll and doorstop_config.ini
   next to the .exe, and a BepInEx folder beside them.
2. Start your OpenXR runtime (e.g. SteamVR) and make sure it is set as the ACTIVE OpenXR runtime.
3. Launch the game normally. It takes a few seconds for VR to start after the game window opens.
4. Keep the game window focused on the desktop (click it once if the controls stop responding).

GET THE GAME HERE: [Resident Evil The Arklay Chronicles](<https://gamejolt.com/games/retac/694117>)

To disable Mod: rename winhttp.dll to winhttp.dll.bak or  win http.dll  (or set enabled = false in doorstop_config.ini).

CONTROLS (right-handed default)
-------------------------------
Gun hand (right)
----------------
  Trigger ............ Shoot  /  click on the floating screen
  Grip (hold) ........ Aim (the game's Fire2)
  
  A .................. Interact / examine / confirm
  
  B .................. Reload  /  back in menus
  
  Stick left/right ... Smooth turn (120 degrees)
  
  Stick up/down ...... Navigate menus

Off hand (left)
---------------
  Stick .............. Move (forward = where you look)
  
  Trigger ............ Run
  
  Grip ............... Skip Menu (title screen)
  
  X .................. Inventory (Tab)
  
  Y .................. Next Weapon

Both stick clicks ..... Re-centre the view

All of this can be changed in:  BepInEx\config\retac.vr.cfg  (created after the first launch).
Bindings accept  btn:<Input Manager button>,  key:<Unity KeyCode>  and  mouse:<0|1|2>.
There are separate binding sets for gameplay and for menus/inventory.

SETTINGS WORTH KNOWING (retac.vr.cfg)
-------------------------------------
[General]  LeftHanded, SnapTurn, SnapTurnAngle, SmoothTurnSpeed, MovementDirection (Head/OffHand)

[Camera]   EyeHeightOffset, EyeForwardOffset, AnchorSmoothing (lower = less head bob),
           HideHead, CopyCameraEffects, DisableFlatCameraRendering, MirrorToDesktop
           
[Weapons]  WeaponInHand, HideArms, LaserSight (Aiming/Always/Off),
           WeaponPositionOffset / WeaponRotationOffset (to fine-tune how the gun sits in your hand),
           AimRotationOffset (the pointing direction of the controller), AutoAimWithTrigger
           
[UI]       Distance, Width, HeightOffset, FollowAngle

[General]  VerboseLogging = true  gives much more detail in the log when something is wrong.

TROUBLESHOOTING
---------------
* The log is BepInEx\LogOutput.log. Send that file along with any bug report.
* "OpenXR not ready": the headset/runtime wasn't running, or the active OpenXR runtime is wrong.
* Black or frozen headset: make sure the game runs on DirectX 11 (add -force-d3d11 to the launch
  options if you changed it).
* Gun held at a strange angle: adjust WeaponRotationOffset (e.g. "0,90,0" or "-90,0,0").
* Laser/bullets not going where the controller points: adjust AimRotationOffset
  (default "70,0,0"; try "40,0,0" or "90,0,0").
* A button does nothing: the game may use a different Input Manager name for it. Rebind it with
  key:<KeyCode> to the keyboard key the game uses instead.
* Low frame rate: lower the resolution in your VR runtime (e.g. SteamVR per-app resolution).
  The mod already stops the flat-screen camera from drawing the scene.

CHANGES
-------
0.2.3  Fixed BepInEx failing to start on some RETAC installs (the game ships an old .NET 2.0
       System.dll). A full System.dll is now provided in BepInEx\unstrip and doorstop_config.ini
       points to it.
0.2.2  [Cheats] UnlimitedHealth and UnlimitedAmmo (both off by default, work live).
0.2.1  Per character + weapon gun settings: the first time you hold a gun, a section like
       [Weapon.<Character>.<Weapon>] appears in retac.vr.cfg. Values set there override the
       [Weapons] ones for that combination only (empty = use [Weapons]).
       Better grip detection for first-person chapters.
0.2.0  Doors no longer switch to the fixed third-person camera ([Camera] StayFirstPersonAtDoors).
       Empty VR hands now use the character's own hands instead of coloured blocks
       ([Hands] HandModel = Character/Box/None, PositionOffset, RotationOffset, Scale - live).
0.1.9  New binding type scroll:up / scroll:down (mouse wheel; repeats while held).
0.1.8  Fixed the VR screen turning black after entering some rooms (the game's
       setClearFlagScript painted every camera's background black, including the UI one).
0.1.7  Fixed the VR screen turning black after a level loads (a finished intro video kept
       drawing its last frame on it). Videos are only shown while they play.
       Hold the off-hand stick click for 1 second to hide/show the VR screen.
0.1.6  Inventory: clicking items with the trigger now works.
       New [UI] FollowMode: Lazy (default), Head (locked to headset), GunHand (held above the
       gun-hand controller - point and click with the OTHER hand's trigger), OffHand.
       HandWidth / HandOffset size and place the hand-held screen.
0.1.5  Barrel direction now uses the weapon's real barrel axis (laser was tilted up/left).
       New LaserRotationOffset turns only the laser/bullets relative to the gun.
0.1.4  Laser and bullets now follow the gun barrel (LaserFollowsGun = true), so they always
       line up with the gun you see, whatever GunModelRotationOffset is set to.
0.1.3  New GunModelRotationOffset / GunModelPositionOffset: adjust the gun mesh in your hand
       without changing the aim (AimRotationOffset sets the laser/bullet direction).
0.1.2  Live config: save retac.vr.cfg while playing and the change applies within a second
       (aim/weapon offsets, laser, bindings, UI placement, eye offsets, turning...).
0.1.1  Gun now points forward (barrel direction is taken from grip to muzzle).
       Player body is invisible during gameplay (shadow kept) - new HideBody setting.
       View no longer lags behind the head when walking/running

Know Issues
-----------
Blood splash away from enemies

2 weapons laser not align good

CREDITS & LICENCES
------------------
* RETAC by Lord DeeJay.
* OpenXR.dll (the native OpenXR bridge) by Astien (c) 2025, from the [MousePI_VR](<https://discord.com/channels/1001138422972432597/1523984295633490031/1541072649634189372>) mod. It is
  redistributed here under its "Free Redistribution or Modification, No Commercial Use" licence.
  See BepInEx\plugins\RetacVR\LICENSES. This mod and its bridge must stay free of charge.
* The rig/UI/input approach follows Astien's VRMod framework design.
* BepInEx - LGPL 2.1 (https://github.com/BepInEx/BepInEx).
* This is a fan-made, non-commercial mod.
