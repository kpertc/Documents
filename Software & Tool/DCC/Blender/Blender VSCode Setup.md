[5 Steps to setup VSCode for Blender Python (on macOS)](https://youtu.be/_0srGXAzBZE?si=rRnpWQ_B4qzoQlnF)
[fake-bpy-module](https://github.com/nutti/fake-bpy-module)

```shell
pip install fake-bpy-module-latest
```

![[fake-bpy-vscode.gif]]

VSCode Plugin: Blender Development by Jacques Lucke
![[blender-development-vscode-plugin.png]]

VSCode command
![[blender-commands.png]]

Blender: Start
Blender: Run

![[Blender-start-run.gif]]

Support VSCode Debug breakpoint

> [!failure] Error
PermissionError: [Errno 1] Operation not permitted
Grant Full Disk Access permissions for the terminal or VSCode if terminal running in VSCode

`__name__` is not `__main__` if run from Blender Development plugin
```python
if __name__ == "<run_path>":
```