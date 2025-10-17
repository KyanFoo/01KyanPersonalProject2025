<<--- Development Notes for [PersonalCharacterControl] README --->>

---------------------------------------------------------------------------
Date: 14/10/2025
---------------------------------------------------------------------------

Reference From:
---------------
1. [CharacterControl1]_Script -> [PlayerCam]_Script  
2. [CharacterControl2]_Script -> [PlayerController]_Script -> [Turn()]_Function  
3. [PersonalEdit]_ChatGPT

===========================================================================
[CameraController1]_Script
===========================================================================

[Overview]
----------
- Serves as the base code for [PersonalCharacterControl].

- Combining references from [CharacterControls] into one unified prototype aligned with my design goals.

From [CharacterControl1]
------------------------
- Gather [Mouse Input] using [GetAxisRaw].

- Calculate [Rotation] values for [xRotation] and [yRotation]. 
	- Clamp [xRotation] to simulate the natural head rotation limit of a human.

- Rotate both [PlayerMesh] and [Camera] to ensure synchronized and consistent facing direction.

From [CharacterControl2]
------------------------
- Compatible with [Cinemachine]'s [VirtualCamera].  
	- Intended for use with [Third-Person-Perspective] in [PersonalCharacterControl].  
	- Benefits from using [VirtualCamera]'s built-in camera controls within the [Inspector].
	- Reducing the need to build a fully custom camera system.
	  
From [PersonalEdit]
---------------------
- Rotate the variable's [Transform.Rotation] rather than the entire Player.  
	- Use [playerBody.rotation] instead of [transform.rotation].  
	- Prevents unwanted rotation of the Player when applying [yRotation].

[Issue Observed (X)]:
- When applying [CameraMovement], the Player's [Transform.Position] flickers.
	- This occurs in most reference [CharacterControl] implementations.

[Solution (O)]:
- Use a parent GameObject structure.
	- Keep the Rigidbody parent object fixed at (0,0,0) with no rotation (handles physics).
 	- Create a child GameObject (mesh/visuals) that handles rotation for visuals and camera alignment.

From [Problem Errors]
---------------------
- When [CameraMovement] is applied, the Player’s [Transform.Position] correctly stays at (0,0,0). 
 
- However, when spawning the Player above floor level:
	- [Transform.Position] is not numerically (0,0,0), despite appearing correctly aligned.  
	- This causes the Player to appear "below zero" even when visually positioned on the floor.
 
===========================================================================
[CameraController2]_Script
===========================================================================

From [PersonalEdit]
-------------------
[Issue Observed (X)]:
- Forcibly resetting the Player’s [Transform.Position] to (0,0,0) is generally unsafe.
- As directly modifying the transform can cause flickering.
	- However, it is acceptable when executed before gameplay begins (e.g., during initialization or spawn setup).
	- 
[Solution (O)]:  
- Create [ResetPlayerState()]_Function
	- Pressing [SpaceKey] resets the Player’s [Transform.Position] to (0,0,0) after spawning from a height.

From [Problem Errors]
---------------------
- This method works effectively for prototype testing.

- However, using a [Key Press] trigger (e.g., [SpaceKey]) for reset functionality is not suitable for final gameplay implementation.


===========================================================================
[CameraController3]_Script
===========================================================================

From [PersonalEdit]
-------------------
[Issue Observed (X)]:
- Resetting the [Transform.Position] should be handled cleanly and occur without interfering with gameplay flow.

[Solution (O)]: 
- Implement a proper Spawn System
	- Introduce a variable [Vector3 spawnPosition] to represent the Player’s designated spawn point.
	- This allows controlled spawning at various locations, such as the center of a plane, a mountain top, or a building’s upper floor.

From [Problem Errors]
---------------------
- The automatic reset of the Player’s [Transform.Position] has not yet been implemented.  
- The necessary functions are already in place; they only need to be properly linked to complete the system.