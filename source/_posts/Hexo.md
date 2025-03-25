---

title: Hexo
date: 2023-06-06 16:12:38
tags: [工具,速通]
excerpt: 快速搭建Blog的框架
categories: 工具使用
---

# [Hexo](https://hexo.io/zh-cn/)

使用hexo搭建一个属于自己的Blog非常快捷，对于有web基础的同学可以1~2h内完成搭建并熟练使用。

## Install

建立一个存放blog的文件夹，然后使用以下指令进行全局安装。（使用cmd并定位到该目录下）

```
$ npm install -g hexo-cli
```

安装 Hexo 完成后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。(<folder>是文件夹的名称，用于后续工作)

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

## Basic

如果有部署网站，所有操作之后需要执行

```
$ hexo g
$ hexo deploy
```

上传 **笔记**

### New

可以在目标文件夹执行下列命令来创造一幢新的 **笔记** 。

```
$ hexo new [layout] <title>
```

其中 **layout** 是笔记的类型，有 **post** 、 **page** 、 **draft**

一般只使用且默认是 **post** 。

建立后在在source/_post中修改markdown即可。

**笔记** 创建后有以下配置项，可以参考修改。

| 参数              | 描述                                                         | 默认值                                                       |
| :---------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `layout`          | 布局                                                         | [`config.default_layout`](https://hexo.io/zh-cn/docs/configuration#文章) |
| `title`           | 标题                                                         | 文章的文件名                                                 |
| `date`            | 建立日期                                                     | 文件建立日期                                                 |
| `updated`         | 更新日期                                                     | 文件更新日期                                                 |
| `comments`        | 开启文章的评论功能                                           | true                                                         |
| `tags`            | 标签（不适用于分页）                                         |                                                              |
| `categories`      | 分类（不适用于分页）                                         |                                                              |
| `permalink`       | 覆盖文章的永久链接，永久链接应该以 `/` 或 `.html` 结尾       | `null`                                                       |
| `excerpt`         | 纯文本的页面摘要。使用 [该插件](https://hexo.io/zh-cn/docs/tag-plugins#文章摘要和截断) 来格式化文本 |                                                              |
| `disableNunjucks` | 启用时禁用 Nunjucks 标签 `{{ }}`/`{% %}` 和 [标签插件](https://hexo.io/zh-cn/docs/tag-plugins) 的渲染功能 | false                                                        |
| `lang`            | 设置语言以覆盖 [自动检测](https://hexo.io/zh-cn/docs/internationalization#路径) | 继承自 `_config.yml`                                         |

### Delete&Change

直接在source/_post中修改/删除markdown即可

删除之后输入一次以下命令

```
$ hexo clean
```

## LocalHost

在搭建有关 笔记 后，需要进行展示

先生成静态文件（每次更新 **笔记** 时都需要此步，便于页面部署，类似于vue中的dist）

```
$ hexo g
```

在本地使用服务器展示使用如下指令即可：

```
$ hexo server
```

接着就可以在网址为  http://localhost:4000/  访问到

# Config

Hexo中用户可修改的配置放在 `_config.yml` 文件中，可根据官网描述修改。

其中基础使用需要修改的项目有 

+ title、author、language （用户信息）
+ theme （自定义主题）
+ deploy （简易部署）

## [Themes](https://hexo.io/themes/)

在上述网站中可以寻找自己喜欢的主题，点击大图可以预览，点击蓝字可以进入该作者的仓库。

在**hexo**目录下的**themes**文件夹下打开**git bash**，输入以下命令，下载主题:

```text
git clone 复制主题的网址
```

配置`_config.yml`文件 修改theme 改为主题的名字

在hexo目录下，打开git bash，输入以下命令，清除缓存，生成静态文件，查看效果

```text
hexo clean
hexo g
hexo s
```

## Deploy

| 参数      | 描述                                                         | 默认                                                         |
| :-------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `repo`    | 库（Repository）地址                                         |                                                              |
| `branch`  | 分支名称                                                     | `gh-pages` (GitHub) `coding-pages` (Coding.net) `master` (others) |
| `message` | 自定义提交信息                                               | `Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}`)            |
| `token`   | 可选的令牌值，用于认证 repo。用 `$` 作为前缀从而从环境变量中读取令牌 |                                                              |

## Index_generator

需要修改每一页的笔记数量可以从`per_page`中修改。

需要修改排序顺序可以从`order_by`中修改，默认`-data`即日期的倒序，可以修改成其他配置项例如`-updated`即修改日期的倒序。

# Deployment

## Git Page

页面托管可以使用github，完美符合静态Blog的需求。

在 **仓库Repositories** 中新建一个 **仓库** ，名称为 **你的githubID.github.io** 点击创建。

接着在创建的文件夹的子文件夹public中使用git连接该仓库，push所有的文件。

等待几分钟页面部署，即可在 **https://你的githubID.github.io** 中访问到。

为了方便 **笔记** 搭建修改 需要在目标文件夹中运行以下命令

```
$ npm install hexo-deployer-git --save
```

在配置文件`_config.yml`中更改

```
deploy:
  type: git
  repo: <repository url> #https://github.com/TaskManagerOL/TaskManagerOL.github.io
  branch: [branch]
  message: [message]
```

完成配置后每次只需执行

```
$ hexo g
$ hexo d
```

即可快速上传文件

