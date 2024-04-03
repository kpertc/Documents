#editor #web-dev 

### Shortcuts

![](https://code.visualstudio.com/assets/docs/getstarted/tips-and-tricks/KeyboardReferenceSheet.png)

Editor Shortcut| 
---|---
Command Palette|⌘ ⇧ P
Toggle Terminal|Ctrl \`
Sidebar|⌘ B
New Tab|⌘ N
New Window|⌘ ⇧ N
Tab Bar Explore (File)|⌘ ⇧ E
Tab Bar Search|⌘ ⇧ F
Open & Fold UnFold| ⌘ ↓
Split Editor|⌘ \
Duplicate Line|⇧ Option ↑ / ↓
Select Entire Line<br>Select Multiple Lines if Multiple Times |⌘ L
Delete Line|⌘ ⇧ K
Insert Line|⌘ Enter
Matching Bracket|⌘ ⇧ \
Multiline Comment|⇧ Option A
Highlight(Select)|Shift ↑/↓/←/→
Select Next Match|⌘ D
Tab|Ctrl + tab#
Close All Tabs|⌘ K W


Same as Chrome| 
---|---
Right Tab|⌘ ⇧ \[
Left Tab|⌘ ⇧ ]
Settings| ⌘ , (MacOS) <br> Ctrl , (Win)
Open last closed Tab|⌘ ⇧ T


Selects the word at the cursor|`⌘` + `D`
multi-cursor|Alt+Click ⌥⌘↓ ⌥⌘↑

Shift+Alt

Ctrl Tab![[ctrl-tab.gif]]

Ctrl Enter
![[ctrl-enter.gif]]

Shift Option ↑ / ↓
![[shift-option.gif]]<br>


Terminal Up / Down
Ctrl ⌘ ↑/↓
![[terminal-up-down.gif]]

### Markdown
https://code.visualstudio.com/docs/languages/markdown

Preview markdown `⇧⌘V`
Preview markdown side by side
![[md-dynamic-preview.gif]]

<br>

### Snippets

![[snippet-JavaScript.gif]]

Basic
```json
	"Console Log" : {
		"prefix": "clg",
		"body": "console.log($1)",
		"description": "Create console.log()"
	}
```

`$#` cursor start point
`Tab` → next `$#`
$0 → last point

```json
	"Console Log" : {
		"prefix": "clg",
		"body": [
			"console.log($1);",
			"$2"
		],
		"description": "Create console.log();"
		},
	
	"Console Log Template String" : {
		"prefix": "clgt",
		"body": [
			"console.log(`${$1}`);",
			"$2"
		],
		"description": "Create console.log(); with Template String"
	}
```

$variable type at same time, `Tab` type next $variable
```json
"For Loop for Array" : {
	"prefix": "forarr",
	"body": [
		"for (let $index = 0; $index < $array.length; $index++) {",
		"\\tconst element = $array[$index];",
		"\\t",
		"}"
	],
	"description": "This will create a for loop through an array"
}
```

Settings Sync is on → VS Code Settings automatically sync
![[Settings-Sync-Configure.png]]

Sync Extension: Settings Sync

<br>

### [Emmet](https://code.visualstudio.com/docs/editor/emmet)

Builtin

![[Emmet.gif]]

```html
div.container
<div class="container"></div>

div#container
<div id="container"></div>

div.className#idName
<div class="className" id="idName"></div>

li*3
<li></li>
<li></li>
<li></li>

input:text
<input type="text" name="" id="">
```

![[Emmet-css.gif]]
```css
p10
padding: 10px;

m10
margin: 10px;
```
<br>

### Open Setting.json
![[vscode-open-settingjson.gif]]

##### Bracket pair colorizer
1. `editor.guides.bracketPairs": true,`
2. restart VS Code
![[builtin-bracket-pair-colorizer.png| 200]]

##### Font Ligatures

```json
{
  "editor.fontFamily": "*** Your ligature enabled font ***",
  "editor.fontLigatures": true,
}
```

![[font-ligatures.png]]


### show space as dot
```json
"editor.renderWhitespace": "all", 
```
![[vscode-renderWhitespace.png]]
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

### `code` Command

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

### C++

![[cmake-run-c++.png]]

### Python
![[switch-python-interpreter-vscode.gif]]
### Extension

Plugin|Function
---|---
Quokka.js|display JavaScript result in editor

##### Command Runner

![[vscode-command-runner.gif]]

```JSON
"command-runner.commands": {
	"node version to 14.18.1": "nvm use 14.18.1",
	"1. npm run clean && git clean -xdf": "npm run clean && git clean -xdf",
	... 
},
```

##### Better Comments
Can add and be customized
![[Better-Comments.png]]

##### Code runner 
run C++
![[vscode-coderunner-run.gif]]
##### Extension Development

[https://code.visualstudio.com/api/get-started/your-first-extension](https://code.visualstudio.com/api/get-started/your-first-extension)

```shell
npm install -g yo generator-code yo code
```

##### [[Blender VSCode Setup]]