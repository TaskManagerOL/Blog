---
title: TailwindCSS
date: 2023-06-29 10:31:19
tags: [工具,速通,前端]
excerpt: CSS框架，减少很多代码量，但是不便于维护。
categories: 工具使用
---

# Tailwindcss介绍

Tailwindcss是一种简单好用的css框架，我们在项目中经常遇见只需要赋一次样式的div。

要么在div上写class后再到css部分去修改样式，这样会相当麻烦（前端人想要6块屏幕呜呜呜），需要上下滑动或者分屏什么什么的。

要么就在div中使用style去进行修改，但是这样会有两个问题：一个是div中的style不可以配合vscode的插件进行一个自动补全，需要自己去记。另一个是很长很繁杂。

Tailwindcss就可以解决这样的问题，灵活、没有运行时的负担。

配置很简单，配置和学习使用半小时可以完成。

# Tailwindcss快速入门

[Framework Guides - TailwindCSS中文文档 | TailwindCSS中文网](https://www.tailwindcss.cn/docs/installation/framework-guides)

此处点击选择进入相应的前端框架（我使用的Vite，然后呢进去有vue和react，一开始我没看见用的react配置，然后就没成。）

然后文档写得很详细了，缺点是他的中文文档似乎没有完全中文化，需要自己进行一个翻译。

大概使用就是

```html
<h1 class="text-3xl font-bold underline">Home</h1>
```

## Vite快速配置

```bash
//在工作区安装tailwindcss
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

```js
//新创建的tailwind.config.js下复制如下代码
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

```css
//在style.css中加入
@tailwind base;
@tailwind components;
@tailwind utilities;
```

