<!--
 * @Description:
 * @version:
 * @Author: LMG
 * @Date: 2020-06-06 23:47:56
 * @LastEditors: LMG
 * @LastEditTime: 2020-06-07 01:01:48
-->

# 快速搭建 Nodejs 环境

## linux(root 用户)

### 克隆 nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"

nvm --version
```

### 通过 nvm 安装 node

```bash
nvm install 14.3.0
nvm use  14.3.0
```

### 查看版本

```bash
nvm ls-remote
npm  -v
npm install -g cnpm --registry=https://registry.npm.taobao.org  //使用淘宝镜像
```

## window(使用 Cmder 命令行)

### 下载 nvm 安装包并安装

[nvm-windows](https://github.com/coreybutler/nvm-windows/releases)

### 查看版本

```bash
nvm -v
```

### 常用命令

```bash
nvm list　　//查看目前已经安装的版本
nvm list available //显示可下载版本的部分列表
nvm install 10.15.0 //安装指定的版本的nodejs
nvm use 10.15.0 //使用指定版本的nodejs
npm install -g cnpm --registry=https://registry.npm.taobao.org  //使用淘宝镜像

cnpm sync connect //同步模块
```
