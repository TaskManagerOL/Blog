---
title: Problem
date: 2024-01-30 20:05:30
tags: 😶‍🌫️
categories: 随笔
excerpt: 这里是一些我遇到的问题集合
sticky: 100
---

# Git -> Time out

+ 背景：

  用于解决git上传Time out的情况。
  无论是用git的push还是hexo的deploy，经常会出现Time out的情况。

+ 解决方法一：

  重启+开开关关梯子+更换网络

  > 这个的话完全看玄学，我之前经常开开关关梯子+换网就解决了，很抽象。

+ 解决方法二：

  ```
  git config --global https.proxy //使用代理
  git config --global --unset https.proxy //取消代理
  ```

  > 这个我用过很多很多很多很多次，都把他背下来了，有时候确实有用

+ 解决方法三：

  在传TS笔记的时候家里的网死活传不上去，尝试过网上所有的方法了整了一下午，很抽象的是可以去外网。

  那不妨直接用git自己内置的update flies，即拖动上传。

# TypeScript -> "Could not find a declaration file for module ‘xxx.js’. ‘xxx.js’ implicitly has an ‘any’ type.

+ 背景：

  尝试使用TS的时候呢，遇到了一些问题，在main.ts中引用已经写好的js文件时(旧版本已经写好的配置文件，详见blog中的vue.config)发生报错，错误代码为ts(7016)，一眼ts和原生起冲突了。

+ 解决方法一：

  我没试过这个方法，但是Vue2的可以试试（也许）。

  ```typescript
  //将import引入改为require引入
  import module from "module.js"
  //改为=>
  const module = require('module.js')
  ```

  为啥我没试过呢，因为在Vue3中，require语法已经不能使用了，在Vue3版本中，直接使用上述的require语法会导致报错，提示require不是一个函数。这是因为Vue3及以上版本使用了ES Module语法，不再支持使用CommonJS语法来引入模块。

  > 小知识：require和import的性能比较
  >
  > `require` 的性能相对于 `import` 稍低。
  >
  > 因为 `require` 是在运行时才引入模块并且还赋值给某个变量，而 `import` 只需要依据 `import` 中的接口在编译时引入指定模块所以性能稍高

+ 解决方法二：

  也是我自己琢磨出来的方法，适用性比较低吧可能。

  问题既然出在 TS 和 JS 对接上，那我向上兼容，把 JS 文件更新成 TS 的不就完事了，在修改引用的文件后缀和文件内容后果然还是不报错了。

+ 解决方法三：

  ```typescript
  //先在项目目录(也就是和众多config同目录)下创建一个modules.d.ts
  //modules.d.ts (modules可以自己取名字)
  declare module '*.js';
  
  //然后在 tsconfig.json 中的 "include" 配置下添加一个 "modules.d.ts"
  // tsconfig.json
  "include": ["src/**/*.ts", "src/**/*.tsx", "src/**/*.vue", "module.d.ts"]
  
  //然后在你的main.ts中用正常的import xx from 'xx.js' 即可
  //main.ts
  import xxx from 'xx.js'
  ```

  推荐使用的方法，无论是你自己的Js文件还是引的依赖包都可以从这里引入到main.ts中，如果引依赖。

  ```typescript
  //modules.d.ts
  declare module '依赖名';
  
  //main.ts
  import xxx from '依赖名'
  ```




# TypeScript  -> 代码未错误但出现错误提醒（编辑器为vscode）

+ 背景：

  在写TS项目的时候发现出了报错提示，但是我是直接粘的element-plus的代码，报的错也很奇怪，网上搜也解决不彻底，最抽象的是项目能跑。

>  后面才知道是因为eslint（vscode扩展-用于检查js书写错误）

​		遂去找ts检查扩展，发现根本找不到。

> 好像目前就没有好用的ts语法检查扩展

+ 解决方法一：

  首先这个方法我是行不通的，但是我觉得可能是我某个扩展的问题。

  打开设置 -> 搜索validate ->下面找到并设置禁止typescript验证 -> 重新启动编辑器。

+ 解决方法二：

  直接让他不检查语法错误。

  ```typescript
  在script标签下加上这行注释。注意，是注释！！
  
  // @ts-nocheck
  ```

  这样ts代码就不会报错了，但也检查不出来问题了，至少不难受了看着。

+ 解决方法三：

  没有三了，按道理来说网上是有某种关于eslint配置可行的，但是我配了两个都不行。我以后找到了再来更新吧🤕



# IPv4&IPv6 -> "http proxy error"

之前在打ICT的时候就遇到过类似的问题，当时以为是es6的fetch哪里没配置好，后面换成axios就可以了，但实际不是这样。今天在打服创的时候又遇到这玩意了。

+ 背景

  跨域，localhost但是不同端口跨域。

  我前端config文件明明配置得好好的，但是f12永远报我接的是前端跑着的端口，代码编辑器上更是出一个http proxy error，我就对着一直改啊改啊，发现一直还是这个报错，后面找到是后端的问题。

+ 解决方法：

  我遇到的问题实际上是后端允许的网络协议和前端发出来的网络协议不同，用的python后端，那边是给的一个IPv4接口，前端用的是IPv6，结果接不上，解决方法就是更改后端接口使用的网络协议。

  ```python
  #此处就放后端部分代码了，语言是python
  if __name__ == '__main__':
      app.run(host = '0.0.0.0',port = 5000)
      #在本地的端口5000运行，配置IPv4 IPv6都可以使用，不然前端报错http proxy error
  ```




# Headers -> 400(Bad REQUEST)`文件上传`

+ 背景：

  是需要上传一个文件，又是经典的Postman可以前端不行。

+ 解决方法：

  最后发现是Headers的问题，大家都说：

  ```typescript
   headers: {
        'Content-Type': 'multipart/form-data'
      }
  ```

  上传文件要这样子配置，但是实际上我把它整个headers删了反而成功了，原因是什么呢？

  > 发现去掉 Content-Type 的请求头部多了一个 boundary ，查查。
  >
  > **Boundary 是一种用于分隔多个实体（如文件、表单字段等）的标识符**。 它通常用于 multipart/form-data 类型的请求中，用于将多个部分组合在一起，并指示它们的边界。

  原来`POST`请求上传文件的时候是不需要自己设置 Content-Type，会自动给你添加一个 boundary ，用来分割消息主体中的每个字段，如果这个时候自己设置了 Content-Type， 服务器反而不知道怎么分割各个字段。



# Javascript&CSS -> label点击事件阻止

+ 背景：

  以下HTML：

  ```html
  <label>
  	<div @click="console.log(1)"></div>
  </label>
  ```

  怎么才能实现点击div但是不触发label的点击事件呢？我找了很多方法CSS的还有JS的都不太行，CSS的话是想hover到div上时label的点击事件取消，但是又会连带到div里，用div包label和div加absolute又很麻烦因为还有别的需求。JS是想使用stopPropagation阻止冒泡，但是label的点击事件不受影响。

+ 解决方法：

  改成这个结构：

  ```html
  <div @click="inputFocus">
  	<div @click="stopFocus()"></div>
  </div>
  <input ref="inputRef">
  ```

  ```js
  const inputFocus = () => {
      inputRef.value.click();
  }
  
  const stopFocus = (event) => {
      //业务函数
      ...
      //阻止冒泡
      window.event.stopPropagation();
  }
  ```

  这样就行了div是可以使用stopPropagation函数的。

  > 但是为什么label不行呢，全网查找了一下没找到。
  >
  > 去MDN看了一下对于这个标签的描述：
  >
  > 不要在 `label` 元素内部放置可交互的元素，这样做会让用户更难激活/触发与 `label` 相关联的表单输入元素。



# HTML&Javascript -> "input标签使用"

+ 背景：

  需求是上传图片、显示、点icon删除、点icon预览。

  但是卡在删除上面了，有一个小bug——每次点击icon删除后就会没办法上传之前上传的那一张图片。

+ 解决方法：

  其实很简单只不过说我把input标签隐藏起来了，每次删除都是把显示的图片删掉，原本传到input里图片的没删掉。

  但为什么还要写到Problem中呢？

  因为我发现input里图片删除也很有意思：

  ```vue
  <template>
  	<input ref="inputRef">
  </template>
  <script>
      const inputRef = ref('')
      //inputRef.value 对应的是他的页面标签
      //inputRef.value.value 对应的是他的图片(路径)
  </script>
  ```




# Vue -> "addEventListener is not a function"

+ 背景：

  在引一个3d canvas库，但是一直报这个错误，后面找到是vue的ref问题，其实报这个错误是因为一直都获取不到标签。

+ 解决方法：

  添加onMounted函数，是这样的：

  + Vue 会首先解析和执行组件中的 `<script>` 部分，这包括响应式数据、计算属性、监听器、方法等的定义。
  + 接着会编译模板，将数据绑定到视图中，渲染生成的 HTML。这一步通常是在`beforeCreate` 和 `created` 阶段中完成，因为 Vue 需要在渲染之前准备好数据、计算属性等。
  + `onMounted` 生命周期钩子函数是在 Vue 3 中的 Composition API 中使用的，它在组件挂载到 DOM 后执行。在 Vue 3 的生命周期中，类似于 `onMounted` 的生命周期钩子函数会在合适的时机被调用。这意味着它在组件渲染后执行。

  因为定义的ref在script中还未访问到DOM元素，就自然还为空，为空的话后续函数就没办法执行咯。



# MITT -> onAPI使用问题

+ 背景：

  在兄弟组件中调用全局事件总线MITT的时候，emit和on都是可以使用的，但是：

  ```js
  const test = ref()
  event.on('name',(val)=>{
      console.log(val);//可以得到值
      test.value = val;
      console.log(test.value);//可以得到值
  })
  console.log(test.value);//不可以得到值
  ```

  这就很抽象了，那我调用on的意义不久完全失去了嘛。

  经过尝试ref -> reactive、生命周期等等都没用。

  讨论了一下能看出是渲染顺序问题或者深拷贝问题，但是就是不知道怎么解决。

+ 解决方法一：

  最原始的方法就是存到localstorage里面🤣。

+ 解决方法二：

  换用pinia Vue状态管理库。

+ 解决方法三：

  先用emit传到父组件中，然后再用defineprops传到目的组件中。



# HTML&CSS -> fixed状态盒子消失

+ 背景：

  Header盒子加了一个fixed样式，但是不见了。

+ 解决方法：

  加一下z-index。



# Pack -> 打包的时候index.html无法打开

+ 背景：

  需要把写好的文件给队友调试，但是发现index.html无法打开。

+ 解决方法：

  在vite.config.js下：

  ```js
  //添加如下代码
  export default defineConfig({
    plugins: [vue()],
    base:'./'
  })
  ```

  然后index.html不要直接打开，会有跨域问题，使用vscode 的`Live Server`插件打开。

# CSS -> 高度非固定造成的样式错误

+ 背景：

  比如一个for循环渲染div，然后造成的高度比预设值多，那就会多出来一些白色的。

+ 解决方法：

  可以包两层div，外层heightauto，内层height100vh，然后在写。

# 文件传输 -> 发送文件服务器报500

+ 背景：

  在打比赛的时候发送为JSON格式的文件不行，服务器报500，Postman也不行

+ 解决方法：

  JSON的key设置为files。


# 服务器搭建 -> 如何快速开始搭建一个服务器

还不是很熟悉服务器相关的操作，所以写一下拿到一个新的服务器相关的操作。

先进root，拿到最高权限。

```shell
sudo passwd root
```

输入两次密码（密码是看不到的，但是其实已经输入了）

```shell
su
```

再输入两次密码。

下载apt-get：

```shell
sudo apt-get install ssh
```

下载nginx，同时检查nginx版本以及启动一下nginx：

```shell
apt-get install nginx
nginx -v
service nginx start
```

之后进入浏览器，在Ubuntu系统中输入`127.0.0.1`，在其他电脑中输入`该服务器的ip地址`即可访问。

在`/var/www/html`目录下：

```shell
sudo git clone <repoName>
```

然后调整配置：

```shell
sudo nano /etc/nginx/sites-enabled/default
```

把`server->root`重写为新clone的目录下。

重新启动nginx：

```shell
sudo nginx -t
sudo systemctl restart nginx
```



# 服务器搭建 -> 如何部署SSL证书

经过备案，获取到SSL证书之后，下载到本地。

先通过ssh传文件到服务器：

```shell
ssh root@<ip>
```

然后从本地传文件，将证书文件传到nginx安装目录下（默认/etc/nginx）：

```shell
scp -r <上传文件目录地址> root@<ip>:<服务器安放地址>
```

然后配置nginx：

```shell
#将端口设置为443
sudo nano /etc/nginx/sites-enabled/default

#修改配置
sudo nano /etc/nginx/nginx.conf

#在http间添加
server {
     #SSL 默认访问端口号为 443
     listen 443 ssl default; 
     #请填写绑定证书的域名
     server_name <>; 
     #请填写证书文件的相对路径或绝对路径
     ssl_certificate xxx.crt; 
     #请填写私钥文件的相对路径或绝对路径
     ssl_certificate_key xxx.key; 
     ssl_session_timeout 5m;
     #请按照以下协议配置
     ssl_protocols TLSv1.2 TLSv1.3; 
     #请按照以下套件配置，配置加密套件，写法遵循 openssl 标准。
     ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
     ssl_prefer_server_ciphers on;
     location / {
         #网站主页路径。此路径仅供参考，具体请您按照实际目录操作。
         #例如，您的网站主页在 Nginx 服务器的 /etc/www 目录下，则请修改 root 后面的 html 为 /etc/www。
         root html; 
         index  index.html index.htm;
     }
 }
```

再运行一次

```shell
nginx -t
nginx -s reload
```

# CI/CD -> Github Page

github action+page 同仓库不同分支集成部署
在`.github`文件下添加`workflows`添加`hexo-deploy.yml`

```yml
name: Hexo Deploy

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Setup Node
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Initialize submodules
      run: git submodule init
      
    - name: Update submodules
      run: git submodule update

    - name: Build Hexo
      run: npm run build 

    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./public 
        publish_branch: [仓库分支]
```

然后如果使用主题的话还得在根目录下添加一个`.gitmodules`

```
[submodule "themes/typo"]
    path = themes/typo
    url = [使用主题的链接]
```

最后还要打开`Setting`->`Actions`->`General`->`Workflow permissions`->`R&W permissions`
