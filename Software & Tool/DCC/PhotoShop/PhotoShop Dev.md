#JavaScript #TypeScript 

## CEP vs UXP
CEP UXP 是开发框架, PhotoShop API才是具体给PhotoShop的指令

CEP (Common Extensibility Platform) 是旧的PS开发框架 → 内嵌浏览器, node.js (ECMAScript 3 标准)
- https://github.com/Adobe-CEP
- https://github.com/Adobe-CEP/Getting-Started-guides

官方UXP对CEP的说明: [developer.adobe.com](https://developer.adobe.com/photoshop/uxp/2022/guides/uxp_for_you/uxp_for_cep_devs/#:~:text=UXP%20comes%20with%20a%20plugin,the%20same%20across%20CC%20applications)

---
### 介绍UXP
UXP API - https://developer.adobe.com/photoshop/uxp/2022/uxp-api/
Samples https://developer.adobe.com/photoshop/uxp/2022/guides/code_samples/
  ↳ https://github.com/AdobeDocs/uxp-photoshop-plugin-samples
  
UXP (Unified Extensibility Platform) 是Adobe开发的新框架, 相对于旧框架, UXP使用现代版本的JavaScript, 支持ES6的语法. UXP的功能包括插件 / 界面 / 网络请求等框架功能. (PhotoShop核心功能 → PhotoShop API)

![[PhotoShop-UXP-Architecture.png]]
UXP Architecture from [Photoshop Plugins With UXP: Introduction by FRANCESCO CAMARLINGHI](https://minifloppy.it/blog/2023/photoshop-plugins-with-uxp-introduction/)

---
### UXP Script 脚本
- `.psjs` - 可直接给PhotoShop运行
    
- [UXP Script - Overview](https://developer.adobe.com/photoshop/uxp/2022/scripting/)
- [How it works](https://developer.adobe.com/photoshop/uxp/2022/scripting/how-it-works/)
---
### 创建UXP Plugin 插件

开发UXP有两种选项:
- 一个完整带UI的工具: UXP Developer Tools (UDT)
- CLI工具: UXP Devtools-cli

### UDT, UXP Developer Tools

### Install UXP Developer Tools by Creative Cloud
https://developer.adobe.com/photoshop/uxp/2022/guides/getting-started/creating-your-first-plugin/

Install UXP Developer Tools
https://developer.adobe.com/photoshop/uxp/2022/guides/devtool/installation/

### Create Plugin

	![[PhotoShop-UXP-CreatePlugin.png|300]]
	
![[PhotoShop-checkVersion-1.png]]|![[PhotoShop-checkVersion-2.png]]
---|---
### Turn on Dev Mode in PhotoShop
| ![[PhotoShop-devMode-1.png]] | ![[PhotoShop-devMode-2.png]] |
| ---- | ---- |
### Load Plugin
![[PhotoShop-loadPlugin-1.png]]
![[PhotoShop-loadPlugin-2.png]]

### Add Plugin
> click "Add Plugin...", and navigate to the "manifest.json" file in this folder.

![[PhotoShop-uxp-addPlugin-1.png]]
![[PhotoShop-uxp-addPlugin-2.png]]


在UXP工具中Add Plugin然后打开对应插件的`manifest.json`
### Debugging
![[PhotoShop-uxp-debugging-1.png]]

![[PhotoShop-uxp-debugging-2.gif]]


UDT带有一个Playground
![[PhotoShop-UDT-Playground.png|300]]

---
### UXP Devtools-cli
💡 无需打开UXP Developer Tool, 在Terminal中进行开发交互
插件主仓: https://github.com/adobe-uxp/devtools-cli/tree/main
安装说明: https://github.com/adobe-uxp/devtools-cli/blob/main/packages/uxp-devtools-cli/README.md

在插件目录下执行
1. 连接 `uxp service start`
	![[PhotoShop-uxp-service-start.png|500]]
2. 新开一个terminal来执行其他操作

如果通过webpack等编译出来的, 先`cd`到编译后的目录, 包含有`manifest.json`
1. `uxp plugin load`
2. `uxp plugin reload`
3. `uxp plugin debug`
---
### 导出/发行 Distributing

![[PhotoShop-uxp-package.png]]
Package → 导出文件格式 `.ccx`
安装/使用: 双击`.ccx` - UXP打开 (未经过Maket验证的插件会有提示)
🔴 `.ccx`格式是重命名版的zip文件, 将`.ccx`文件重命名为`.zip`后 可以直接打开, 内容不加密

> 教程: [[YouTube] Distributing UXP plugins by NT Productions](https://youtu.be/eX4DkjDmJ0Q?si=T9hUy0XLnHLsHCu9)

---
## 开发参考

[UXP Get Started](https://kihlh.github.io/uxp-photoshop-zh-cn/)
- [Photoshop API Overview](https://developer.adobe.com/photoshop/uxp/2022/ps_reference/)
- UXP
    - Data Transfer:
        - [websocket](https://kihlh.github.io/uxp-photoshop-zh-cn/uxp/reference-js/Global%20Members/Data%20Transfers/WebSocket/)
            - UXP 框架window自带websocket
            - 做Client没问题. 相对于标准websocket, UXP的websocket没有WebSocket.Server? -> 不能作为server?
            ```JavaScript
              const ws = new WebSocket("ws://localhost:8082");
              ws.addEventListener("open", () => {
                console.log("We are conneceted");
              });
            ```
        - WebSocket Sample: https://github.com/AdobeDocs/uxp-photoshop-plugin-samples/tree/main/io-websocket-example
        - localstorage
			use localstorage to persist plugin data
            
            ```JavaScript
            // save
            localStorage.setItem("size", sizeInput.value);
            // get
            sizeInput.value = localStorage.getItem("size");
            ```
    - UI Element
    - 教程: [Adobe UXP: Things you need to know! #9 Adobe Spectrum | Davide Barranca](https://www.davidebarranca.com/development/adobe-uxp-things-you-need-to-know-9-adobe-spectrum-uxp)
            UXP中的环境是Adobe自己开发的模拟浏览器环境, 所以支持部分HTML元素, 比如`<div>`, 但是部分元素以及属性是不支持的或者和浏览器环境中不一致, 也在意料之中. 虽然原生元素可以使用, 但是开发中推荐使用Spectrum元素, 避免使用原生HTML元素.
        - Spectrum 是个设计框架 ☞ [Spectrum, Adobe’s design system](https://spectrum.adobe.com/)
            - [Spectrum CSS](https://opensource.adobe.com/spectrum-css/index.html) 可以把HTML拼成Spectrum类型的元素?
            - Components
                - [Coral Spectrum](https://opensource.adobe.com/coral-spectrum/documentation/)
                - (自带) [Spectrum - User Interface](https://kihlh.github.io/uxp-photoshop-zh-cn/uxp/reference-spectrum/User%20Interface/)
                    - UXP自带的Component基于[Spectrum Web Components](https://opensource.adobe.com/spectrum-web-components/) 但是(由于环境等原因)UXP自带的组件属性和Web Components在一些地方不一样
            - React Components
                - [React Spectrum](https://react-spectrum.adobe.com/react-spectrum/index.html)

> [!warning] 问题
>  没有原生自带`<sp-tabs>` → 可以参考官方 [ui-kitchen-sink](https://github.com/AdobeDocs/uxp-photoshop-plugin-samples/tree/main/ui-kitchen-sink) 和 [Tabs in React plugin - Photoshop / UXP Plugin API - Adobe Creative Cloud Developer Forums](https://forums.creativeclouddeveloper.com/t/tabs-in-react-plugin/4846)

wrapper component -> WC

---
### `manifest.json`

`manifest.json`整体为 UXP manifest, 包含了目标软件(PS, XD等)的manifest, 这里指PhotoShop manifest

UXP Manifest
- [Manifest v4](https://developer.adobe.com/photoshop/uxp/2022/guides/uxp_guide/uxp-misc/manifest-v4/)
- [Manifest v5](https://developer.adobe.com/photoshop/uxp/2022/guides/uxp_guide/uxp-misc/manifest-v5/)
PhotoShop manifest → [Photoshop Product specific manifest](https://developer.adobe.com/photoshop/uxp/2022/guides/uxp_guide/uxp-misc/manifest-v4/photoshop-manifest/)

`manifest.json`中`main`可以是html或js
带界面 Panel ☞ `"main": "index.html"`
不带界面 Command ☞ `"main": "index.js"`  

### `entrypoints`

插件的形式可以分为:
- Panel (点击后 出现标准的插件窗口)
- Commands (点击后 没有UI, 直接执行命令)
- Dialogs (点击后弹出窗口, 窗口不是标准的UI, 不能被dock)

https://developer.adobe.com/photoshop/uxp/2022/guides/uxp_guide/uxp-misc/manifest-v4/photoshop-manifest/
在`manifest.json`中, 比较重要的设置就是`entrypoints`, `manifest.json`的`entrypoints`只是设置UI入口, 实际的功能还需要通过`id`连接在`.js`文件中设置

> [!warning] 更改`manifest.json`的参数后, 需要重新加载组件

`manifest.json`中
```JSON
...
"entrypoints": [
    {
      "type": "command",
      "id": "uniqueID",
      "label": {
        "default": "new command"
      }
      ...
    },
    {
      "type": "panel",
      "id": "vanilla",
      "label": {
        "default": "Starter Panel"
      }
      ...
    }
]
...
```

![[PhotoShop-Plugin-1.png]]|![[PhotoShop-Plugin-2.png]]
---|-

js中
```JavaScript
const { entrypoints } = require('uxp');
```

command
```JavaScript
entrypoints.setup({
  commands: {
    // 方法一, 一个object中, 包含了一些function
    uniqueID: {
      run() { console.log("run") }
      ...
    }
    
    // 方法二, ID直接接function
    uniqueID: () = { ... }
    
    // 如果fucntion和ID同名, 可以直接用
    uniqueID
  }
  })
  
function uniqueID() {
    console.log("22222");
}
```

Panel
```
```

[www.davidebarranca.com](https://www.davidebarranca.com/development/adobe-uxp-things-you-need-to-know-4-commands-panels-manifest)

---
#### Icon
![[PhotoShop-Plugin-Icon.png|300]]

---
##### Flyout Menu
教程参考: [Adobe UXP: Things you need to know! #11 Flyout Menus and Entrypoints | Davide Barranca](https://www.davidebarranca.com/development/adobe-uxp-things-you-need-to-know-11-flyout-menus)

![[PhotoShop-Plugin-FlyoutMenu-1.png\|100]] |![[PhotoShop-Plugin-FlyoutMenu-2.png]]
---|-
实现的Flyout Menu的方式:
	在.js文件中`entrypoints.setup`中panel类型的入口中添加`menuItems`
```JavaScript
entrypoints.setup({
  panels: {
    vanilla: {
      ...
      menuItems: [
        {
          label: "Preferences", submenu:
            [
              { id: "bell", label: "🔔  Notifications" },
              { id: "dynamite", label: "🧨  Self-destruct", enabled: false },
              { id: "spacer", label: "-" }, // SPACER
              { id: "enabler", label: "Enable  🧨" },
            ]
        }, 
        ...
      ],
      // 当menu呗点击时返回id
      invokeMenu(id) {
        console.log(id);
      }
    }
  },
```

代码运行大致效果如下:
![[PhotoShop-FlyoutMenu-run.gif|500]]

##### Dialog / 弹窗
重要信息或者用户输入
教程: [Adobe UXP: Things you need to know! #10 Modal Dialogs by Davide Barranca](https://www.youtube.com/watch?v=wwuevOgv72g&list=PLRR5kmVeh43alNtSKHUlmbBjLqezgwzPJ&index=10)

> [!tip]
> Modal: focus can not interact other
Modeless: permits other activities 


`<dialog>`
modal
[Adobe Developer Products Products UXP for Adobe XD Develop UXP Design Share Console Sign in Edit Pro](https://developer.adobe.com/xd/uxp/develop/reference/ui/dialogs/)
```HTML
<dialog id="dialog">
    ... some content here
    <div>
        <sp-heading> </sp-heading>
    </div>
</dialog>const 
```
[Adobe Developer Products Products UXP for Adobe XD Develop UXP Design Share Console Sign in Edit Pro](https://developer.adobe.com/xd/uxp/develop/reference/ui/dialogs/showing/)
```JavaScript
// get the HTML element
const res = await document.querySelector('#dialog')

// open aysnc
await res.uxpShowModal({
    title: 
})

// close
res.close('OK') // will return the string for reason specification
```
`<sp-dialog>`
```JavaScript
.setAttribute("open") // open
.removeAttribute("open") // close
```

### 文件操作

UXP中两种方式来操作文件, 详情见文档: https://developer.adobe.com/indesign/uxp/resources/recipes/file-operation/

1. `localFileSystem` 返回`Entry` File Reference

```JavaScript
require('uxp').storage.localFileSystem; 

core.executeAsModal(async () => {
    // 插件路径内1.png
    const newFolderEntry = await require('uxp').storage.localFileSystem.getEntryWithUrl("plugin:/");          console.log(newFolderEntry);
})
```

2. `FS` https://developer.adobe.com/xd/uxp/uxp/reference-js/Modules/FileSystem/

```JavaScript
const fs = require("fs"); 

core.executeAsModal(async () => {
    // 插件路径内1.png
    const _file = await require("fs").readFile(`plugin:1.png`);
})
```

https://developer.adobe.com/photoshop/uxp/2022/guides/how-to/#file-io

- `"plugin:"`
    - `/Applications/photoshop-plugin-test/Test-9tkcnd/`
        
- `"plugin-data:"`
    - `/Users/userName/Library/Application Support/Adobe/UXP/PluginsStorage/PHSP/25/Developer/Test-9tkcnd/PluginData/`
        
- `"plugin-temp:"`
    - `/var/folders/p0/kb961x5d6wd79gfp2h6t_8500000gn/T/Adobe/UXP/PluginsStorage/PHSP/25/Developer/Test-9tkcnd/PluginData/`
- `"file:"` - `file:/Users/user/Documents` any file on computer

常用引用
```JavaScript
const fs = require('uxp').storage.localFileSystem;
const fs = require("fs"); 
```

##### Get文件夹(Entry)
```JavaScript
var saveFolder = await require("uxp").storage.localFileSystem.getFolder(); // 选择文件夹
```

##### 打开文档
https://youtu.be/zcvcLcEb788?si=WdRseNSX7mhfmmoE

```JavaScript
  core.executeAsModal(async () => {
    const entry = await require("uxp").storage.localFileSystem.getFileForOpening();
    await app.open(entry);
  })
```

##### 保存文档
https://developer.adobe.com/photoshop/uxp/2022/ps_reference/classes/document/

```JavaScript
// psd png jpg ...
const fileName = "target.psd";
await core.executeAsModal(async () => {
    let entry = await require('uxp').storage.localFileSystem.getFileForSaving(fileName);
    app.activeDocument.saveAs.psd(entry);
}
```

##### 读取插件目录下的文件, 并粘贴到图层
(batch部分详情参考PhotoShop API BatchPlay部分)
```JavaScript
  require('photoshop').core.executeAsModal(async () => {
    let result;
    let psAction = require("photoshop").action;
    const fs = require('uxp').storage.localFileSystem;
    const myfile = await fs.getEntryWithUrl("plugin:/1.png"); // 创建entry
    const token = fs.createSessionToken(myfile); // 创建Token
    let command = [
      // 导入进PS as 图层
      { "_obj": "placeEvent", "layerID": 2, "null": { "_kind": "local", "_path": token } }
    ];
    result = await psAction.batchPlay(command, {});
  })
```

## PhotoShop API

```JavaScript
const app = require('photoshop').app;
const core = require("photoshop").core;
```

### Document
```JavaScript
document.saveAs.jpg(entryJpg, { quality: 12 }, true); // 保存 (JPG)
```

```JavaScript
uxp.host.version // PhotoShop version
uxp.versions.uxp // UXP version
```

### Alert
```JavaScript
app.showAlert("alert content")
```

### Layers
```JavaScript
// get first object' name in layer
app.activeDocument.layer[0].name
app.activeDocument.layer[0].name = "new name"; // 可以直接重命名

// all layer
const layers = app.activeDocument.layers;

// selected layers
const activeLayers = app.activeDocument.activeLayers;

if(activeLayers.length === 0) {
    // no layer selected
}

activeLayers.forEach(layer => layer.selected = false);

layer.selected = true / false;

// 复制图层
layer.duplicate()

```

### 是否为调整图层
```JavaScript
isAdjustmentLayer(layer) {
    return layer.adjustmentInfo.hasOwnProperty(layer.kind);
}
```

```JavaScript
await core.executeAsModal(async () => {
    // 创建一个文档
    await app.documents.add();
    
    // 创建图层
    await app.activeDocument.createLayer({ name: "myLayer", opacity: 80, blendMode: "colorDodge" });

    // 
})
```

### [ExecuteAsModal](https://developer.adobe.com/photoshop/uxp/2022/ps_reference/media/executeasmodal/) 模态执行?

```JavaScript
Button.addEventListener("click", (async ()=> {
            await core.executeAsModal( fucntionName ); 
        }
    )
)
```

BachPlay
Photoshop is complex software, with many internal classes and methods. Not all of these are yet exposed via UXP. ☞ Use batchplay if there is not PhotoShop API. Batchplay in UXP replaces actionmanager in CEP?

```JavaScript
// 添加一张图
_obj: "placeEvent",
ID: 4, // ?
null: {
   _path: "/Users/userName/Downloads/20231128-191053.jpeg",
   _kind: "local"
},
```

BatchPlay async
``` js
photoshop.action.batchPlay([toSmart0bject],{synchronousExecution: true})
```

ActionManager
可以添加[Event Listener](https://developer.adobe.com/photoshop/uxp/2021/ps_reference/media/advanced/event-listener)的方式查看batchplay, 或者用插件[Alchemist](https://exchange.adobe.com/apps/cc/2bcdb900)

> [!warning] 不要使用商店中的版本
> 商店中的版本权限不全, 指令记录不全
使用开发版的: https://github.com/jardicc/alchemist 按照正常node编译即可

| ![[PhotoShop-alchemist-Listen.png]] | ![[PhotoShop-alchemist-code.png]] |
| :--: | :--: |
| 点Listener开始记录 | 生成代码 |

---
## 其他
### PNG-8 vs PNG-24


通过PS分别导出PNG-8和PNG-24格式的PNG, 在Mac中Terminal File命令查看文件:
- PS的PNG-24是8-bit/color RGB(A)
- PS的PNG-8是8-bit colormap
![[PhotoShop-PNG8:24-1.jpeg]]
其实不管PNG-8还是PNG-24都是8bit的图片. 不过PNG-8是用colormap格式, colormap是单8bit通道, 通过256个预设颜色来显示图片. PNG-24有多个通道, 是我们正常理解的R,G,B 3个通道分别有8bit(0-256)的值.
![[PhotoShop-PNG8:24-2.jpg]]