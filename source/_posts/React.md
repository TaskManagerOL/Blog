---
title: React
tags:
  - 笔记
  - 前端
categories: 技术栈
excerpt: 著名框架之一
date: 2024-06-24 12:14:35
---

本笔记是基于已有一定前端基础的情况下做的，如果看不懂建议看官方文档，还是看不懂建议上视频平台找博主视频手把手教。

> have fun😗

# Next框架

next对于react教程简单易懂，是我目前见过最友好的文档了，next补全了react的文档可以这么说。它不仅教你自己的脚手架怎么使用，还教你更新node、使用ts及tailwindcss，甚至还会让你跟着他一点点的改代码显示改出来的效果，让你答题恢复注意力，就和哄幼儿园的宝宝一样。

链接[Learn Next.js: Getting Started | Next.js (nextjs.org)](https://nextjs.org/learn/dashboard-app/getting-started)

> clsx库[clsx - npm (npmjs.com)](https://www.npmjs.com/package/clsx) 可以结合JS/TS 条件更换样式

> next 自带的组件库很好用嘞

## 页面路由

对于`page.tsx`，它 是一个特殊的Next.js文件，用于导出 React 组件，并且需要它才能访问路由。

相当于你在app里面创建一个新的文件夹`new`下面放`page.tsx`后，访问页面路由`/new`就可以看到这个页面，他是文件夹形式的路由安排，而vite是将一份新的js文件如`route.js`写上页面的逻辑。

>  next允许在不知道路由名称的时候创建路由，使用方括号`[]`设置。

同样的对于css样式，next使用`layout.tsx`文件进行编写。这样就可以实现主页里的小页面进行更换了。

> 对于/app/layout.tsx，其引用的文件是全局适用的，这被称为`根布局`。

Link组件可以让用户在应用程序中页面链接。

> 值得一提的是为了改善导航体验，Next.js 会自动按路由段对应用程序进行代码拆分。这与传统的 React SPA 不同，在传统的 React SPA 中，浏览器会在初始加载时加载所有应用程序代码。
>
> 按路由拆分代码意味着页面变得孤立。如果某个页面抛出错误，应用程序的其余部分仍将正常工作。

在实际开发中我们经常会遇到需要用到路由name的时候，对于vue我们可以从我们写的路由js文件中找到`$route.path`等方式获取路由名称。而对于react，可以使用`usePathname()`的钩子来实现这个操作。

> 添加 ‘use client’ 在文件顶部可以将此模块机器传递的依赖标记为客户端代码。 这些组件在用户设备上运行，并且可以使用浏览器API和React的状态和效果钩子，相对应的是'use server'。

> tips:在第六章设置数据库那里，部署到vercel上会在seed组件报错，只需要删掉seed目录即可。详见[Issue #768](https://github.com/vercel/next-learn/issues/768)
>
> 同样的，当数据库配置好了之后再下下来/seed路径及其文件然后继续即可。

## 流媒体

流式处理是一种数据传输技术，它允许您将路由分解为更小的“块”，并在它们准备就绪时逐步将它们从服务器流式传输到客户端。

> 在next中loading.tsx是一个特殊的页面，会在对应页面加载时显示。

React Suspense 可以更为精细的控制流媒体。

```tsx
import { Suspense } from 'react';
```

这样做之后就可以用suspense标签包住想要精细化控制显示的路由了。

## 部分预渲染

Next.js 14 引入了部分预渲染的实验版本——一种新的渲染模型，允许在同一路线中结合静态和动态渲染的优势。

```tsx
//next.config.mjs
 
const nextConfig = {
  experimental: {
    ppr: 'incremental',
  },
};
 
export default nextConfig;

//组件
export const experimental_ppr = true;
```

## 搜索

这里采用URL搜索参数，以下是好处：

+ 可添加书签和可共享的 URL：由于搜索参数位于 URL 中，因此用户可以为应用程序的当前状态添加书签，包括其搜索查询和筛选器，以供将来参考或共享。
+ 服务器端渲染和初始加载：可以直接在服务器上使用 URL 参数来渲染初始状态，从而更轻松地处理服务器渲染。
+ 分析和跟踪：直接在 URL 中进行搜索查询和筛选，可以更轻松地跟踪用户行为，而无需额外的客户端逻辑。

接下来我们要做的就是：

+ 获取用户的输入
+ 使用搜索参数更新URL
+ 保持URL和输入同步
+ 更新表

> `URLSearchParams` 是一个 Web API，它提供用于操作 URL 查询参数的实用工具方法。可以使用它来获取参数字符串，而不是创建复杂的字符串文本，例如 `?page=1&query=a`

### 消抖

在我们一开始handleSearch中，加入`console.log`测试，但是在控制台中输入`你好`我们可以看到：

```markdown
n
ni
ni'h
ni'ha
ni'hao
你好
```

> 因为每次敲击键盘的时候都会更新URL，所以每次更新都会查询数据库，这明显是不合适的。

我们采用停止键入延迟固定时间后才运行代码的方式进行消抖。

## 处理错误

对于正常遇到的错误，我们需要对其进行处理。

> 在next中error.tsx是一个特殊的页面，会在对应页面错误时显示。

如果是404页面，我们也许可以进行一些特殊处理。

```tsx
import { notFound } from 'next/navigation';
//判断并调用
notFound();
```

并在根目录下添加not-found.tsx，就在可以404返回状态下触发了。
