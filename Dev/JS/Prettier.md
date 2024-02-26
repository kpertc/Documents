### Install
prettier recommends install a exact version, using `—save-exact` in npm `-exact` in yarn
```bash

```


```bash
# formatting
prettier --write index.html # format a file
prettier --write . # format all files, need to use ignore node_modules, dist ...
prettier --write \"{./src,./statics}/**/*.{js,ts,tsx}“ # file glob syntax

# checking
prettier --check index.html # check

# watch
prettier --watch
```

### ignore file 
`.prettierignore`
```
build
dist
node_modules

*.html # all .html
```

### Config
`.prettierrc` /  `.prettierrc.json`
```json
{
	"semi" : true,
	"overrides" : [
		{
			// override rules, specific to .ts files
			"files" : ".ts",
			"options" : {
				"semi" : false
			}
		},
		{
			// override rules, specific to files in legacy path
			"files" : "legacy/*",
			"options" : {
				"semi" : false
			}
		}
	]
}
```

---

install Prettier VSCode extension

Eslint
> If you use ESLint, install [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier#installation) to make ESLint and Prettier play nice with each other. It turns off all ESLint rules that are unnecessary or might conflict with Prettier.


![[vscode-defaultFormatter.png]]

enable format on save
![[vscode-formatOnSave.png]]