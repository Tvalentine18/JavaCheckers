# 2D Game Engine
A game engine intended to by used for a top-down twin stick shooter.  
[Dev Ops](https://www.gamasutra.com/blogs/MichaelKissner/20151027/257369/Writing_a_Game_Engine_from_Scratch__Part_1_Messaging.php)

## Branches
Master will contain a universal engine that's implementation is written in OpenGL in C++.  
I'm planning on making a branch that operates in Vulkan.

## Features
List of features and design decisions and notes.  
The following notes are derived from 
[this](https://www.gamedev.net/articles/programming/general-and-gameplay-programming/making-a-game-engine-core-design-principles-r3210/) 
article. Other articles are cited in-line below.

### Game Loop
Updates the game and then draws a frame, repeat. Should regulate the frame rate to match the refresh
rate of the monitor (like G-Sync).  
[Game Loop](https://gafferongames.com/post/fix_your_timestep/ "Game Loop")  

### Scene
The Scene manages all of the game objects Receives updates/draw messages and alerts the components 
attached to game objects in the scene. Probably going to be an observer pattern. See the design
documents folder (whenever I get to making it) for furthur details.

### Renderer
The renderer needs to decide which game objects need to be computed during a screen update. Some seem to
use a concept called **layers** which will let objects know if they need to be redrawn. For a 2D engine
this should be a little easier.

### Collision Detection
Collision detection seems like it has a lot of tradeoffs to consider. Using a circle makes it fairly
easy to detect collisions but gives back false positives for collisions if the object it is representing
is not circular or spherical by nature. Using other polygons makes the collisions detected more accurate
but seems computationally expensive.  

### Game Object
Contains a bunch of components. Some components are the **object's transformation**, **the renderer**,
**physics**, and **game logic**. Game objects can also hold a reference back to the scene so it can
query scene information. For instance, determining if the player is visible to an enemy.
 
