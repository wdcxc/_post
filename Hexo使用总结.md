---
title: Hexo使用总结
date: 2015/10/24 
tags: 
- Tools
- Hexo
categories:
- Tools
---

[toc]

---

## 1.简介

[Hexo](https://hexo.io/zh-cn/)是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

---

## 2.安装

**1.Git的安装**

Linux (Ubuntu, Debian)

```
sudo apt-get install git-core
```

Linux (Fedora, Red Hat, CentOS)

```
sudo yum install git-core`
```

**2.Node.js的安装**

安装 Node.js 的最佳方式是使用nvm

+ nvm的安装

curl

```
curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```

wget

```
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```

+ Node.js的安装

```
nvm install 0.10
```

**3.Hexo的安装**

```
npm install -g hexo-cli

```

---

## 3.基本使用

### 3.1 初始化

```
hexo init <folder>
cd <folder>
npm install
```

### 3.2 常用命令

|命令|使用场景|使用语法|参数|
|-|-|-|-|
|init|新建一个网站|hexo init [folder]||
|||||
|new|新建一篇文章|hexo new [layout] \<title\>||
|g[enerate]|生成静态文件|hexo g[enerate]|-d,-w|
|s[erver]|启动服务器|hexo s[erver]|-p,-s,-l|
|deploy|部署网站|hexo deploy|-g|
|||||
|clean|清除缓存和静态文件|hexo clean||
|list|列出网站资料|hexo list \<type\>||
|version|显示Hexo版本|hexo version||

[更多命令](https://hexo.io/zh-cn/docs/commands.html)

### 3.3 文件结构

```
.
├── _config.yml
├── package.json
├── scaffolds
├── scripts
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

+ *_config.yml*
网站的**配置**信息，可以在此配置大部分的参数

+ *package.json*
应用程序的信息，EJS, Stylus 和 Markdown renderer 已默认安装,可以自由移除

+ *scaffolds*
**模版**文件夹，新建文章时，Hexo 会根据 *scaffold* 来建立文件。

+ *scripts*
**脚本**文件夹。脚本是扩展 Hexo 最简易的方式，在此文件夹内的 JavaScript 文件会被自动执行。

+ *source*
**资源文件夹**是存放用户资源的地方。除 *_posts* 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 *public* 文件夹，而其他文件会被拷贝过去。

+ *themes*
**主题**文件夹。Hexo 会根据主题来生成静态页面。

### 3.4 基本配置

可以在 *_config.yml* 中修改大部份的配置

+ **网站**

|参数|描述|
|-|-|
|title|网站标题|
|subtitle|网站副标题|
|description|网站描述|
|author|您的名字|
|language|网站使用的语言|

+ **网址** 

|参数|描述|
|-|-|
|url|网址|
|root|网站根目录|    
|permalink|文章的永久链接格式|

[更多配置](https://hexo.io/zh-cn/docs/configuration.html)


### 3.5 主题使用

选择想要使用的[主题](https://hexo.io/themes/)，根据指导配置即可

### 3.6 插件使用

选择想要添加的[插件](https://hexo.io/plugins/)，根据指导安装即可

### 3.7 部署

Hexo 提供了快速方便的一键部署功能，让您只需一条命令就能将网站部署到服务器上

```
hexo deploy
```

在开始之前，必须先在 *_config.yml* 中修改参数，一个正确的部署配置中至少要有 type 参数，例如

```
deploy:
  type: git
```

可以同时使用多个 deployer，Hexo 会依照顺序执行每个 deployer

```
deploy:
- type: git
  repo: 
- type: heroku
  repo:
```

#### 3.7.1 Git的部署

1.安装 hexo-deployer-git

```
npm install hexo-deployer-git --save
```

2.修改配置

```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```

|参数|描述|
|-|-|
|repo|库（Repository）地址|
|branch|分支名称，如果使用的是 GitHub 或 GitCafe 的话，程序会尝试自动检测|
|message|自定提交信息|

[更多部署](https://hexo.io/zh-cn/docs/deployment.html)

---

## 4.注意点

+ nvm 安装以后需要重启，相应命令才能生效

+ 我自己使用虚拟机(ubuntu)安装使用 Hexo ，重启的时候输入 `hexo` 提示找不到命令，先执行以下命令，然后就可以再执行相应的  `hexo` 命令了

```
nvm use [安装的Node.js版本号]
```

+ `hexo` 的相应命令要到 `hexo init` 指定的文件夹下执行

+ 站点配置文件(_config.yml)中的 theme 属性值要和 *theme* 目录下的主题文件夹的名字一致(即从 github 下载主题后要对主题文件夹的名字进行相应修改)，不然执行 `hexo g` 的时候可能会报错

+ 执行 `hexo s` 前需要确保防火墙正确设置，相应的端口可以被开启

+ 可以直接把文章放在 *source/_posts* 下,而不用每次都运行 `hexo new` 命令生成


