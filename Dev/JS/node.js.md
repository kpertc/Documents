#JavaScript #web-dev 

### Basics

- JavaScript -> only run in browser
- node.js
	-   Open source, cross platform, runtime environment for executing JavaScript code outside a browser. (Not a language or a framework)
	-   Built on the V8 JavaScript engine (Same a Google Chrome)
	-   Written in C++

**NPM** is a package manager for Node.js

```shell
node -v #nodejs version to check if nodejs is installed
```

### Why use node
- Fast, efficient and highly scalable
- Event driven, non-blocking I/O model
- Popular in the industry
- Same language on the front and back e nd (JS)

- Single threaded
- Supports concurrency via events & callbacks
- EventEmitter class is used to bind events and listeners

![[event-emitters.png| 200]]

Good to use Node.js
- REST API & Microservices
- Real Time Services (Chat, Live Updates)
- CRUD Apps - Blogs, Shopping Carts, Social Networks
- Tools & Utilities

Short Answer: Anything that is not CPU intensive
CPU intensive work → offload to `worker_threads` (stable since Node 12)



### Execute JavaScript

Execute JS code
`node`
![[node.png | 200]]

Execute JS file in terminal thru node
![[run_JavaScript_VSCode.gif]]

<br>

```JavaScript
console.log(process)
```

![[prrocess.png | 300]]

```js
process
process.platform
process.env // webpack
```

<br>

### NPM 
Node Package manager
Acquired by GitHub (2020)

https://www.npmjs.com

-   is an online repository for open-source node.js projects
-   CLI tool that helps with installation, version and dependency management.

Local & Global install
-   Local installs have links created at `./node_modules/.bin/directory`
-   Global installs have links created from global `/bin` directory

```shell
npm -v # show version

# help page
npm
npm help

npm run # list all commands
# command script defined in package.json
```

```bash
# Remove node_modules, packages and yarn
rm -rf node_modules yarn.lock package-lock.json
```

```shell
# install pacakges
npm install packagename1 # install one package
npm install packagename1 packagename2 ... # install multiple at once

npm install -g packagename # install globally 

npm install packagename@4.17.3 # install specific version

npm install ... --no-save # install but will not add to package.json
npm install ... # save to package.json dependencies (default since npm 5, --save is a no-op)
npm install ... --save-dev # save to package.json devDependencies 

npm install # all dependencies (include devDependencies)
npm install --omit=dev # only install dependencies (not devDependencies), was --production
npm ci --omit=dev # clean install from package-lock.json (CI / Docker)

# Uninstall package:
npm uninstall packagename
npm remove packagename # alias
npm rm packagename # alias
```

- dependencies : Packages required by your application in production. 
- devDependencies: Packages that are only needed for local development and testing. (tools to assist dev)

`node_modules` will also includes dependencies' dependencies

```shell
# list all packages
npm list

npm list --depth 0 # only show top level packages
npm list --depth 1 # only show secondary level packages
```

##### `package.json`

Manifest file with app info
- ==Lists dependencies== (name & version)
- Specify if versions should be updated
- Create NPM scripts
- Easily create with `npm init`

```shell
npm init # create package.json
npm init -y # default settings
npm init --yes
npm init ...  # start a project with settings

# npm config → ~/.npmrc, NOT package.json
npm set ...
npm config set ...

# get npm config
npm get ...
npm config get ...

# delete npm config
npm config delete ...

# edit package.json itself
npm pkg set key=value

# get registry 
npm get registry

# set registry
npm config set registry=http://xxxxxxx


# clean cache
# use when installatopm failed
npm cache clean --force
```

![[semantic_versioning.png | 350]]


install to latest minor version
`"^2.20.1"`
> install to 2.22.1

install to latest patch version
`"~2.20.1"`
> install to 2.20.4

install exact version
`"2.20.1"`
> install to 2.20.1

install latest version (Not a good idea)
"\*"
> install to 5.0.0


`"three": "*"` → Latest version

##### Scripts
```shell
npm start

# other name need add "run"
npm + run + scripts name

# e.g.
npm run start
```

##### Global Packages
``` shell
npm install -g packagename # install globally

npm remove/uninstall -g packagename

# where global packages are installed to
npm root -g
# /usr/local/lib/node_modules
```

##### `npm link`
```shell
# 1. in the package folder (~/my-lib)
npm link # register globally

# 2. in the consuming project
npm link my-lib

npm unlink my-lib # teardown
```
link between a globally installed package and a local project. Allows you to work on a package locally while using it as a dependency in another project without the need to publish it to the npm registry.

##### NVM Node Version Manager

create the path first, then install
``` sh
touch ~/.bashrc
touch ~/.zshrc
```

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

##### `npx`
installed with Node.js and NPM
run packages without in a project packages and dependencies

![[image-2.png]]

check if NPX is installed `which npx`
if missing → repair/update Node & NPM (`npm install -g npx` is deprecated and shadows the bundled one)



Install Command Line Tools: [[Env Tools]]

<br>

### fs
fs → file system module

```js
const fs = require("fs");

// read file
const fileContents = fs.readFileSync("./file.txt", "utf-8");

fs.readFile("./file.txt", (error, data) => {
	
})

// internal buffer
```

run shell command
```js
const { exec } = require("child_process");

// callback is (error, stdout, stderr)
exec("pwd", (err, data) => {
	if (err) { console.log(err) }
	else { console.log(data) }
})
```