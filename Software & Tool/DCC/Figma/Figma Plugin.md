#JavaScript #TypeScript

Figma Documentation: https://www.figma.com/developers
API Reference: https://www.figma.com/plugin-docs/api/api-reference/
Tutorial: https://youtu.be/pFGhMr6rDhc


## Figma Shortcuts

Search `⌘ +` `/`

Runs the last plugin `⌥ + ⌘ + P`

Build `⇧ +⌘ + B` -> Choose `TSC: Watch` to convert Ts to Js

  

### New Plugin in Figma

New Plugin|Open Console
---|---
![[Figma-Plugin-img/New Plugin.png]]|![[Figma-Plugin-img/Open Console.png]]

### [Setup Envir](https://www.figma.com/plugin-docs/setup/)

> [!info]
>Recommend writing in Typescript then convert to Javascript

Install [Node.js](https://nodejs.org/en/download/) include npm
Install TypeScript `sudo npm install -g typescript`
安装TypeScript后在Figma中新建~~的Plugin就有.~~~~ts~~~~文件了！~~

`npm install --save-dev @figma/plugin-typings`

TypeScript|Add to tscofig.json as need
---|---
![[Figma-Plugin-img/TS.png]]|![[Figma-Plugin-img/tscofig.jpg]]

### Example Code:

  

HTML

```JavaScript
<script>
    document.getElementById('id').onclick = (event) => {
        parent.postMessage({pluginMessage: {type: 'type'}}, '*')
    }
</script>
```

  

```TypeScript
// Selection:
// Get current selection
var nodes = figma.currentPage.selection;

// Set current selection
figma.currentPage.selection = 
```