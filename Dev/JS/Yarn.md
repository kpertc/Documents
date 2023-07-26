#web-dev #JavaScript 

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

yarn run 

yarn remove packagename 

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

# remove package
yarn remove packagename
```