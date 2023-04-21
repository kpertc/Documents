### Basics

-   JavaScript -> only run in browser
    
-   Node.js
    
    -   Open source, cross platform, runtime environment for executing JavaScript code outside a browser. (Not a language or a framework)
        
    -   Built on the V8 JavaScript engine (Same a Google Chrome)
        
    -   Written in C++

**NPM** is a package manager for Node.js

`node -v` nodejs version to check if nodejs is installed

### Run JS in VS Code
![[run_JavaScript_VSCode.gif]]

<br>


### NPM (Node Package manager) (download something)
-   is an online repository for open- source node.js projects
-   CLI tool that helps with installation, version and dependency management.

Local & Global install
-   Local installs have links created at `./node_modules/.bin/directory`
-   Global installs have links created from global `/bin` directory


```bash

Command:
npm run # list all commands

npm uninstall + package name # Uninstall package:

npm config set registry=http://xxxxxxx # Set registry

npm init + xxx # start a project with settings

```

```bash
# Remove node_modules, packages and yarn
rm -rf node_modules yarn.lock package-lock.json
```

<br>

```shell
npm install ... # save to package.json dependencies 
npm install ... --save # save to package.json dependencies 
npm install ... --save-dev # save to package.json devDependencies 
```

- dependencies : Packages required by your application in production. 
- devDependencies: Packages that are only needed for local development and testing.

<br>

##### NVM Node Version Manager

Install at https://github.com/nvm-sh/nvm
Windows version: https://github.com/coreybutler/nvm-windows

If problem`-bash: nvm: command not found` use `source ~/.nvm/nvm.sh`

Type `nvm` will list all commands 

![[nvm.png]]

```bash
# list all
nvm ls 
nvm install [verison] # install a node js
nvm use [version] # use a version of node js
```

NPX (run something)

![[image-2.png]]

check if NPX is installed `which npx`

Install NPX `npm install -g npx`



Install Command Line Tools: [[Env Tools]]