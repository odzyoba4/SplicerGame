# Splicer
3D Unity first-person street brawler game created with a team of 5 developers. 
<br>
[Game Website](https://frigid-vtx.itch.io/splicers) 
<br>

## Overview
I took the role of programmer in this 5-person class project, during which I learned to develop game systems using the Unity engine.
I worked with the player mechanics and movement, the UI/HUD, saving/level progression, and enemies. During this time, I learned more about the C# language, particularly about event-driven architecture.
<br/>

## Player Input & Controller Support
One of my most robust systems was the player input, which was recognized with Unity's new input system. 
<br>
A large challenge was displaying the correct binding on-screen based on whether a controller or a mouse/keyboard was being used, and allowing the user to switch seamlessly. I wanted to avoid at all costs checking for such a change every frame. Instead, I made all necessary HUD elements inherit from an abstract class, which subscribed to an event on initialization that would be invoked as soon as a player switched input types:
<br>
| ![Buttom Prompt example](/images/buttonPromptExample.png) | ![Buttom Prompt example](/images/swappableUIExample.png)|
| -------------------------------- | ----------------------------------------|

<br>
This way, any button prompt on the screen would instantly update itself without much overhead.
<br/> 

|![Keyboard Input Prompt](/images/keyboardInputExample.png) |![Controller Input Prompt](/images/controllerInputExample.png) |
| -------------------------------- | -----------------------------------------|

<br/>


## Debugging Tools
For our game's enemies, I encountered challenges debugging Unity's NavMesh system. There were constant issues with enemy pathing, and I realized that monitoring variables in my code alone
was slowing me down. I decided to create a line renderer debug tool to help me visually track what was happening in-game and better understand where my code was going wrong.
<br>
<br>
Because this tool was for development only, and would not be in the final build, I wanted a way to easily add lines without causing conflicts if the tool was turned off or removed. 
So, I made a singleton class that owned multiple line renderers, which would only activate when some other class wanted to draw a line during the game update.
```C#
public class DebugLineRenderer : MonoBehaviour
{
    [SerializeField] private List<LineRenderer> lines;
    private List<bool> availableLines;
    public static DebugLineRenderer Instance { get; private set; } //singleton access

    public static void DrawLine(Vector3 startPos, Vector3 endPos)
    {
        if (Instance != null)
        {
            for (int i = 0; i < Instance.lines.Count; i++)
            {
                if (Instance.availableLines[i]) //if this line is not being drawn currently
                {
                    //set line parameters
                    Instance.lines[i].SetPosition(0, startPos);
                    Instance.lines[i].SetPosition(1, endPos);
                    //set availability to false so other calls to DrawLine do not alter this line
                    Instance.availableLines[i] = false;
                    return;
                }
            }
            //all slots were full if reaching this point
            Debug.LogError("DebugLineRenderer: Limit exceeded. To draw this line, increase Lines size");
        }
    }

    // ... //

```
This visual addition helped me resolve numerous issues with our enemies but was also a great general-use tool for tracking movement mid-game.
<br>
<br>
![Debug Line Renderer](/images/enemyDebugExample.png)
