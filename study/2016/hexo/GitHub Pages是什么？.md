title: Github Pages与Hexo搭建博客教程
date: 2015-06-16 11:06:53
tags: '教程'
---

## GitHub Pages是什么？

GitHub Pages是GitHub提供的免费空间，可以用来托管用户的静态网页。网页内容可以是用户/组织介绍或者项目介绍。官网给出的描述是：“Websites for you and your projects.”

有两种方式创建、发布静态页，1：使用Automatic Page Generator工具；2：使用GitHub客户端或者命令行。本文使用第二种方法。

## 创建GitHub Pages

### 1. 安装、配置Git工具：
参考：https://help.github.com/articles/set-up-git/

### 2. 创建站点：
参考：https://pages.github.com

* 创建一个新的项目，名为：username.github.io，注意这个username一定要是你GitHub账号名，否则后续操作不能成功。如下图：

![](https://pages.github.com/images/user-repo@2x.png)

* 将这个项目从github克隆到本地文件夹

```
~ $ git clone https://github.com/username/username.github.io
```

* 进入文件夹，增加一个index文件

```
~ $ cd username.github.io
~ $ echo "Hello World" > index.html
```

* 进入文件夹，增加一个index文件

```
~ $ cd username.github.io
~ $ echo "Hello World" > index.html
```

* 新增这个文件、并提交至本地库，然后推送至远程github库

```
~ $ git add --all
~ $ git commit -m "提交的说明信息"
~ $ git push -u origin master
```
* 最后在浏览器中访问：`http://username.github.io` ，Duang~~如果看到页面显示Hello World就成功了。

## 使用Hexo博客框架为你的博客添砖加瓦

### 1. 安装Hexo

前提：[node.js](https://nodejs.org/)，[Git](http://git-scm.com/)

安装完以上必要程序，即可安装Hexo

```
$ npm install -g hexo-cli
```
### 2. 初始化
安装完Hexo，新建文件夹如：Hexo，进入此文件夹执行以下命令：

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

初始化完成后，目录如下：

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

### 3. 安装Hexo本地服务器

```
$ npm install hexo-server --save
```

启动本地服务器

```
$ hexo server
```

浏览器中访问：http://localhost:4000 即可看到初始的博客界面，默认主题是：landscape。

在服务器启动期间，Hexo 会监视文件变动并自动更新，您无须重启服务器。

### 4. 生成静态文件
```
$ hexo generate
```

### 5. 部署至GitHub Pages

首先修改Hexo根目录下的_config.yml配置，一般在尾部

```
deploy:
  type: git
  repo: 'git@github.com:username/username.github.io.git'
  branch: 'master'
  # message: [message]
```

此处repo就是之前在Github Pages创建的项目SSH地址。

最后部署到GitHub Pages

```
$ npm install hexo-deployer-git --save
$ hexo deploy
```

部署完成后，再次访问`http://username.github.io`，就可以看到线上的博客了，并且有一篇名为“Hello World”的默认的文章。

至此，通过Github Pages与Hexo搭建博客站已完成，可以进行近一步优化你的博客，如：修改为中文、修改主题、添加评论等等。






