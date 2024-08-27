![[open-blueprint.png]]


### Blueprints

- Print String

<br>

- Set Actor Location
- Get Actor Location

- Add Relative Location

hide / unhide object
- Set Visibility 
- Set Actor Hidden in Game
	- Set Actor Enable Collision

Play Sound 2D
Play Sound at Location

<br>

- Delay (`D` + LMB)
	- can not be added in function
	- Calling again while it is counting down will be ignored.
- Retriggerable Delay

- Set Timer by Event
- Set Timer by Function Name

<br>

- Add(`+`)

- Branch (if condition)

<br>

### Variables

Create Variable (Left)|Variable Details (Right)
--|--
![[variable.png]]|![[variable details.png]]
Drag to blueprint<br>Ctrl drag -> Get<br>Alt drag -> Set|

Split / Recombine
![[split&recombine.gif]]


<br/>

Event Graph

Add Event

Add Event from component|Event Trigger to print text
---|---
![[collision-test-1.png]]|![[collision-test-2.png]]

<br/>

Event Tick (Frame Dependent)
	- Delta Seconds (Frame Independent)

Custom Event

Create custom event|Trigger custom event
---|---
![[create-custom-event.png]]|![[trigger-custom-event.png]]


Collapse to function
![[collapse-to-function.png]]


Double click to create re-route
![[double-click-reroutel.gif]]

Shift F1 Mouse Control

Split vec3 to 3 float
![[split-struct.gif]]
