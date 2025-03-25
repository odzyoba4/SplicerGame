# Splicer
3D Unity first-person street brawler game created with a team of 5 developers. <br>
[Game Website](https://frigid-vtx.itch.io/splicers) <br></br>

## Overview
I took the role of programmer in this 5-person team project, during which I learned to develop game systems using the Unity engine.
I worked with the player mechanics and movement, the UI/HUD, saving/level progression, and enemies.

One of my most robust systems was the player input, which was recognized with Unity's new input system. During this time, I learned more about the C# language, particularly about event-driven architecture.
A large challenge with player input was displaying the correct binding on-screen based on whether a controller or a mouse/keyboard was being used.<br/>

GameController Class Diagram:
![CentipedeGameFlow](/images/CentipedeGameFlow.png)

## Finite State Machine (Centipede)
One of the systems I implemented was the main centipede's movement. To do this, I used a finite state machine to create static state classes to decide between actions that the centipede took when going in a zig-zag motion.
<br/> 

Class Diagram: <br/>
![CentipedeGameFlow](/images/CentipedeFSM.png)

<br/>
The state machine helped me create a more computationally efficient update method for the centipede, which only checked the necessary data for the state that it was in, and also made graphical updates to the sprites easier.

## Command Pattern (Sound Manager)
Another pattern I learned to implement was the command pattern, which I used to create the centralized sound manager for the game. With the command pattern, I could avoid too many sounds combining at once by having a sound manager that would accept commands to play and stop a sound. 
This way, a sound was played only once per frame, even if multiple objects called to play the sound. <br>
![CentipedeSoundManager](/images/CentipedeSound.png)
