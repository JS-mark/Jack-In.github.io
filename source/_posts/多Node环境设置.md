---
title: 多Node环境设置
type: categories
author: Mark
layout: post
comments: true
external_link:
  enable: true
date: 2020-09-12 22:35:01
categories: JavaScript #分类
tags:
  - 前端开发
  - JavaScript
  - NPM
---

建议使用 [NVM](https://github.com/creationix/nvm) 对`Node`进行管理，在安装Node之前可以先安装好`NVM`，下面几种安装方式任选其一即可。
<!-- more -->

[](#安装NVM "安装NVM")安装NVM
-----------------------

* curl

  curl -o- <https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh> | bash

* wget

    wget -qO- <https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh> | bash

* **git**（建议这种安装方法，能够获取到最新的NVM版本）

  git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout \`git describe --abbrev=0 --tags\`

    . ~/.nvm/nvm.sh

上述操作成功之后，打开`Terminal`输入`NVM`，若能看到帮助信息说明安装成功。

[](#使用NVM "使用NVM")使用NVM
-----------------------

安装好 `NVM` 之后就可以安装指定版本的`Node`了，假设安装4.2版本的可以执行下面命令：

```bash
nvm install 8.0
```

`NVM`可以同时安装多个版本的`Node`，切换使用也是相当方便，下面命令指定使用4.2版本的：

```bash
nvm use 8.0
```

查看你安装的`Node`列表：

```bash
nvm ls
```

`NVM`默认从 [http://nodejs.org/dist/](http://nodejs.org/dist/) 下载资源，速度相对较慢，我们可以切换到国内的源：

```bash
export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/dist
source ~/git/nvm/nvm.sh
```

[](#NPM "NPM")NPM
-----------------

`NPM`作为`Node`的包管理器，现在是随着`Node`的安装同时进行安装的，通过`NPM`可以很方便地对包进行管理。

### [](#NPM加速 "NPM加速")NPM加速

`NPM`默认是从 [http://register.npmjs.org/](http://register.npmjs.org/) 进行资源的下载，在碰到需要`node-gyp`进行编译的时候还要从 [http://nodejs.org/dist/](http://nodejs.org/dist/) 重新下载一次资源，这会导致下载速度非常慢，通过下面命令切换下载源加速`NPM`。

```bash
npm --registry=https://registry.npm.taobao.org --disturl=https://npm.taobao.org/dist
```

### [](#解决NPM全局安装需要Sudo的问题 "解决NPM全局安装需要Sudo的问题")解决NPM全局安装需要Sudo的问题

1. 创建全局包目录

    $ mkdir "${HOME}/.npm-packages"

1. 在.bash\_profile/.zshrc中增加下面代码

    NPM\_PACKAGES="${HOME}/.npm-packages"

    NODE\_PATH="$NPM\_PACKAGES/lib/node\_modules:$NODE\_PATH"

    PATH="$NPM\_PACKAGES/bin:$PATH"

2. 在 $HOME/.npmrc 中增加下面代码

    prefix=${HOME}/.npm-packages

如果你很懒，那么你可以看看 [这里](https://github.com/glenpike/npm-g_nosudo) 的说明进行自动化帮你解决问题！

### [](#npm-install-xxx报-EACCESS-mkdir错误 "npm install xxx报 EACCESS,mkdir错误")npm install xxx报 EACCESS,mkdir错误

~/.npm目录权限问题，

```bash
sudo chown -R $USER:$GROUP ~/.npm

npm cache clean
```
