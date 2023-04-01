#Unity #VR

### 资源

[XR 学习](https://bytedance.feishu.cn/docs/doccnY8PDwgOKvorAAvqWHEk1Fe#5Wio1C)
[Oculus VR 设计指南](https://bytedance.feishu.cn/docx/doxcnnvTftIKR86bVNHBHCWOLTf)

<br>

### VR General

[Unity Intergration SDK](https://developer.oculus.com/downloads/unity/) 可以通过Unity Asset Store


![[img/Unity VR img/immersion-navigation-interaction.png | 300]]

<br>

> [!info] 
> 由于VR环境不好测试 使用Gameobject onEnable作为按钮方便进行测试

<br>

### Pico

Build for Pico, Android (26) later
[adb 的安装与使用](https://bytedance.feishu.cn/wiki/wikcnDH1ELzIyxFxEWqtqiSManh#qxouGl)
[VS for Mac调试Pico(Android)下的Unity C#脚本](https://bytedance.feishu.cn/docx/doxcnAO9xvysEKoxLF6h7c54u6b)

<br>

### Unity

XR Plugin

<br>

XR
https://docs.unity3d.com/Manual/xr_input.html
https://docs.unity3d.com/560/Documentation/Manual/OpenVRControllers.html
VR Controller Input Binding Layout

![[img/Unity VR img/VR Controller.png]]
  

### Unity Input System (Unity 2019+)

> [!info]  **[InputSystem Documentation](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.3/manual/QuickStartGuide.html)**
>- [Meet the Devs: Input System | Unite Now 2020](https://www.youtube.com/watch?v=gVus9PqfgAM)
>- [Input System: Workflow tips and feature integrations | Unite Now 2020](https://www.youtube.com/watch?v=xF2zUOfPyg8)

##### Switch Input System `Project Settings -> Player -> Configuration -> Active Input Handing`

> [!info] 
>Old 🠒 UnityEngine.Input;
>New 🠒 UnityEngine.InputSystem;

![[img/Unity VR img/player-inputsystem.png]]
  
![[img/Unity VR img/player-input.png]]

<br>

API
`using UnityEngine.InputSystem;`
```C#
读取整个 InputActionAsset
public InputActionAsset _InputActionAsset; //Create "Input Action" Asset in Unity First

InputAction A_Button;

void Start()
{
    A_Button = _InputActionAsset.FindAction("A_Button");
    A_Button.performed += (InputAction.CallbackContext _ctx) => Debug.Log("A_Button Pressed!");
    A_Button.Enable();
}

读取单个 InputActionProperty  Unity Action-Based Input
public InputActionProperty triggerProperty;
public InputAction _triggered;

void OnEnable() {
    _triggered = triggerProperty.action;
    _triggered.performed += (InputAction.CallbackContext callbackContext) => takeSelfie();
    _triggered.Enable();
}

读取Vector2
input = callbackContext.ReadValue<Vector2>(); 
```

##### [Debugging](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.3/manual/Debugging.html) `Window -> Analysis -> Input Debugger`

### Haptics 震动反馈

```C#
// unity XR
List<UnityEngine.XR.InputDevice> devices = new List<UnityEngine.XR.InputDevice>();

UnityEngine.XR.InputDevices.GetDevicesWithRole(UnityEngine.XR.InputDeviceRole.RightHanded, devices);

foreach (var device in devices)
{
    UnityEngine.XR.HapticCapabilities capabilities;
    if (device.TryGetHapticCapabilities(out capabilities)) {
        if (capabilities.supportsImpulse) {
            device.SendHapticImpulse(0, amplitude, duration);
        }
    }
}

// OVR
OVRInput.SetControllerVibration(frequency, amplitude, OVRInput.Controller.RTouch);
```

<br>

### OVR

Hand

Put ”OVRCustomHandPrefab_L“ and ”OVRCustomHandPrefab_R“

OVRPlayerController / OVRCameraRig / TrackingSpace / LeftHandAnchor and RightHandAnchor


<br>


### Unity XR Interaction Toolkit

Unity Demo https://github.com/Unity-Technologies/XR-Interaction-Toolkit-Examples

<br>  

##### XR-Rig (Action Base), no offset (recommend)

Add `Input Action Manager`

<br>  

##### Grab

XR Grab Interactable

<br>  

##### Teleport

-   Add `Locomotion System`
    
-   Add `Teleportation Anchor` or `Teleportaton Area`

<br>  

##### UI Interaction by Ray Interactor https://www.youtube.com/watch?v=BZt74PVb7sM

-   Canvas `Render Mode` -> `World Space` // 缩放 0.002
-   Canvas add `Tracked Device Graphic Raycaster`
-   Event System add `XRUI Input Module`