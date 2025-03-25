---
title: Pinia
tags: [笔记,前端]
categories: 技术栈
excerpt: Pinia 是 Vue 的专属状态管理库，允许你跨组件或页面共享状态。
date: 2024-03-25 16:31:57
---

# Pinia简介

Pinia 是 Vue 的专属状态管理库，可以同时支持vue2和vue3，它允许你跨组件或页面共享状态。如果你熟悉组合式 API 的话，你可能会认为可以通过一行简单的 `export const state = reactive({})` 来共享一个全局状态。对于单页应用来说确实可以，但如果应用在服务器端渲染，这可能会使你的应用暴露出一些[安全漏洞](https://cn.vuejs.org/guide/scaling-up/ssr#cross-request-state-pollution)。 而如果使用 Pinia，即使在小型单页应用中，你也可以获得如下功能：

- Devtools 支持
  - 追踪 actions、mutations 的时间线
  - 在组件中展示它们所用到的 Store
  - 让调试更容易的 Time travel
- 热更新
  - 不必重载页面即可修改 Store
  - 开发时可保持当前的 State
- 插件：可通过插件扩展 Pinia 功能
- 为 JS 开发者提供适当的 TypeScript 支持以及**自动补全**功能。
- 支持服务端渲染

Pinia其实就是Vuex5，所以他们是一样的东西。

它拥有比MITT更多的功能。而且也没有遇到兄弟组件传值出现的问题。好用。

# Pinia安装

[Pinia官网](https://pinia.vuejs.org/zh/getting-started.html)

Nodejs包管理器下载：

```bash
npm install pinia
```

vite配置

```js
//main.js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
const pinia = createPinia()
createApp(App).use(pinia).mount('#app')
```

# Store

### Store简介

Store (如 Pinia) 是一个保存状态和业务逻辑的实体，它并不与你的组件树绑定。换句话说，**它承载着全局状态**。它有点像一个永远存在的组件，每个组件都可以读取和写入它。它有**三个概念**，[state](https://pinia.vuejs.org/zh/core-concepts/state.html)、[getter](https://pinia.vuejs.org/zh/core-concepts/getters.html) 和 [action](https://pinia.vuejs.org/zh/core-concepts/actions.html)，我们可以假设这些概念相当于组件中的 `data`、 `computed` 和 `methods`。

### Store使用

先创建一个js/ts文件。

```js
//我是直接创到了public目录下  /public/store/user.js
import { defineStore } from 'pinia'
import { ref,computed } from "vue"
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }

  return { count, doubleCount, increment }
})
```

然后直接使用：

```js
import { useCounterStore } from '/public/stores/user.js'
const store = useCounterStore()
console.log(store.count)
```

就行了，感觉比MITT方便不少，store似乎就是一个reactive对象。可以解构。
