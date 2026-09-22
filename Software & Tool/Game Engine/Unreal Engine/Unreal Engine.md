[[Unreal Engine Windows]]
[[Unreal Engine Material]]
[[Unreal Engine Level Design]]
[[Unreal Engine Blueprints]]
[[Unreal Engine Movie Render]]

Programming
[[Unreal Engine Python]]
[[Unreal Engine C++ Game Framework]]
[[Unreal Engine Console]]

> [!tip]- C++ Install components via Visual Studio Installer
> Workloads:
>		- .NET desktop development
>		- Desktop development with C++	
>		- Game Development with C++
>	
>	Individuals components:
>		- .NET runtime per UE version (.NET Core 3.1 is EOL)
>		- Unreal Engine installer

`UObject` → The parent class for all other Unreal Engine Classes
Can not be placed in scene

`Actor` →  any object that can be placed into a level, such as a Camera, static mesh, or player start location

	UObject	
		↳ Actor Class → can be spawn 
			↳ Pawn Class → can receive input
				 ↳ Character Class
			↳ Info Class
				 ↳ Game Mode Class
			↳ Controller Class
				 ↳ Player Controller Class
		↳ Actor Component Class → not an Actor, attached to Actors
			↳ Scene Component Class
				 ↳ Primitive Component Class
### Change Quality
Settings > Engine Scalability Settings
Adjust Performance ↔ Quality

### Default Maps
Maps & Modes → Default Maps
The map show up when the UE open

### Enable Nanite
DX12 enabled required

Method 1|Method 2
---|---
![[nanite-method-1.png]]|![[nanite-method-2.png]]

Nanite View
![[nanite-view.png|300]]