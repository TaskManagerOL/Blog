---
title: MiniProgram
tags:
  - 笔记
  - 前端
categories: 技术栈
excerpt: 小程序就是依托，我说的。
date: 2024-04-30 19:56:30
---

发现运行打不开，说要配置好小程序的AppId，一个身份证号、一个手机号只能注册5个小程序。

> 管理员身份验证还卡了我一下，说是要重新绑定一遍银行卡，成了。

uniapp运行又打不开，要到微信开发者工具那里设置端口开放，全部关掉重开才行。

想用element-plus 好，他不给用；想用pinia，好，还是报错，刚刚问了一下，tailwind也是不能用的。哈哈。

去网上搜索了一下，原来uniapp本来就没什么好用的UI库，难绷。uniapp的风评更是依托。看到这我打算直接转回原生开发平台开发了。

哈哈。原本以为可以爽复制粘贴的项目，重构吧。

## Config

### 页面路由

app.json下pages配置，页面内使用navigarto标签进行跳转，一个文件夹下的wxml、wxss、js直接放一起打包了。

## Promble

### 阿里icon引入问题

问题一：阿里的icon引不了，需要去icon库里下载，然后将download好的文件放入工作区，新建一个`iconfont.wxss`复制`iconfont.css`的内容。在`app.wxss`中`@import`引入`iconfont.wxss`。

还需要把最新的链接`@font-face`复制粘贴替换掉

```html
//在wxml文件中 iconfont表示iconfont.wxss中默认引入源 icon-name表示图标类名，可以在下载的包的html中查看
<i class="iconfont icon-name"></i>
```

更新的时候要把文件替换，还要把在线链接换掉iconfont.wxss的在线链接换掉。

### JS文件引入问题

引入JS文件需要让文件名大写。

### 修改/初始化变量及打印

```JS
//想要在success回调函数中改变data中的数据要
success: (r) => {
    this.setData({
        console.log(1)
    })
}
//在主函数或者某个函数中打印要
console.log(this.data)
```

```js
//使用函数初始化data里的数据
onLoad:function(){
	init()//初始化你data的操作
	this.setData({
	  dataName:this.data.dataName
	})
} 
```

### div能否代替view

用div不用view的话盒子撑不开，比如你已经设置了w&h，但他还是会没有大小

### 点击传参问题

小程序点击不能在函数后面加括号传参，要写个`data-xxx`然后在`e.currentTarget.dataset.xxx`里获取

### 云开发路径获取问题

小程序的云开发 不可以读取服务器中的文件结构 只能上传下载文件和查某个文件的路径

### 云函数调试失败问题

云函数不能调试是因为你还要在该函数的目录下下载依赖

> 也就是说一个函数一个依赖 wtf 这得多大，不知道是我弄错了还是怎么样，但是这个解决方法是我发现的唯一解。

## Components

### 高德地图

[入门指南-微信小程序插件 | 高德地图API (amap.com)](https://lbs.amap.com/api/wx/gettingstarted)

logo隐藏找了几篇都不行，决定overflowhidden完事。

### 高德定位app.json配置

```
"permission": {
    "scope.userLocation": {
      "desc": "你的位置信息将用于小程序位置接口的效果展示"
    }
  },
  "requiredPrivateInfos": [
    "chooseLocation",
    "getLocation"
  ]
```
