#web-dev #JavaScript 

https://www.youtube.com/watch?v=g9_6KmiBISk

Yarn (Yet Another Resources Negotiator) 
A JavaScript Package Manager developed by Facebook
Any thing can be installed by NPM can be installed by Yarn

Yarn is used to be much better than NPM, but not so much for now
NPM 2017
Compare to NPM 4
- Much faster than NPM 4
- Added standardized lockfile for cross-package compatibility
- Removed the need for --save to save as dependency

NPM 5 is also fast

```Bash
# 在Mac Terminal里全局安装
npm install -g yarn

# 如果显示权限报错，请在前面加sudo
sudo npm install -g yarn

# 回到VS Code的Terminal
# 输入
yarn

安装依赖资源后会生成node_module文件夹
```

```shell
yarn help

yarn cache list
yarn cache list --parten packagename

yarn cache clean
```

```shell
# init a project from zero
yarn init # some options
yarn init -y # default
# then create package.json

# install packages in package.json
yarn install

# add package
yarn add packagename
yarn add packagename@4.17.3 # add specific version

# add as devdependency
yarn add packagename -D
yarn add packagename --dev

# remove package
yarn remove packagename

# install globally 
yarn global add packagename

# remove globally 
yarn global remove packagename

# where global install
yarn global bin
# /usr/local/bin

# upgrade
yarn upgrade
yarn upgrade@4.1.1 #specific version
```

``` shell
# list all packages
yarn list

# list only "packagename" 's dependency
yarn list --parttern packagename

yarn list --depth=0 # only list top layer packages
```

```shell
# check outdated packages
yarn outdated 

# check specific packages
yarn outdated packagename
```

![[yarn-outdated.png]]

##### lock file

Install exact version cross different computes

```shell
# check if yarn.lock match package.json
yarn check

# generate yarn.lock base on existing node_module
yarn import
```

##### Script
```shell
yarn run 
```

```shell
# Creates a compressed gzip archive of package dependencies.
yarn pack
```

```shell
# 在home directory

yarn set version stable # 升到3

yarn set version 1.22.19 #  使用1**
```