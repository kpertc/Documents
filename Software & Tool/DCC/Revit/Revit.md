`WA` wall
直接输入数字 设置长度

hold `shift` draw wall orthogonal line (vertical & Horizontal)

Properties:
Location Line

选择
左上 右下
右下 左上

单位设置
project unit
`UN`

zoom the view to change snap settings
manage > snaps

建筑 结构 机电

项目 Project
族 Family
图元

![[revit-option.png|400]]

3D view
![[revit-3Dview.png]]

close Hidden Window

![[revit-property-projectBrowser.gif]]

### Development
[Revit API](https://aps.autodesk.com/developer/overview/revit)

##### add-in Manager
RevitSDK includes add-in Manager [Revit SDK 及LookUp 各版本下载地址](https://blog.csdn.net/weixin_46433786/article/details/115633252)
> Copy `AddInManager.dll` & `Autodesk.AddInManager.addin` to `%appdata%/autodesk/revit/addins`
> [Install add-in Manager](https://tailoryourbim.com/revitexternalcommand/use-add-in-manager-from-autodesk/)

##### Revit LookUp
https://github.com/jeremytammik/RevitLookup/
[Revit Lookup for 2018 and the Revit 2018 SDK](https://wrw.is/httpwhatrevitwants-blogspot-com201704revitlookup-for-2018-and-revit-2018-sdk-html/)
[[compiled 2018]]

https://www.youtube.com/watch?v=MSGSrk4kWgY

Type of Revit Add-in
- command
- application

VSCode reference:
`RevitAPI.dll`
`RevitAPIUI.dll`


addin file
- .dll
- .addin manifest


