---
title: MITT
date: 2023-11-13 14:58:08
tags: [笔记,前端]
excerpt: 一个全局传参的JavaScript库
categories: 技术栈
---

在Vue3中为了优化代码会使用全局事件总线bus去在不同组件之间传值。

首先先安装一下mitt

```
npm install mitt
```

添加一个bus.js的文件里面放这些

```
import mitt from 'mitt'
export const events = mitt()
```

在需要使用bus的组件里引入依赖

```
import { events } from '.../.../bus.js'
```

使用方法主要是三种：

+ emit：想要传出值或函数

  ```javascript
  events.emit('functionName', postValue)
  //其中functionName是你绑定的一个函数名，相当于一个标识，可以在不同组件中靠这个来判定来源和目的地，postValue是你要传的值。
  ```

+ on：想要接受传入值

  ```javascript
  events.on('functionName', (val) => { ... })
  //其中functionName是你绑定的一个函数名，相当于一个标识，可以在不同组件中靠这个来判定来源和目的地，val是你上面传出来的postValue，要干什么自己写在...里。
  ```

  兄弟组件之间使用on会有一个小问题，详见[Problem](https://taskmanagerol.github.io/2024/01/30/Problem/) 

+ off：想要解绑事件

  ```javascript
  //某些情况可能要解绑
  events.off("functionName")
  ```

  
