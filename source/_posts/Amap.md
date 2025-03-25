---
title: Amap
tags:
  - 工具
  - 前端
categories: 工具使用
date: 2024-04-08 17:39:27
excerpt: 高德API小小标记一下
---

## 高德地图api使用

[概述-地图 JS API 2.0|高德地图API (amap.com)](https://lbs.amap.com/api/javascript-api-v2/summary)

### Vue 使用前准备

+ 首先登录高德，注册成为开发者，创建key，服务平台选择Web端（JS API）。

+ 进入工作区：

  ```shell
   npm i @amap/amap-jsapi-loader --save
  ```

+ 在需要使用的组件下：

  ```js
  import AMapLoader from '@amap/amap-jsapi-loader';
  ```

+ 示例代码

  ```vue
  <script setup>
  import { onMounted, onUnmounted } from "vue";
  import AMapLoader from "@amap/amap-jsapi-loader";
  
  let map = null;
  
  onMounted(() => {
    AMapLoader.load({
      key: "", // 申请好的Web端开发者Key，首次调用 load 时必填
      version: "2.0", // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
      plugins: ["AMap.Scale"], //需要使用的的插件列表，如比例尺'AMap.Scale'，支持添加多个如：['...','...']
    })
      .then((AMap) => {
        map = new AMap.Map("container", {
          // 设置地图容器id
          viewMode: "3D", // 是否为3D地图模式
          zoom: 11, // 初始化地图级别
          center: [116.397428, 39.90923], // 初始化地图中心点位置
        });
      })
      .catch((e) => {
        console.log(e);
      });
  });
  
  onUnmounted(() => {
    map?.destroy();
  });
  </script>
  
  <template>
    <div id="container"></div>
  </template>
  
  <style scoped>
  #container {
    width: 100%;
    height: 800px;
  }
  </style>
  ```

### Vue 水印去除

在index.html中加上：

```html
<style>
    .amap-logo {
      display: none;
      opacity: 0 !important;
    }
  
    .amap-copyright {
      opacity: 0;
    }
  </style>
```

