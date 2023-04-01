[[Unreal Engine Windows]]

[[Unreal Engine Level Design]]

[[Unreal Engine Blueprints]]

[[Unreal Engine C++ Game Framework]]
[[Unreal Engine Console]]

<br>

> [!tip]- C++ Install components via Visual Studio Installer
> Workloads:
>		- .NET desktop development
>		- Desktop development with C++	
>		- Game Development with C++
>	
>	Individuals components:
>		- .Net Core 3.1

<br>


`UObject` → The parent class for all other Unreal Engine Classes
Can not be placed in scene

`Actor` →  any object that can be placed into a level, such as a Camera, static mesh, or player start location

	UObject	
		↳ Actor Class → can be spawn 
			↳ Pawn Class → can receive input
				 ↳ Character Class

	Actor Component Class
	↳ Game Mode Class
	↳ Player Controller Class

<br>

### Change Quality
Settings > Engine Scalability Settings
Adjust Performance ↔ Quality

<br>

### Default Maps
Maps & Modes → Default Maps
The map show up when the UE open