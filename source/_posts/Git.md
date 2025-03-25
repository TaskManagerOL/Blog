---
title: Git
date: 2023-06-24 17:57:48
tags: [工具,迁移]
excerpt: 经典的文件控制工具
categories: 工具使用
---

## 从本地到github简易流程

```bash
//首先对于你的工作文件夹
git init
//添加所有文件或者添加某个文件到缓存区
git add .
//然后commit到本地仓库
git commit -m "本次上传的信息"
//添加远程仓库位置
git remote add origin https://github.com/.......
//修改分支
git branch -m main
//提交
git push -u origin main
```



## Git基础使用

### 初始化

```bash
//git初始化
git init 
//clone仓库，在init之后
git clone <repo> <dir>
//查看git状态
git status
```

### 上传到暂存区

```bash
git add <file>
//上传所有文件就是
git add .
```

### 提交到本地仓库

```bash
//提交到仓库
git commit -m "信息"
//查看提交记录
git log --oneline
```

### 远程仓库

```bash
//查看所有仓库
git remote
//查看所有仓库详细信息
git remote -v
//添加仓库
git remote add <name> https://github.com/.......
//删除仓库
git remote rm <name>
//显示某仓库信息
git show <name>
//修改仓库名字
git rename <old_name> <new_name>
```

### 分支

```bash
//查看分支
git branch
//新建分支
git branch <name>
//修改当前分支
git branch -m <name>
//删除本分支
git branch -d
//创建新分支的同时进入分支
git branch -b
//切换分支命令/返回历史版本命令
git checkout <branch>
//将当前分支合并到目标分支
git merge <new_branch>

//更清晰的切换分支
git switch <branch>
//创建新分支并且切换
git switch -c <branch>
//回到前一个分支
git switch -
```

###  拉取

```bash
git pull <远程仓库名> <远程分支名>:<本地分支名>
```

### 推送到远程仓库

```bash
//提交，一般来说本地分支和远程分支名字相同，所以可以省略冒号及其后面的部分
git push <远程仓库名> <本地分支名>:<远程分支名>
//强制推送
git push -f ...
//设置默认值
git push -u ...

```

### 撤销

```bash
//还原所有未提交的更改，包括工作目录和暂存区的更改
git restore .
//使用该命令会将add到缓存区的文件撤销
git restore --staged <file>
```

### 删除

```bash
//从暂存区和本地文件夹中删除
git rm <file>
//只删除暂存区文件
git rm --cached <file>
//遍历删除文件夹及其下的子文件夹 
git rm -r <file>
//强制删除
git rm -f <file>
```

### 回退

```bash
//回退到某个版本
git reset <version>
//回退到上一个版本
git reset HEAD^
//回退到上上个版本
git reset HEAD^^
//将文件夹中文件一并回退
git reset --hard HEAD^
```

### .gitignore

添加`.gitignore`文件并在其下写上文件路径，就不会被传到github

## Issues

github中可以对别人的仓库添加一个issue

### 提出Issues

点击到库中的issue里，可以添加一个New Issues去对库中某个地方提出问题，此时该issue会带有一个编号 #xxx

### 解决Issues

点击到库中的issue里，右边可以处理你对该issue的设置，同时你下一次解决issue的时候，可以带上 #xxx 代表你解决的是该issue。

## Pull Request

PR相当于你自己去解决别人的代码问题

### 提出PR

+ 点击你想要PR的仓库中的fork，创建一个新仓库用于修改代码。
+ 将项目clone到你的新仓库，并且remote到你想要PR的仓库。
+ 修改，完成后回到你想要PR的仓库页面，点击PR，可以看到有请求可以合并你的仓库到你想要PR的仓库上。
+ 如果还需要进行后续代码编写，本地仓库有两个分支，不能直接删除，需要先Pull才能删除。

### 解决PR

+ Issues和PR同用 # 代表问题。
+ 当收到PR，没问题时，点击merge即可合并。
+ 合并后删除刚刚新增的分支。
+ 回到工作区（文件夹），拉取（Pull）新的文件下来到工作区。

## Tag & Release

```bash
//查看tag
git tag
//增加版本号
git tag -a v1.0.0 -m "消息"
//上传tag
git push --tags
```

Release 可以直接选择 Tag 发行版本。

## Actions

Github Action 就是 “什么时候” + “干什么事情” ，自动化工作流。

### 初始化

在根目录创建`.github`文件夹，再在此文件夹下创建`workflows`文件夹，再在此文件夹下创建`xxx.yml`就会自动开启actions。

### 工作流 & 项目打包部署

在`xxx.yml`文件中写如下自动打包示例代码：

```yml
name: 打包

on: push

jobs:
	npm-build:
		name: 打包
		runs-on: windows-latest
		
		steps:
		- name: 读取仓库
		  uses: actions/checkout@v4
		  
		- name: 安装依赖
		  run: npm install
		  
		- name: 打包操作
		  run: npm run build
```

即可运行。

>  还没学过yml，看起来和脚本差不多的感觉诶。

上面是为了理解，一般使用 New workflow 用模板创建。

需要部署时：

`xxx.yml`内容改为：

```yml
name: 打包

on: push

jobs:
	npm-build:
		name: 打包
		runs-on: windows-latest
		
		steps:
		- name: 读取仓库
		  uses: actions/checkout@v4
		  
		- name: 安装依赖&打包操作
		  run: 
		  	npm install
		  	npm run build
		  
		- name: 部署
		  uses: JamesIves/github-pages-deploy-action@v4
		  witch:
		  	//deploy是部署分支
		  	branch: deploy
		  	//dist是打包文件夹
		  	folder: dist
```

然后找到仓库设置 左侧的page Build and deployment 下Branch选择 deploy 点击 save。

### Docker & secrets 

> 还没学过Docker，但是知道Docker可以打包程序和运行环境，先标记。

生成Docker镜像并推送到Docker仓库里。

+ 先在根目录下创建一个`Dockerfile`，写一些创建镜像的基本操作。
+ 在仓库设置 Secrets and variables 中 Actions下可以设置Repository  secrets。
+ 可以在`Dockerfile`文件中使用 `${{ secrets.name }} `和  `${{ secrets.name }}` 放账号密码。



