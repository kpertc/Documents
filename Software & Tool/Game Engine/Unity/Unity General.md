#C＃ #Unity 

### Shortcut

https://docs.unity3d.com/2022.1/Documentation/Manual/UnityHotkeys.html

shortcut|function
---|---
Z|Center / Pivot
X|Local / World
Ctrl F|Search
Ctrl Shift N|Create Empty GameObject
Alt Shift N|Create Empty GameObject as a child of selected object
Ctrl Shift F|Camera align
Ctrl "Num"|Open / Create window
Ctrl B|Build
Ctrl P|Play
Ctrl Shift P|Pause
Ctrl Alt P|Step / Play frame by frame

<br/>

Slider
Hold shift faster
Hold Alt slower

<br/>

### Transform

Transform 不能被实例化

object space to world space -> [Transform](https://docs.unity3d.com/ScriptReference/Transform.html).TransformPoint

Transform.SetPositionAndRotationn

<br/>

  

### Color Pick create Swatches library
![[img/Unity-General-img/Color Pick create Swatches library.png | 500]]

  

### Unity Event accepts Input
![[img/Unity-General-img/Unity Event accepts Input-1.png]]|![[img/Unity-General-img/Unity Event accepts Input-2.png]]
---|---

<br/>

### Update() FixUpdate() LateUpdate()

-   Update() called everyframe -> framerate dependent
    
-   FixUpdate() called before Update() Not framerate dependent
    
    -   `Project Setting` -> `Time`
        
    -   good for physics calculation and movement
        
-   LateUpdate() is called after every Update() -> framerate dependent
    
    -   good for camera calculation (called when the gameobject finish it's Update())

<br/>


  

### [Coroutine](https://docs.unity3d.com/Manual/Coroutines.html), IEnumerator, yield -> Unity MonoBehavior

A Coroutine is like a function that has the ability to pause execution and return control to Unity but then to continue where it left off on the following frame.

Return

<br/>


### Async -> C#

<br/>

### Logging

-   Type of logging
    
-   Style of logging [rich text](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/StyledText.html) formatting   

![[img/Unity-General-img/rich-text-log.png]]

<br>

### Mesh Generation

<br>

### Unit Test

`Window` -> `General` -> `Test Runner`

Edit Mode / Play Mode

Create a folder

  

NUnit.Framework

Assert

`Test`

`UnityTest`

<br>

### Screenshot, texture saving and loading

```C#
//Save Texture to file thru Bytes
Camera selfieCam = _camera;

Texture2D snapShot = new Texture2D(resWidth, resHeight, TextureFormat.RGBA32, false);
selfieCam.Render();
RenderTexture.active = _rd;
snapShot.ReadPixels(new Rect(0, 0, resWidth, resHeight), 0, 0);
byte[] bytes = snapShot.EncodeToPNG();

if (!Directory.Exists(path))
    Directory.CreateDirectory(path);

string fileName = path + screenShotName + ".png";
System.IO.File.WriteAllBytes(fileName, bytes);
```

```C#
//Load Texture2D from Bytes
// new texture2D for temp stored the screenshot
Texture2D screenShot = new Texture2D(resWidth, resHeight);
screenShot.LoadImage(bytes);

// ScreenShot Show
screenShotPic_Mat.SetTexture("_MainTex", screenShot);
```