---
title: Vue.Config
date: 2023-11-13 14:57:44
tags: [前端,😶‍🌫️]
excerpt: 每次新建项目都得配置不少东西，在这里标记一下防止遗忘。
categories: 技术栈
---

## Vite框架项目创建

```bash
npm create vite@latest
npm install
npm run dev
//(别忘记在package.json中"scripts"对象中"dev"后面把"vite"改成"vite --open")
```

## Vue Router路由安装

```bash
npm install vue-router@4
//安装后别忘记在src下新建一个router子文件夹和index.js、routes.js子文件
```

### index.js（直接复制粘贴即可）

```js
// 导入router所需的方法
import { createRouter, createWebHashHistory } from 'vue-router'

// 导入路由页面的配置
import routes from './routes.js'

// 路由参数配置
const router = createRouter({
    // 使用hash(createWebHashHistory)模式，(createWebHistory是HTML5历史模式，支持SEO)
    history: createWebHashHistory(),
    routes: routes,
})

// 全局前置守卫，这里可以加入用户登录判断
router.beforeEach((to, from, next) => {
    // 继续前进 next()
    // 返回 false 以取消导航
    next()
})

// 全局后置钩子，这里可以加入改变页面标题等操作
router.afterEach((to, from) => {
    // const _title = to.meta.title
    // if (_title) {
    //     window.document.title = _title
    // }
})

// 导出默认值
export default router
```

### routes.js（直接复制粘贴即可）

```js
const routes = [
    {
        path: '/',
        name: 'HOME',
        component: () => import('')
    }
]
export default routes
```

```js
//最后就是别忘记在main.js里添加引入依赖
import router from './router/index.js'
createApp(App).use(router).mount('#app')//.use(router)
```

## APP.vue初始化

```vue
<script setup></script>

<template>
  <router-view></router-view>
</template>

<style scoped></style>
```

## style.css初始化

```css
/* 部分标签修改 */
body {
  margin: 0;
  display: flex;
  place-items: center;
}

#app {
  max-width: 1280px;
  margin: 0 auto;
  text-align: center;
}
```

