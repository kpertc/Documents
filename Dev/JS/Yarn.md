#web-dev #JavaScript 

https://www.youtube.com/watch?v=g9_6KmiBISk

Yarn (名字不是缩写，别和 Hadoop 的 YARN 混)
A JavaScript Package Manager developed by Facebook
Any thing can be installed by NPM can be installed by Yarn

Yarn is used to be much better than NPM, but not so much for now
NPM 2017
Compare to NPM 4 (2017 snapshot)
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

安装依赖资源后会生成node_modules文件夹
```

```shell
yarn help

yarn cache list
yarn cache list --pattern packagename

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

# install globally (Yarn 1 only, 2+ 已移除 global)
yarn global add packagename

# remove globally 
yarn global remove packagename

# where global install
yarn global bin
# /usr/local/bin

# Yarn 2+: 一次性执行用 yarn dlx packagename，常驻的用 npm -g 装

# upgrade (Yarn 2+ 改叫 yarn up)
yarn upgrade
yarn upgrade packagename@4.1.1 #specific version
```

``` shell
# list all packages
yarn list

# list only "packagename" 's dependency
yarn list --pattern packagename

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
# Yarn 1 only: check if yarn.lock match package.json
yarn check
# Yarn 2+ (Berry): yarn install --immutable (CI 里就用这个)

# Yarn 1 only: generate yarn.lock base on existing node_module
yarn import
# Yarn 2+: 已移除，不需要替代
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

yarn set version stable # stable = 当前 major（现在是 4.x）
yarn set version 4 # 明确锁到 4

yarn set version 1.22.19 #  使用1**
```