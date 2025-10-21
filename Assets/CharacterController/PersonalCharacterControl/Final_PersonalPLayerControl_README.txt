<<--- Development Notes for [Final_PersonalPlayerControl_README] --->>

---------------------------------------------------------------------------
Date: 20/10/2025
---------------------------------------------------------------------------
Overview:
---------
- This is README notes of how I created my [PersonalCharacterController] by reference from various Character Controllers seen in YouTube Video. There are also some improvement or tweaks I made using my own ideas.

- Each Implementations of Call-Function structure is mainly reference from other Character Controllers. Here is where I will note where I got the reference from and why I decide to use them.

===========================================================================
[PlayerInputHandler]_Script
===========================================================================

Reference From:
---------------
2. [CharacterControl2]_Script -> [PlayerController]_Script -> [InputManagement()]_Function  
3. [PersonalEdit]_ChatGPT

Overview:
---------
- Serves as the base [InputManagement] for [PersonalCharacterControl].

- Calling for inputs made from the Player from mouse inputs to key inputs.

From [CharacterControl2]
------------------------
- Use this function as a base template
     - This method is simple and compact.  
     - All input code is in one place, which makes it easier to manage.  

From [PersonalEdit]
-------------------
- [Input.GetAxis] change to [Input.GetAxisRaw]
	- Precise snappy Movement instead of smooth ramping Movement.
	- Rename variables to match other [CharacterController] reference.

- Seperate the [InputHandler] Function into a entirely new Script
	- A seperate script that handles all input reading and distribution.
	- Putting everything into one script will be very long. (over ~1000 lines and not-readable, hell scroll.)

- Debugging made easier
	- When something breaks, you know where to look.
	- If everything were in one file, debugging becomes a maze.

- Call Functions hasn't slow down due to calling for variables from different scripts.
	- separating your logic into multiple scripts does not make any measurable performance difference.

===========================================================================
[FirstPlayerCam]_Script
===========================================================================
Reference From:
---------------
1. [CameraController_README]

Overview:
---------
- Implements the [First-Person-Perspective] camera system for [PersonalCharacterControl].

- All development notes, version history, and prototype testing are fully documented in [CameraController_README].

- This script focuses on handling camera rotation, mouse input, and synchronization between Player visuals and view direction.

From [CharacterControl1]
------------------------
- Restructure a hierarchy to define a stable parent-child structure. 
 
PlayerRoot (Rigidbody, position 0,0,0, no rotation)
 └─ PlayerMesh (your mesh/visuals, rotates for camera)
     └─ Camera (Virtual Camera, rotates vertically)

- Based on [GetAxisRaw] mouse input for responsive and unsmoothed camera rotation.  

- Utilizes [xRotation] and [yRotation] variables to manage vertical and horizontal angles with clamped camera control.

From [CharacterControl2]
------------------------
- Adapted compatibility for [Cinemachine VirtualCamera] to support both first and third-person perspectives. 

From [PersonalEdit]
-------------------
- Established separation between [CameraController] and [InputManagement] functions for cleaner modular design.  

- Implemented [Parent-Child] transform handling to prevent physics flickering and maintain stable camera tracking. 


===========================================================================
[PlayerMovement]_Script
===========================================================================
Overview:
---------
- Implement [ResetPlayerState()] to reset's Player’s [Transform.Position] before gameplay begins.

From [PersonalEdit]
-------------------
- Integrated [spawnPosition] and [ResetPlayerState()] system for safe and flexible Player initialization during testing.
