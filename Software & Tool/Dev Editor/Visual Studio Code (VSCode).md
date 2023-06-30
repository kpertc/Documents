#editor #web-dev 

Command Palette `⌘` + `Shft` + `P`

Editor Shortcut
Selects the word at the cursor `⌘` + `D`
multi-cursor Alt+Click ⌥⌘↓ ⌥⌘↑
Shift+Alt

<br>

### Markdown
https://code.visualstudio.com/docs/languages/markdown

Preview markdown `⇧⌘V`
Preview markdown side by side
![[md-dynamic-preview.gif]]
<br>

### Open Setting.json
![[vscode-open-settingjson.gif]]

Builtin bracket pair colorizer
1. `editor.guides.bracketPairs": true,`
2. restart VS Code
![[builtin-bracket-pair-colorizer.png| 200]]

<br>

### Compare with Selected
[Compare Contents of Two Files](https://www.mytecbits.com/microsoft/dot-net/compare-contents-of-two-files-in-vs-code)

1. Select a file
2. `RMB` on `Compare with Selected`

<br>

### (File) Timeline
https://github.com/microsoft/vscode-docs/blob/vnext/release-notes/v1_66.md#local-history

<br>

### Restart TS server
当TS自动补全失效时尝试
![[restart-TS-server.webp]]

<br>

### `code`

### [How to Open Visual Studio Code From Your Terminal](https://www.freecodecamp.org/news/how-to-open-visual-studio-code-from-your-terminal/)

1.  Install code command

[https://code.visualstudio.com/docs/editor/command-line](https://code.visualstudio.com/docs/editor/command-line)

```shell
# open folder by VSCode
cd {path} 
code .

# open the file
code src/Data.ts

# open folder in a new window
code src/Plugin/
```



### Plugin
Plugin|Function
---|---
Quokka.js|display JavaScript result in editor



### Command Runner
![[vscode-command-runner.gif]]

```JSON
"command-runner.commands": {
	"node version to 14.18.1": "nvm use 14.18.1",
	"1. npm run clean && git clean -xdf": "npm run clean && git clean -xdf",
	... 
},
```

<br>

### Extension

[https://code.visualstudio.com/api/get-started/your-first-extension](https://code.visualstudio.com/api/get-started/your-first-extension)

```shell
npm install -g yo generator-code yo code
```