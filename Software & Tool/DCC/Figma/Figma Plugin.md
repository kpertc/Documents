#JavaScript #TypeScript

Figma Documentation: https://www.figma.com/developers
API Reference: https://www.figma.com/plugin-docs/api/api-reference/
Tutorial: https://youtu.be/pFGhMr6rDhc


## Figma Shortcuts

Search `⌘ +` `/`

Runs the last plugin `⌥ + ⌘ + P`

VS Code Build `⇧ +⌘ + B` -> Choose `TSC: Watch` to convert Ts to Js

  

### New Plugin in Figma

New Plugin|Open Console
---|---
![[Figma-Plugin-img/New Plugin.png]]|![[Figma-Plugin-img/Open Console.png]]

### [Setup Envir](https://www.figma.com/plugin-docs/setup/)

> [!info]
>Recommend writing in Typescript then convert to Javascript

Install [Node.js](https://nodejs.org/en/download/) include npm
Install TypeScript `npm install --save-dev typescript`，用 `npx tsc` 运行
Figma 新建 Plugin 时可以直接选 TypeScript 模板

`npm install --save-dev @figma/plugin-typings`

TypeScript|Add to tscofig.json as need
---|---
![[Figma-Plugin-img/TS.png]]|![[Figma-Plugin-img/tscofig.jpg]]

### Example Code:

  

HTML (UI thread -> plugin thread)

```HTML
<script>
    document.getElementById('id').onclick = (event) => {
        parent.postMessage({pluginMessage: {type: 'type'}}, '*')
    }
</script>
```

Plugin side (code.ts) receives it

```TypeScript
figma.showUI(__html__)
figma.ui.onmessage = (msg) => {
    if (msg.type === 'type') {
        // do something
    }
    figma.closePlugin()
}
```

  

```TypeScript
// Selection:
// Get current selection
var nodes = figma.currentPage.selection;

// Set current selection
figma.currentPage.selection = [node]; // takes an array of SceneNode
figma.viewport.scrollAndZoomIntoView([node]);
```