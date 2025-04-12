---
title: Interview
tags:
  - 😶‍🌫️
categories: 随笔
excerpt: 面试问题集合
date: 2024-08-31 16:17:29
sticky: 100
---

# 面试技巧

## 简历准备

Boss是不能先发送简历附件的，要填写线上简历+打招呼内容。

## 网申

HR一般会在上午9点半左右以及下午两点左右打开邮箱，在上午11点、下午三点左右通知你面试；每周二、周五看邮箱的几率稍大。HR的工作顺序是：查看并筛选主动投递简历→看平台推荐人才简历→主动检索简历，打招呼后正常发简历就行。

> 您好，我对贵司xx职位很感兴趣，请您看下我的简历，如果合适可以随时联系我，谢谢。
>
> （发送简历）

若已读未回，可能简历处于合适和不合适之间，可以做以下处理：

> HR您好，我非常看好贵司机会，此前投递简历后，发现您已读未回，可能是您没来得及处理，也可能是我的简历没有通过筛选，我想确认一下，希望能得到您的回复。谢谢！
>
> 以下是我的微信和电话，如方便，您可以直接给我电话。盼复。
>
> （发送微信和电话）

若还是已读不回，应该是不合适了，如果还是很想投的话可以考虑找到HR电话致电。

## 个人介绍

面试官您好，很荣幸参加本次面试。

我叫xxx，今天来面试贵司的前端开发实习生岗位，接下来我做一个简单的自我介绍。

我是xx届的毕业生，就读xx大学的计算机与信息安全学院，在大学期间自学了Web前端及其相关技能。大一下学期的时候在xxxxx找到一份前端开发的线上实习。

在实习的时候，主要使用的技术栈和工具就是vue3+element plus，工作内容就是和其他前端一起写前端页面，我是负责写数据管理等页面或者组件，然后通过git平台上传整合，周期交任务写报告之类的，积攒了不少经验。

最近的项目是我自己写的一个TODO平台，前后端UI设计服务器部署都是我自己做的。之前有团队协作做过小程序项目，用过uniapp但最后在微信开发者平台开发的。

大学期间也还做过不少其他项目，大部分是在比赛中做的，也拿到了例如网挑国奖的成绩。在学院里担任科技协会主席，逻辑清晰，善于沟通。

以上就是我的大致情况，谢谢。

# 技术栈

## Vue

### VUE3项目目录结构

```
| node_modules					--项目依赖
| public      					--公共文件夹
---| favicon.ico				--网站图标
| src         	    			--源文件目录
---| assets					    --静态文件
	---| utils				    --工具类JS
	---| api				    --接口类JS
---| components					--组件
---| router						--路由配置
---| store						--状态管理器
---| views						--视图文件，与路由结构对应
---| App.vue					--根组件
---| main.js 					--入口文件
| index.html					--入口html
| package.json					--命令配置及依赖管理
| package-lock.json				--依赖版本及更完整的依赖树
| README.md						--说明文件
| vue.config.json 				 --代理、打包等配置文件
```

---

> **public和assets区别：**
>
> ​	同样用于存放静态文件的文件夹。由于vue-cli、vite等工具打包时，public下的文件会原封不动的添加到dist中，而assets下的文件会被合并压缩。
>
> ​	两者的区别是public下一般用于放有更新需求的第三方插件、图片且需要使用绝对路径来引用(否则会warning)，而assets下适合用于存放项目中所必须的图标、JS文件只支持相对路径。[相关文档](https://vitejs.cn/vite3-cn/guide/assets.html#importing-asset-as-url)

---

> **有了package.json为什么还需要package-lock.json：**
>
> ​	前者声明依赖的种类而后者决定实际安装的版本，使用`npm install`时就是根据package-lock.json进行安装。

## JavaScript

### ECMA-262标准化语言规范

> ### ECMAScript和Javascript的区别:
>
> ​	ECMAScript是JavaScript的核心语言规范，而JavaScript则是基于这些规范的具体实现，包含了更多的功能和API，以便在浏览器和其他环境中运行。

```markdown
ES1（1997年）
+ 基于Netscape的JavaScript 1.1。

ES2（1998年）
+ 与ISO/IEC 16262标准保持一致。

ES3（1999年）：
+ 正则表达式：引入了正则表达式支持。
+ 更好的字符串处理：增加了新的字符串方法。
+ 控制语句：添加了try/catch异常处理。
+ 其他改进：包括更严格的错误定义和数字格式化。

ES5（2009年）：
+ 严格模式：提供了更严格的错误检查。
+ JSON支持：内置了对JSON的支持。
+ Array方法：如forEach、map、filter等。
+ Object方法：如Object.keys、Object.defineProperty等。

ES6（2015年）：
+ 箭头函数：简化了函数表达式。
+ let和const：引入了块级作用域变量。
+ 模板字符串：支持多行字符串` ` 和内嵌表达式${ }。
+ 类和模块：引入了类和模块系统。
+ Promise：用于处理异步操作。

ES7（2016年）：数组includes方法、指数运算简化
+ Array.prototype.includes()：检查数组中是否包含某个元素。
+ 指数运算符：简化指数运算为双星号。

ES8（2017年）：简化异步、对象方法优化、字符串填充方法
+ Async/Await：简化异步代码。
+ Object.values() 和 Object.entries()：返回对象的值和键值对数组。
+ String padding：字符串填充方法。

ES9（2018年）：
+ 异步迭代器：支持异步数据流处理。
+ Rest/Spread属性：（...）扩展对象的解构赋值和扩展运算符。

ES10（2019年）数组/对象/字符串处理方法增加
+ Array.prototype.flat() 和 Array.prototype.flatMap()：数组扁平化方法。
+ Object.fromEntries()：将键值对列表转换为对象。
+ String.prototype.trimStart() 和 String.prototype.trimEnd()：去除字符串开头和结尾的空白字符。

ES11（2020年）：BigInt、空值合并、动态导入模块、可选链
+ BigInt：支持任意精度的整数。
+ 动态导入：按需加载模块。
+ 空值合并运算符（??）：处理null或undefined。
+ 可选链运算符（?.）：简化深层嵌套对象属性的访问。

ES12（2021年）：逻辑赋值运算、字符串匹配方法
+ 逻辑赋值运算符（&&=、||=、??=）：结合逻辑运算和赋值操作。
+ String.prototype.replaceAll()：替换字符串中所有匹配的子串。
+ Promise.any()：返回第一个成功的Promise。

ES13（2022年）顶层await、类字段声明初始化
+ 顶层await：在模块顶层使用await。
+ 类字段声明：简化类中字段的声明和初始化。

ES14（2023年）数组方法优化
+ Array.prototype.toSorted()：返回排序后的数组副本。
+ Array.prototype.toReversed()：返回反转后的数组副本。
+ Array.prototype.toSpliced()：返回删除或替换元素后的数组副本。

ES15（2024年）symbol描述、匹配字符串索引
+ RegExp Match Indices：提供匹配子字符串的索引。
+ Symbol.prototype.description：返回Symbol的描述。
```

### for in和for of

for in用于循环一个对象的可枚举属性，可以用来遍历对象的键，数组的索引等。

for of用于循环一个可迭代对象的值。

> 对象不能直接用for of遍历，因为他不是一个可迭代对象，可以用Object.values转化为数组再用for..of循环，或者用Object.entries将对象转化为可迭代对象再用for..of循环

### == 和 ===的区别

在使用`==`时会默认使用隐式转换改变数据类型，`===`的时候不会。

null和undefined只能彼此相等，其他情况均不相等。

```JS
null == undefined // true
null == false // false
undefined == false //false 
```

### 闭包（Closure）

> 不说废话，出个实战题目：写一个函数，每调用一次输出的数字比上一次加一。

闭包的翻译好啊，原来的含义是：在封**闭**的作用域中，**包**含另一个作用域。

当我们创建一个函数A中再**创建**一个函数B的时候，B中可以使用在A初始化的数据——这就是闭包。

也就是说，闭包可以让你在一个内层函数中访问到其外层函数的作用域。

而且呢，还可以在外部函数执行完毕之后，仍然访问这些变量，这个就很牛了。

闭包一般拿来干啥呢？

#### 延长变量生命周期

这个就是我刚刚问的例子了

```JS
//例子1
const Counter = () => {
    let num = 0
    return () => {
        num++
        console.log(num);
        
    }
}

newCounter() /* 输出1 */
newCounter() /* 输出2 */

//例子2
function getArea(width) {
    return height => {
        return width * height
    }
}
const getTenWidthArea = getArea(10)
// 之后碰到宽度为10的长方形就可以这样计算面积
const area1 = getTenWidthArea(20)
// 而且如果遇到宽度偶尔变化也可以轻松复用
const getTwentyWidthArea = getArea(20)
```

#### 创建私有变量

立即调用函数表达式：一种编程模式，定义一个函数后立刻执行他。格式如下：

```js
(function () {
// 函数体
})(/* 传入的值 */);

(function () {
// 函数体
}(/* 传入的值 */));

(() => {
// 函数体
})(/* 传入的值 */);
```

私有方法/变量：面向对象编程的概念，指只能在定义它的类或者对象内部访问的方法。目的是封装代码逻辑（防止从外部直接调用或修改），提高代码安全性。就好像你要点火才能运行汽车，点火是公用方法，而里面的齿轮动是私有方法。

```JS
const Counter = (() => {
    let num = 0 //私有变量
    const fn = () => {//私有方法
        return num+2
    }
    return {//公有方法
        value:()=>{
            return num
        },
        add:()=>{
            return fn()
        }
    }
})()
console.log(Counter.value()); /* 输出0 */
console.log(Counter.add()); /* 输出2 */
```

### 作用域及作用域链

作用域决定了代码区块中变量及其他资源的可见性，一般将作用域分为`全局作用域`、`函数作用域`、`块级作用域`，作用域在变量被创建好的时候就确定了，不会随着执行的时候改变。

作用域链是指你需要调用变量的时候，会先从局部作用域寻找，一直往上直到全局作用域。

全局作用域：不在任何函数或者大括号中声明的变量，可以在程序的任何位置访问。

函数作用域：也叫局部作用域，是在函数内部声明的，不能在函数之外访问（除了闭包）

块级作用域：ES6中引入了`let`&`const`，这两者只能在大括号内访问，大括号外不可以访问。

```js
var globalValue = "1"
function test() {
 var functionValue = "2"
}
test()
{
 let blockValue = "3"
	log(blockValue)//"3"
}

log(globalValue)//"1"
log(functionValue)// 报错
log(blockValue)//报错
```

### this

`this`是函数的一个运行时自动生成的内部对象，只能在函数内使用，指向最后调用它的对象。

#### 绑定规则

优先级：new绑定优先级 > 显示绑定优先级 > 隐式绑定优先级 > 默认绑定优先级

+ 默认绑定：全局对象会默认绑定，如果严格模式下，`this`会绑定到undefined。

```js
window.name = 'Jenny';
function person() {
    return this.name;
}
console.log(person());  //Jenny,调用函数的对象
```

+ 隐式绑定：函数作为对象的某个方法调用，`this`就指向这个对象

```js
var o = {
    a:10,
    b:{
        a:7,
        fn:function(){
            console.log(this.a); //undefined
        }
    }
}
o.b.fn();//7
var j = o.b.fn;
j();//this指向window
```

+ new绑定：如果用`new`构造函数生成一个实例对象，`this`指向此对象。

```js
function test() {
　this.x = 1;
}

var obj = new test();
obj.x // 1
//new过程遇到return一个对象，此时this指向为返回的对象
function fn()  
{  
    this.user = 'xxx';  
    return {};  
}
var a = new fn();  
console.log(a.user); //undefined
//如果返回一个简单类型的时候，则this指向实例对象
function fn()  
{  
    this.user = 'xxx';  
    return 1;
}
var a = new fn;  
console.log(a.user); //xxx
//注意的是null虽然也是对象，但是此时new仍然指向实例对象
function fn()  
{  
    this.user = 'xxx';  
    return null;
}
var a = new fn;  
console.log(a.user); //xxx
```

显示修改：`apply` `call` `bind`这些方法作用是改变函数的调用方法。

```js
var x = 0;
function test() {
　console.log(this.x);
}

var obj = {};
obj.x = 1;
obj.m = test;
obj.m.apply(obj) // 1
```

箭头函数的`this`在代码书写编译时就已经绑定，会捕获其定义时的词法作用域中的 `this`

### apply&call&bind

都是改变this的指向的方法，位于`Function`构造函数的`prototype`属性上，用法都是`Fn1.apply(Fn2,...args)`,其中Fn1&Fn2均为构造函数，但是也有些许不同：

```js
apply(thisArg, argsArray)
call(thisArg, arg1, arg2,/* …, */ argN)
bind(thisArg, arg1, arg2,/* …, */ argN)
```

apply作用于args接收数组同时给构造函数中传入数组，call的args接收的是值，这两个方法都返回Fn1执行后的返回值。
bind在函数接收方面和call一样，但是他会返回被绑定的函数Fn1，而且不执行Fn1

怎么记忆呢：apply的开头是a 记成array；call和bind都是四个字符 接受一样的；bind有绑定的有意思，就是先绑定不用。

### 事件与事件模型

JS中的事件，其实就是浏览器中发生的一种交互操作。

事件流经历三个阶段：事件捕获阶段(capture phase)、处于目标阶段(target phase)、事件冒泡阶段(bubbling phase)

事件冒泡是一种从下往上的传播方式，由处于目标阶段的触发节点逐渐向上传播到最上的节点也就是DOM中最高的父节点。

```js
var button = document.getElementById('clickMe');

button.onclick = function() {
  console.log('1.Button');
};
document.body.onclick = function() {
  console.log('2.body');
};
document.onclick = function() {
  console.log('3.document');
};
window.onclick = function() {
  console.log('4.window');
};

//1.button
//2.body
//3.document
//4.window
```

事件模型可以分为三种：原始事件模型（DOM 0级）、标准事件模型（DOM 2级）、IE事件模型。

一般使用原始事件模型和标准事件模型。

```html
//原始事件模型
<button onclick="handleClick()">Click me</button>
```

```js
//标准事件模型
element.addEventListener('click', handleClick, useCapture);
```

区别是原始事件模型简单，但有局限，不支持事件捕获和多个事件处理器；标准事件模型提供更多灵活性和控制。

### typeof与instanceof

`typeof`操作符返回一个字符串，用于表示未经计算的操作数的类型。

```js
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
typeof null // 'object'
typeof [] // 'object'
typeof {} // 'object'
typeof console // 'object'
typeof console.log // 'function'
```

`instanceof` 运算符用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上，返回布尔值。

```js
// 定义构建函数
let Car = function() {}
let benz = new Car()
benz instanceof Car // true
let car = new String('xxx')
car instanceof String // true
let str = 'xxx'
str instanceof String // false
```

> **手写instanceof：**
>
> ```js
> function myInstanceOf(left,right){
>     if(typeof left !== 'object'||typeof left === null)return false
>     let proto = Object.getPrototypeOf(left)
>     while(true){
>         if(proto === null) return false;//防止不是使用构造函数创建的实例
>         if(proto === right.prototype)return true
>         proto = Object.getPrototypeOf(proto)
> 	}
> }
> ```

### 事件代理

事件委托，会把一个或者一组元素的事件委托到它的父层或者更外层元素上，真正绑定事件的是外层元素，而不是目标元素。

如果我们有一个列表，列表之中有大量的列表项，我们需要在点击列表项的时候响应一个事件，如果给每个列表项一一都绑定一个函数，那对于内存消耗是非常大的，这时候就可以事件委托，把点击事件绑定在父级元素`ul`上面，然后执行事件的时候再去匹配目标元素。

### 事件循环

JS中所有任务都可以分为同步任务和异步任务。其中异步任务还可以分为微任务和宏任务。

> **微任务和宏任务：**
>
> + 微任务：一个需要异步执行的函数，执行时机是在当前主函数执行结束后，宏任务结束之前。例如：Promise.then、Process.nextTick
> + 宏任务：常见的宏任务有：setTimeout/setInterval、I/O

---

> **async和await：**
>
> async函数会返回一个promise对象，await会将其后的代码化为微任务。

### 防抖和节流

```js
var debounce = function(fn, t) {
    let timer = setTimeout(()=>{},t)
    return async function(...args) {
        clearTimeout(timer)
        timer = setTimeout(()=>{
            return fn(...args)
        },t)
    }
};
```

### 大文件上传

影响的原因就三点：**服务器本身处理数据的能力**，**程序自设的请求超时**，**网络波动**。解决方案是**分片上传**。

#### 分片上传

前端有个文件（zip或者视频）要传到后端，咋做呢？

首先我们进行思考，一整个传过去肯定不现实，中间断了就得重传，那么我们把他拆分成好几个块异步并发上传不就好了。但是拆成块就有个问题，多个上传任务（单用户多文件/多用户）那不是会乱掉，所以我们需要和服务端确认这个文件的唯一标识。

1. 第一步：初始化文件，使用`new FileReader()`创建一个对象，传文件名（大小等）给后端，后端返回唯一标识。

> 如果服务端已经有了完全上传好的文件（通过唯一标识判断），可以不用再上传，直接前端显示完成，这个过程称为秒传

2. 第二步：文件转化为Base64编码，按照数量或者大小进行分片

> 如果文件比较小或服务器需要控制并发量就按照数量切分；如果文件比较大或者网络带宽有限的时候就按照大小来切分（因为如果文件很大，切分之后还是很大，那就没啥用）；还有，不是分片分得越小越好，分片分得小说明需要高并发和多次网络请求。

3. 异步并发，带上唯一标识和此片的索引上传

> 如果某一片上传失败，后端可以返回错误信息，前端可以写一个重传机制，重新上传现在没有上传的分片 

4. 验证完整性：按照唯一标识和索引进行拼接

> 如果上传过程中关闭网页了，可以使用断点续传技术，前端在初始化的时候发现有这个任务的前半截，那就返回索引，继续上传。

---

> 怎么才能不影响主线程工作上传文件？
>
> 可以使用Web Worker，`new Worker('js程序')`然后再用`postMessage()`去给他发送消息。
>
> Web Worker可以允许网页在后台执行一些耗时的操作，而不会阻塞主线程，他允许开发者在JS主线程之外单开一个线程。

### SSG、SSR、CRG

首先我们来了解一下页面渲染的全流程：

首先浏览器会将用户输入的域名解析找到服务器的位置 > 然后浏览器和服务器建立TCP连接 > 浏览器向服务器发送HTTP请求，请求指定的资源 > 服务器收到请求之后对请求进行处理 > 返回资源 > **解析HTML文件 > 解析CSS文件 > 执行JS文件 > 构建渲染树（DOM和CSSOM结合） > 布局 > 绘制 > 事件循环处理交互和页面更新**

好了我们再来说上面三个是啥。

#### SSG

SSG是静态站点生成的意思，像我们一开始学习前端的时候直接写的三剑客（不加以其他东西）就属于静态站点，常见的还有博客之类的，这些都属于SSG，优点是服务器返回的资源不会再进行更改。

#### CRG

CRG是客户端渲染的意思，我们可以看到页面渲染中会解析HTML文件、JS文件，之后构建渲染树，使用CRG的时候会先返回一个基础的HTML，只包含结构和对JS的引用，等到JS下载解析好之后会更新DOM树。这种方法比较常见，一般用于交互性强的应用，比如单页应用等。

> 单页应用是一种现代的Web应用架构，会使用路由在单个HTML页面中动态的更新内容。我们常见的网站基本都是单页应用。

#### SSR

SSR是服务端渲染的意思，前面我们提到使用CRG的时候会先返回一个基础的HTML，只包含结构和JS的引用。而对于SSR来说，服务器会返回一个带有完整数据的HTML，后续就不会需要更新一轮DOM树了。因为他是完整的数据，且省了一轮DOM更新，所以首屏加载快，SEO友好（容易爬取内容），如下是一个SSR实现的简易代码：

```js
const express = require('express');
const app = express();

// 模拟数据获取函数
function fetchData() {
  return { title: 'SSR 页面', content: '这是服务器端渲染的内容' };
}

// 页面模板
function renderTemplate(data) {
  return `
    <html>
      <head>
        <title>${data.title}</title>
      </head>
      <body>
        <div id="root">${data.content}</div>
        <script>
          // 客户端代码（可选）
          console.log('页面已通过 SSR 渲染');
        </script>
      </body>
    </html>
  `;
}

// SSR 路由
app.get('/ssr', (req, res) => {
  // 获取数据
  const data = fetchData();
  // 渲染页面
  const html = renderTemplate(data);
  // 返回 HTML 给客户端
  res.send(html);
});

// 启动服务器
app.listen(3000, () => {
  console.log('服务器已启动：http://localhost:3000/ssr');
});
```

## JavaScript - Prototype

我特别将原型这个部分分了出来，因为我觉得有些概念理解需要渐进的，上面的比较分散，而这一章则是有顺序的，你可以从上往下读，我会带你逐渐了解这些复杂的概念。

### 构造函数

我们先从一切的源头开始看起，什么是构造函数？

首先构造函数是一个函数，那他肯定是形如`function fn (){}`这样的。

第二，它是用于构造东西的，构造函数通常返回一个对象。我们使用`new`关键字来让构造函数创建对象，至于`new`到底干了什么，我们稍晚些再说。

我们常见的数据类型比如`Array` `String` 他们本身就是一个构造函数。当然我们也可以自己制造一个构造函数。

> 字符串对象和普通字符串是不一样的，普通字符串的性能更优。

构造函数到底是拿来干什么的，一言蔽之就是用来创建包含相同属性、方法的对象实例的。

> 后面会用到`instanceof`，你如果没见过就理解为：如果是由这个构造函数构造出来的就为true 否则为false(当然这个是不准确的说法，只是为了理解)

```js
function Cup(name){
    this.name = name
    this.size = 10
    this.use = function(){
        console.log('use')
    }
}
const cup = new Cup('kitty')
const arr = new Array()
console.log(cup instanceof Cup,cup.size,arr instanceof Array)//true 10 true
cup.use()//use
```

关键的东西来了：

构造函数有一个`prototype`属性，指向一个对象，这个对象上的方法和属性会被所有用这个构造函数创建的实例共享。

```js
function Cup(){}
Cup.prototype.value = 1
Cup.prototype.fn = function(){
    console.log('fn')
}

const cup = new Cup()
const bottle = new Cup()
console.log(cup.value,bottle.value)//1 1
cup.fn()//fn
cup.value = 3
Cup.prototype.value = 2
console.log(cup.value,bottle.value)//3 2
```

### 静态方法与实例方法

> 我们总是能看见一些方法是形如`Array.isArray(obj)`，另一些方法是形如`obj.splice()`，有啥区别呢？

前者是静态方法，定义在`Array`**类**上，不依赖于实例的状态，不需要创建实例。

后者是实例方法，定义在类的原型链上，用来处理类的实例对象。

```js
Array.prototype.test = () => {//创建实例方法
    console.log('test1');
}

Object.defineProperty(Array, 'test', {//创建静态方法——可配置版
    value: function (e) {
        console.log(e);
    },
    writable: true, //可写
    configurable: true, //可配置
    enumerable: false //不可枚举
})
//或者
Array.value = function(e){//创建静态方法——快速不可配置版
    console.log(e)
}

const testArr = new Array()
testArr.test()//test1
Array.test('test2')//test2
```

###  New

好的，接下来我们来讲讲`new`到底干了啥玩意。

首先我们之前提到构造函数返回的一般是一个新创建的对象，但是也有特殊情况，若构造函数返回一个普通对象，那么new不再返回新构造的对象，而是返回这个普通对象。

有点绕对吧，来看例子：

```js
function Special(){
    return {
        a:0,
        f1:function(){
            console.log(1)
        }
    }
}

function Normal(){}

const special = new Special()
const normal = new Normal()
console.log(special,normal)//{a:0,f1:function(){console.log(1)}}  Normal
console.log(special instanceof Special,normal instanceof Normal)//false true
```

我们使用`new`将一个给定的构造函数创建一个实例对象。`new`做了如下事情：

- 创建一个新的对象

- 将对象指向构造函数

  > 所有对象都有一个`__proto__`专门用来指向构造函数，用于实现构造函数的属性和方法的继承

- 将构造函数的this指向对象

  > 使用`apply`函数实现换绑，同时调用Fun拿到一个返回值

可以写成下面这样：

```js
function mynew(Fun,...args){//args用于接收构造函数的参数
	const obj = {}
    obj._proto_ = Fun.prototype
    let result = Fun.apply(obj,args)
    return result instanceof Object?result:obj;//用来处理特殊情况,如果返回普通函数就返回
}
```

很好你已经学会什么是构造函数，构造函数的结构，如何用构造函数创建一个实例对象了，接下来学点难的。

### 继承

继承是面向对象中的一个概念，继承可以让子类具有父类的各种属性和方法，不需要再编写相同的代码，并且在子类别继承父类别的同时，可以重新定义某些属性、方法，获得不同的功能。

属性和方法有不同的继承方式（原因下面会解释）：

构造函数继承（继承属性）

```js
function Parent() {
    this.name = 'P'
}
function Children() {
    Parent.call(this)
    this.value = 'C'
}
const test = new Children()
const test2 = new Parent()
console.log(test,test2);//Children {name: 'P', value: 'C'} Parent {name: 'P'}
```

> 不知道你会不会好奇`call`改变了`this`的指向，为什么还能获取到`Parent`的`name`，因为`call`只是临时改变了`Parent`的上下文，不改变他的定义。

原型链继承（继承方法） 

```js
//写法一 每一个new Child，创建出来的每一个实例改变父类属性时都会影响到父类。
Child.prototype = new Parent();
//写法二 创建原型链继承的现代方法
Child.prototype = Object.create(Parent.prototype)
Child.prototype.constructor = Child
```

对于写法一：

如果 `Parent `的构造函数中有依赖于 `this`的逻辑，可能会导致意外行为。

当构造函数的 `prototype `和实例自身的属性有同名属性时，实例对象会优先访问自身的属性，而不是原型链上的属性。这是因为`JavaScript`的属性查找机制会先在实例对象上查找，如果找不到才会沿着原型链向上查找。（这也是为什么属性和方法要分开继承）

所以，当使用`Child.prototype = new Parent()`时，Parent的属性会被存入到Child的prototype中，但是如果Child构造函数自身拥有同名属性时，Child构造出来的实例会优先继承Child中的属性，但是Parent在构造原型链的时候已经被调用一次，这就有可能导致一些问题。

```js
function Parent() {
  console.log("Parent 构造函数被调用");
  this.count = 0;
}
function Child() {
  console.log("Child 构造函数被调用");
}
Child.prototype = new Parent();//Parent 构造函数被调用
const childInstance = new Child();
console.log(childInstance.count); // 输出 0
//这里只是调用了一个log如果里面写入一些抽象逻辑，就会出bug。
```

对于写法二：

首先构造函数的`prototype`中除了拥有继承的属性、方法之外还拥有一个特殊的属性`constructor`，这个函数用于指向其本身。这个属性的键为`constructor`，值为构造函数本身。

`Child.prototype = Object.create(Parent.prototype)`目的是创建一个和Parent一模一样的构造函数Child。

以上这一步做到了复制构造函数的原型对象，但是我们把constructor也给复制过来了，这时候就要改一下指向，将constructor指向构造函数本身，这么做的目的是为了防止后续的指向性问题。

### 深拷贝和浅拷贝的区别

浅拷贝指创建新的数据，如果属性是基本类型，则为其字面量；如果属性为引用类型，拷贝的就是内存地址。即浅拷贝出来的对象还是指向同一个内存地址。

> eg.`slice()`、`concat()`

深拷贝则是开一个新的栈，基本类型的值也是拷贝字面量；但是如果是引用类型，值相同但是会有不同的内存地址。即深拷贝出来的对象不指向同一个内存地址。

> eg.`JSON.stringify()`

简而言之：浅拷贝只复制其字面量不改变新值的内存地址（还是指向旧的值），深拷贝则会改变赋予一个新的内存地址。因为浅拷贝只会复制其字面量而不更改地址，当对新值进行修改时，旧的值也会被修改。但是由于基本数据类型是存在栈中的，而对象是存在堆中的。所以深拷贝是对于对象而言的。

> 堆和栈的区别：栈`Stack`是一种后进先出的数据结构，栈中的内存由编译器自动分配和释放，不需要程序员手动管理。堆`Heap`是一种动态内存分配的区域，堆中的内存需要程序员手动分配。

```js
//深拷贝
let obj1 = {name: 'A'}
const obj2 = JSON.parse(JSON.stringify(obj1));
obj1.name = 'B'
console.log(obj2); // {name: "A"}

//浅拷贝
var obj1 = {}
var obj2 = obj1;
obj2.name = 'B';
console.log(obj1.name); // "B"
```

**手写深拷贝：**

```js
function deepClone(obj,hash = new WeakMap()){//用weakmap是因为垃圾回收策略，避免内存泄漏
    if(typeof obj !== 'object'||obj === null)return obj//不是对象直接返回即可，深拷贝是对于对象而言的
    if(obj instanceof Date)return new Date(obj)
    if(obj instanceof RegExp)return new RegExp(obj)//日期、正则对象可以使用他们内置的拷贝构造函数
    if(hash.has(obj))return hash.get(obj)//有了就返回
    let cloneObj = new obj.constructor()//拿某个对象的原型对象构造出来的对象
    hash.set(obj, cloneObj);//加到hash中
    for (let key in obj) {//一层一层向下找
        if (obj.hasOwnProperty(key)) {//如果不是继承的就进if
            cloneObj[key] = deepClone(obj[key], hash);//递归拿到不是继承的属性的键
        }
    }
    return cloneObj;
}
```

### 原型及原型链

JS中 每一个对象都有一个原型对象，当访问一个对象的属性的时候，JS不仅会在对象上寻找，还会搜索该对象的原型，以及该对象原型的原型（这叫做原型链）直到匹配或者到达原型链的末尾。

> 什么是对象的属性：对象的属性是用来描述对象状态或者特征的，属性可以包含各种各样的数据，可以是基本数据也可以是函数、对象等，每个属性都有一个键值对。

也就是说，这些属性和方法是定义在object的构造函数的`prototype`而非实例本身。

实例通过`_proto_`属性上溯原型链，每个原型都有`prototype`，而`prototype`又有`constructor`属性来指向该原型（`constructor`主要就是用于指向确认该原型）

## JavaScript - Type

### 数据类型

#### 基本类型

基本类型有六种。

 ```js
//Number
 let intNum = 1,octNum = 001,hexNum = 0x1 //整数，常见十进制、八进制、十六进制
let floatNum = 0.1,eNum = 1.11e7//可以表示科学计数法e后面是幂
 log(0/0) //返回NaN 意思是本来返回数值的操作失败
 ```

---

```js
//Undefined
 let message,log(message)//返回undefined，变量声明过但未被初始化。
```

---

 ```js
//String
 let AStr = "1",aStr = '1',someStr = `1`//字符串一旦被创建，值就不可以再被改变，如果执行改变的操作，会先销毁再创建。
 ```

---

 ```js
//Null
 let nullOne = null,log(typeof nullOne)//null是一个空对象指针，输出为Object，如果变量要保存对象，但是当时又没有对象可以保存，就用null填充。
log(null==undefined)//undefined是由null派生来的，返回为真
 ```

---

 ```js
//Boolean
 //对于非空字符串、数值、对象、N/A 转为布尔值为true
//对于""、0、NaN、null、undefined 转为布尔值为false
 ```

---

```js
//Symbol
 let aSymbol = Symbol('1'),bSymbol = Symbol('1'),log(aSymbol==bSymbol)//返回false，symbol是原始值，symbol实例是唯一且不可变的，symbol的作用是确保对象属性使用唯一标识符。
```

---

#### 引用类型

引用类型统称为`object`，包括`object` `array` `function` `Date` `RegExp` `Map` `Set` 

 ```js
//Object对象
 let man = { // 属性名可以是字符串或者数值
	name:"zero",
 	"age":1,
 	1:true
 }
 ```

---

 ```js
//Array
 let colors = ["red", 2, {age: 20 }] //JS数组是动态大小的，每个槽位可以存储任意类型数据的。
 ```

---

 ```js
//Function
 let sum = (num1, num2) => {
 return num1 + num2;
 };
 ```

---

####  区别

 基本数据类型和引用数据类型存储在内存中的位置不同：

 - 基本数据类型存储在栈中
 - 引用类型的对象存储于堆中

 ```js
let a = 10;
let b = a; // 赋值操作
b = 20;
console.log(a); // 10值

var obj1 = {}
var obj2 = obj1;//这个操作让obj1和2的引用地址相同了。
obj2.name = "1";
console.log(obj1.name); // 1
 ```

### Iterator

#### 迭代器生成方式及使用方式

某些方法会返回一个迭代器，如`arr.entries()`返回一个带有全部键值对的迭代器，使用`next()`方法返回迭代器结果对象。

 ```js
 const array1 = ['a', 'b', 'c'];
 
 const iterator1 = array1.entries();
 
 console.log(iterator1.next().value);
 // Expected output: Array [0, "a"]
 
 console.log(iterator1.next().value);
 // Expected output: Array [1, "b"]
 ```

### Array

#### 数组长度与空槽

`arr.length`可以输出数组长度，甚至可以更改`arr.length`去改变数组长度，如果用此法扩展数组长度，没有被赋值的地方会产生`空槽`，`空槽`无法输出，对于不同数组方法，`空槽`也有不同的行为。

如`forEach`等迭代方法根本不会访问空槽。而其他的拼接复制方法如`concat`则会保留空槽。一些较新的方法会视其为undefined 如`splice()`拼接数组，`join()`等。

---

####  常用的数组方法

 + `every()/some()`-对数组内所有元素执行括号内函数，全部通过/有一个通过返回布尔值。
 + `fill(target,start,end)`-对数组内指定索引覆盖target值，超出范围不会扩展数组。
 + `find()/findLast()`-返回括号内函数符合条件的第一个/最后一个值，否则返回undefined。
 + `findIndex()/findLastIndex()`-返回括号内函数符合条件的第一个/最后一个索引，否则返回undefined。
 + `indexOf()/lastIndexOf()`-返回括号内值符合条件的第一个值/最后一个值的索引，否则返回-1。
 + `flat()`-扁平化数组，括号内为深度，ES10新语法
 + `includes()`-判断数组是否包含一个值，返回布尔值，ES7新语法
 + `join()`-将一个数组更改为其各元素以括号内字符串连接的字符串，默认使用逗号，如目标数组不是纯数组，报错。
 + `pop()/push()`-移除/添加数组末尾一个元素并返回该值，如果push的是一个数组则会在末尾添加数组，push自身会导致循环引用。
 + `shift()/unshift()`-移除/添加数组第一个元素并返回该值
 + `reverse()/toReversed()`-转置原数组改变原数组/转置原数组不改变原数组，`toReversed()`ES14新语法
 + `slice(start,end)`-浅拷贝一个由start开始end结束的数组，不改变原数组。
 + `sort()/toSorted()`-对数组按照元素第一个字符的ascii码排序改变原数组/不改变原数组
 + `splice(start,num,value...)/toSpliced()`-删除由start开始的num个数值，并在start索引下添加value值，改变原数组/不改变原数组。

---

> **forEach、filter、map、reduce的区别:**
>
> 三者都是ES5的新特性，均用于数组。
>
> `forEach`遍历数组全部元素并对数组进行操作，不返回新数组，return用于跳出循环，返回undefined。
>
> `filter`遍历数组全部元素并使用判断语句返回新数组，return值为假的时候过滤。
>
> `map`遍历数组全部元素并操作数组产生新数组，不改变原数组。
>
> `reduce((accumulator, currentValue)=>...,initialValue)`-遍历数组，若initialValue设置则为初始accumulator值，若没设置则currentValue为数组第一个值，不可处理数组对象。

 ```js
 //设分别执行三种函数
 let arr = [
 {name:'小明', age: 14},
 {name:'小华', age: 11},
 {name:'小红', age: 15},
 {name:'小黄', age: 17},
 ]
 
 let forEachBack = arr.forEach(item => {
 item.name = "学生"+item.name
 })
 console.log(forEachBack)//undefined
 console.log(arr)//name前都加上学生
 
 let filterBack = arr.filter(item => {
 return item.age>10
 })
 console.log(filterBack)//包含有name属性的，每一项age大于10的新数组
 console.log(arr)//arr不变
 
 let filterBack = arr.filter(item => {
 return item.age>10
 })
 console.log(filterBack)//包含有name属性的，每一项age大于10的新数组
 console.log(arr)//arr不变
 
 let mapBack = arr.map(item => {
 return item.age + 1
 })
 console.log(mapBack)//不包含有name属性的，每一项age加1的新一维数组：[15,12,16,18]
 console.log(arr)//arr不变
 
 let initialValue = -1;
 let reduceBack = mapBack.reduce(
 (accumulator, currentValue) => accumulator + currentValue,
 initialValue
 );
 console.log(reduceBack)//60 = -1 + 15 + 12 + 16 +18
 console.log(arr)//arr不变
 ```

### String

`String()`作为函数调用时，返回字面量原始值。`String()`作为构造函数（使用`new`）被调用时，会创建一个String对象，该对象不是原始类型。

```js
const a = new String("Hello world"); // a === "Hello world" 为 false
const b = String("Hello world"); // b === "Hello world" 为 true
a instanceof String; // 为 true
b instanceof String; // 为 false
typeof a; // "object"
typeof b; // "string"
```

---

####  常用的字符串方法

 + `concat(value,str)`-以value值拼接两个字符串。
 + `endsWith(value,index)/endsWith()`-查找字符串是否以value结尾/开头，index为查找的末尾索引+1，返回布尔值。
 + `includes(value)`-查找value值，返回布尔值。
 + `indexOf(searchString, position)/lastIndexOf()`-查找第一次/最后一次出现searchString的索引，position为查找开始的索引，默认为0。
 + `match()/search()`-匹配正则表达式，返回匹配的字符的数组/索引。
 + `replace(value,origin)/replaceAll()`-匹配字符串value替换origin，返回替换后的字符串。
 + `slice(start,end)`-提取字符串的一部分返回新字符串，不改变原字符串。
 + `split(rule)`-按照rule模式将字符串分割成一个数组，返回该数组。
 + `toLowerCase()/toUpperCase()`-全部换成小写/大写
 + `trim()`-从字符串两端移除空白字符，返回新字符，不修改原来的字符。

### Map

Map对象保存键值对，并且可以记住键的原始插入顺序，任何值都可以作为键或者值。比较适合多次查找的情况。

>  **Object和Map的区别：**
>
>  |   区别   |                     Map                      |                      Object                       |
>  | :------: | :------------------------------------------: | :-----------------------------------------------: |
>  | 键的类型 |             Map的键可以是任何值              |         Object的键必须为字符串或者Symbol          |
>  | 键的顺序 |         Map的对象按照插入的顺序迭代          | Object的排序就很混乱，ES6之后按照属性创建顺序迭代 |
>  |   迭代   |          可迭代对象，可以使用for of          |            不可迭代，默认只能用for in             |
>  |   性能   | 在涉及频繁添加和删除键值对的场景中表现更好。 |   在涉及频繁添加和删除键值对的场景中表现更好。    |

---

####  常用的map方法

 + `clear()`-清除所有元素
 + `delete()`-删除指定键的值
 + `forEach()`-对每一个键/值进行一次操作
 + `get()`-获取指定键的值，一般并对其进行后续处理。
 + `has()`-检查指定键是否存在，返回布尔值。
 + `keys()/values()`-返回一个迭代器对象，该对象包含了此map中每个元素的键/值
 + `set()`-向map中添加一个指定的键值对。

### Promise

表示对异步操作的完成或者失败及其结果。

#### 常用的Promise方法

+ `all()`-同时执行所有的异步任务，如果有一个执行失败，那么失败。（用于异步并发上传文件）
+ `allSettled()`-同时测试执行所有的异步任务，返回测试结果
+ `race()`-只要有一个promise完成，无论成功与否返回结果。
+ `any()`-只要有一个promise成功，返回成功结果，否则等待所有失败返回错误。
+ `resolve()`-将promise对象以成功标志返回。
+ `then()`-promise对象以成功标志返回时，执行then中的语句
+ `reject()`-将promise对象以失败标志返回。
+ `catch()`-promise对象以失败标志返回时，执行catch中的语句
+ `finally()`-promise对象最终一定执行此代码块中的语句

# 算法

## Hash算法

hash(哈希)算法是把任意长度的输入，通过算法变换成固定长度的输出。

>  eg.[两数之和](https://leetcode.cn/problems/two-sum/description/?envType=study-plan-v2&envId=top-100-liked)

# 实际面试环节

## 10.15海康威视

+ 你的上一段实习有什么亮点/难点？

  ```markdown
  原答：需要对给过来的一些数据进行处理。
  
  修正：当时作为初学者接到的任务都不是很难，主要遇到的困难有使用Element Plus样式穿刺、组件间传值这些问题。
  ```

+ JS中常用的数据结构类型有哪些？

  ```markdown
  原答：7种，number，undefined，string，null，boolean，symbol，其他的类型统称object，object可能包含对象、数组、函数之类的。
  
  修正：JS中有六种基本的数据类型，分别是number、string、boolean还有undefined、null和symbol。除此之外还有一个复杂数据类型object，它包含了对象、数组和函数等，这些对象可以用来构建更复杂的数据结构，例如链表、树等。
  ```

+ JS怎么处理大整形类型？

  ```markdown
  原答：一般是用bigint，对数据转化成大整形类型之后如果需要加加减减的话就要加n，比如加一就是加一n
  
  修正：在JS中处理大整数，可以使用BigInt类型，它允许你安全地表示和操作超出Number类型安全范围的大整数。使用BigInt时，只需要在数值后面加上n或者用BigInt()函数来创建。进行算数运算时，必须所有操作数都是BigInt类型，BigInt与Number不兼容。
  ```

+ JS的Map和对象有什么区别？

  ```markdown
  原答：Map和对象的一些方法属性可能不同，比如has、get之类的。
  
  修正：首先Map的键可以是任意类型的，对象的键在访问的时候总是被当作字符串处理。迭代顺序不同，对象是按照属性创建时间迭代，Map是按照添加到map的顺序迭代。对象没有内置方法取得键值，Map有keys，values之类的。数据规模小时使用对象，数据规模大时使用map，因为map是为了快速查找而优化的。对象有原型链，Map没有原型链。
  ```

+ 怎么获取对象的属性值？返回一个数组，数组是对象的所有值怎么写？

  ```
  原答：直接用键获取就可以了，用Object.values()即可返回数组。
  
  修正：可以使用Object的静态方法values，也可以使用forin循环中间包一个obj.hasOwnProperty(key)用于确保该键是此对象的，而不是继承下来的。
  ```

+ 对象可以直接用for of循环拿这些值吗？

  ```
  原答：可以，直接用for of应该就可以拿到。//你知道什么是可迭代对象吗？对象还可以用for of拿这些值吗？
  
  修正：不可以，for of是用于遍历可迭代对象的每个元素，例如数组 字符串 Map Set。for in用于遍历一个对象的所有可枚举的属性，包括其原型链上继承的。
  ```

+ 讲一下原型链吧

  ```markdown
  原答：意思是说每一个对象，每一个对象构建的时候需要用构造函数去构造原型。每一个对象都有一个prototype指向它的属性，里面还有一个constructor指向他自己，如果我需要用一个构造函数去构造一个新的对象的话，新的对象也会有一个_proto_指向原来的构造函数，如果想要获取一开始的构造函数的话，可以用原型链溯源往上找。
  
  修正：原型链是一个用于实现继承的机制，每个对象都有一个内部属性，叫做prototype，这个内部属性引用了另一个对象，称为该对象的原型，代码中一般用getPrototypeOf去获取。这个对象的原型又有一个原型，这样一直往上就是原型链。如果想要访问一个对象的属性时，该对象本身没有这个属性，JS会沿着原型链网上找直到找到或者达到末端。
  ```

+ 你有一个实例，怎么通过这个实例拿到他的构造函数？

  ```
  原答：可以通过循环访问_proto_去找他的原型，如果寻找到的原型的prototype和实例的相同，那就说明这是他的构造函数。//不对，八股文背得太浅了，没有理解本质
  
  修正：可以使用对象.constructor获取其构造函数，但是这个值其实可以被覆盖的。如果需要更稳健的方法，那可能得创建实例的时候就保存这个引用关系。
  ```

+ 什么是构造函数，什么是原型对象？

  ```
  原答：构造函数就是用于构造对象的函数，原型对象就是你要创建一个实例的一个对象，比如我new Person()，Person就是他的原型对象。
  
  修正：构造函数是用于创建函数的函数，当用new关键字调用了一个函数时，这个函数就成为了一个构造函数。构造函数会创建一个新的对象，这个对象会继承构造函数prototype的属性和方法。原型对象是指某个对象中prototype所指向的对象，每个对象都有一个对象原型，该对象从其对象原型中继承相关的属性和方法。
  ```

+ 在Vue场景下，让你封装一个Vue组件，组件实现一个登录表单界面，一个name一个password，要求创建一个子组件给别人用，别人通过v-model传进来，你的表单里也是有一个name和password，如果后续你的表单扩了，后续别人也是通过v-model传，你的这个自定义组件的v-model怎么实现？

  ```
  原答：不太理解 
  //那你v-model怎么用的？ 
  原答：绑定我所需要的一些input之类的 
  //那自己写的组件不可以用v-model吗？ 
  原答：直接赋值不就行了吗？
  //什么是v-model
  原答：是用vue的时候写在盒子里的用于双向绑定的。
  //那如果我绑定在你自定义的属性上面呢？v-model是为了解决什么问题？
  原答：是为了解决视图到模型的问题吧
  
  修正：可以使用一个对象来作为v-model的值，并且为每一个属性创建一个input事件，这样在调用这个组件的时候外面只管传一个对象即可。
  
  修正：v-model是用于表单输入和应用状态之间创建数据双向绑定，对于自定义组件，可以使用defineModel来简化v-model，接收传入的值和及时返回改变的值。
  ```
  

## 10.16云合智网

+ ES6有接触过吗，用过里面的哪些东西呢？

  ```
  原答：用过Map之类的，和箭头函数。
  
  修正：使用过箭头函数、模板字符串、解构赋值、Promise异步、let和const、Map等。
  ```

+ 能说一下箭头函数有哪些优势吗？

  ```
  原答：箭头函数和普通函数的区别是写法不同，箭头函数的this指向它本身，普通函数的this按照JS规定指向，普通函数可以用new去构造，箭头函数不可以。
  
  修正：箭头函数的出现让函数的书写变得很简洁，除此之外还解决了this执行环境所造成的一些问题，比如匿名函数和setTimeout的this指向问题。
  ```

+ Map的键可以有哪些类型？

  ```
  原答：Map的键可以是任何类型，如果是对象就不可以，对象的键只能被读为字符串。
  
  （无修正，答得挺好的，下次加油）
  ```

+ call、apply和bind的区别？

  ```
  原答：这三者都是用于改变this的指向，call传入两个值，第一个值是指向的对象，第二个值传入一个参数。apply第二个值是传入的数组，然后bind就是直接返回指向的对象。
  
  修正：这三个函数都用于改变this指向，他们三个都是函数对象的静态方法，当一个函数调用call的时候，会把函数中的this指向改为传入的第一个对象值，还能接受一系列参数，这些参数会传递给函数。apply的用法和call差不多，但是他不再接受一系列参数而是一个数组。bind和call用法一样，但是返回一个新函数可以稍后调用。
  ```

+ 有没有了解过let、const和var有什么区别？

  ```
  原答：let和const是ES6新增的特性，是块级元素；var一般作用域全局变量。let的值是可变的，const的值是不可变的，如果你想要试图改变它的话会报错。//那如果const定义一个对象，那么我们可以改变这个对象里属性的值吗？
  原答：可以的
  
  修正：var变量具有函数作用域，但是let和const是块级作用域；let和var可以被重新赋值，const不能被重新赋值，但这不代表它指向的引用类型比如对象或数组内容不能改变。当var在全局作用域下声明变量的时候，这个变量会变成全局对象的属性，let和const就不会。
  ```

+ 你了解过哪些进行深拷贝的方法？

  ```
  原答：getPrototypeOf，通过获取某个对象的原型的属性和方法来进行深拷贝。//还有别的吗
  
  修正：JSON.stringify+JSON.parse序列化加反序列化可以深拷贝，但是这种方法不可以复制函数、undefined和循环引用。有些对象比如日期对象 正则对象可以使用他们的拷贝构造函数来进行深拷贝。还有一种方法就是手写递归拷贝。（一定要会手写）
  ```

+ 有没有了解过闭包？

  ```
  原答：假如在函数a中定义了一个函数b，b中可以用到a定义的量。//什么时候使用闭包？
  原答：用于构建私有变量，用于...说不出，可以举个例子。...（但是举错了，把延长变量存在时间的例子举成了构建私有变量的了。）
  
  修正：（答得挺好的，把例子举完整即可）
  ```

+ 有没有用过splice这个函数？

  ```
  原答：用过，splice对数组进行操作，第一个值是指要操作的索引，第二个值是要删除元素的数量，splice会从该索引后删除指定数量的元素，第三个值是值删除后在这个位置添加的数组。
  
  （无修正，答得挺好的，下次加油）
  ```

+ 有没有了解过事件冒泡？

  ```
  原答：在DOM中有三个阶段，第一个是啥来着，会去找那个事件，从最高的window往下找，一直找到那个事件，然后进入处于目标状态，比如click获得这个事件的状态，然后再往上冒泡，再从最小的盒子再冒泡到全局变量。
  
  修正：当在DOM树中触发了一个事件，比如点击或键盘输入，这个事件会经历三个阶段：分别是事件捕获、目标阶段、事件冒泡。事件捕获会从文档的根节点开始一直传播到目标元素本身。然后就到了目标阶段，这里就是事件实际发生的地方。然后就从目标元素开始向上冒泡，一直冒泡到根元素，我们可以在目标元素以上的祖先元素设置事件监听器来响应事件。
  ```

+ 你用过HTML5吗，用过里面什么东西？

  ```
  原答：...(不确定是不是HTML5的)
  
  修正：用过header、footer等语义元素，有助于搜索引擎优化。用过H5的一些新表单类型，比如type=email、url、number。用过video元素嵌入视频。用过canvas绘制图形。用过localStorage和sessionStorage存储数据。
  ```

+ 有接触过HTML5的websocket吗？

  ```
  原答：我拿它和平时我们用的一些协议来对比吧，比如我们平时用的是Http、Https，然后用get、post传请求，这种只能是一次过一次回这样之类的，但是websocket是进行一个长线链接，比如说我要做一个聊天网站，我在这边发，另一台电脑也会马上同步信息过去，这就是平时websocket需要用到的一个场景。
  
  修正：websocket提供了一种在单个TCP连接上进行全双工通信的方法，这就意味着服务器和客户端可以同时发送和接收数据，这和传统的http响应模式不同，http通常只支持客户端到服务器的单向通信。
  ```

+ 你对Http协议了解得多吗？

  ```
  原答：只了解一点点//现在最新的版本是多少？
  原答：http2吧好像到3了。
  
  修正：http叫做超文本传输协议，是实现网络通信的一种规范，是万维网的数据通信的基础。最新的版本是2022年刚更新的http3，添加的一些特性包括改用基于UDP的QUIC协议作为传输层协议，取代了传统的TCP协议。quick UDP internet connections整合了TCP的可靠性和UDP的低延迟性，同时还提供TLS加密。QUIC还允许IP地址变化的情况下保持连接状态，提供了更高效的重传机制，能够更快地检测和回复丢包。
  ```

+ 有了解过https和http的区别吗？

  ```
  原答：https简单来说就是http+TLS/SSL 因为http本身是不安全的，https相当于在http上进行了一个加密，需要在网站上获取证书啊，去进行一个传来的密文的解密。
  
  修正：http的信息传输是明文进行的，没有进行加密处理。https在http的基础上加入了SSL/TLS协议，连接的时候需要进行额外的握手过程，保证一定安全但也会消耗一些性能。http的端口默认使用80，https的端口默认使用443。http不需要申请证书，https需要。搜索引擎策略会给https的网站更高的曝光度。
  ```

+ 有没有了解过https加密用的是什么算法呢？

  ```
  原答：没有
  
  修正：主要用非对称加密算法例如公钥私钥、对称加密算法例如三重数据加密算法、hash算法去加密。
  ```

+ 有了解过http请求方法有哪些吗？

  ```
  原答：常用的get post，不常用的push delete之类的
  
  修正：GET方法用于从服务器获取数据，POST方法用于向服务器发送数据，PUT用于向服务器发送数据用以替换内容，DELETE用于请求服务器删除资源，OPTIONS用于返回服务器支持的HTTP方法及查看服务器性能，TRACE方法用于回显服务器收到的请求，用于调试。
  ```

+ 有了解过get post有什么区别吗？

  ```
  原答：getpost平时我们用的时候都是要有请求头的，然后post是可以传一个请求内容的。
  
  修正：GET主要是向服务器获取数据，在url明文传递内容，不安全，且只能传输ASCII字符。POST主要是向服务器提交数据，在请求体中传递内容，可以传输多种数据类型，比如文本，二进制文件。
  ```

+ 有了解过常见的http响应码有哪些吗？

  ```
  原答：200开头的就是服务正常，300开头没怎么见过，400开头比如404 405Method Not Allow这种一般是前端路由这边的一些问题，500开头一般是服务器那边的问题。
  
  修正：100是服务器已经接收到请求的一部分；2xx是成功响应码，例如200是成功；3xx是重定向响应码，例如301表示请求的资源已经被移动到新的url，会返回新的url；4xx是客户端错误，例如400bad request错误的参数或地址，服务器理解不了，403forbidden服务器拒绝请求，404not found找不到资源，405method not allow请求方法服务器不允许；5xx是服务器错误，例如500是服务器错误，503是服务器超载。
  ```

+ 有没有了解Vue中computed和watch有什么区别？

  ```
  原答：计算属性不太了解，watch是用于监听ref属性的改变，如果改变的话就会执行后续的相应函数。
  
  修正：computed属性是基于其他其他的响应式数据动态计算并返回一个新的值，有缓存功能，只有当其依赖的数据发生变化时，才会重新计算，通常用于一个属性受到多个属性影响。watch属性是监听某个响应式属性，没有缓存功能，一旦监听的值改变就会发生回调，通常用于一个属性影响多个属性。
  ```

+ 写v-for的时候一般会加一个key，为什么？

  ```
  原答：key是用于和v-for一起去遍历盒子的
  
  修正：key作为唯一标识，可以帮助vue快速定位到需要更新的DOM元素，提高渲染效率。同时还需要选择稳定的key去保持每个列表值与其对应的组件实例的稳定关系。
  ```

+ 如果你的vue项目中遇到兄弟组件之间的通信，你会用什么方法呢？

  ```
  原答：用一些相关的插件比如pinia，可以让父传子props再用子传父emit
  
  修正：使用父传子props再用子传父$emit，如果是祖先组件传给后代组件可以用provide和inject，如果是那种没什么关系的组件传值的话，一般用全局总线库或者pinia。
  ```

+ 有部署过项目嘛，用什么Web容器呢？

  ```
  原答：直接把文件传到服务器中，然后用nginx去部署的
  
  修正：使用Nginx部署。（常见的还有tomcat，但是没用过就不强答了。）
  ```

+ 那你改过nginx的配置嘛？

  ```
  原答：改过端口号和index页面和location指向我的文件夹。
  
  修正：监听端口、location块、SSL/TLS证书和密钥。
  ```

+ 平常有接触linux？

  ```
  原答：接触得少
  
  （没什么好说的，不是一下子能提升的）
  ```

+ 听说过docker容器嘛？

  ```
  原答：听说过，相当于我这边写好了，然后用docker把我这边的环境什么的打包给别人。
  
  修正：Docker容器中包含应用程序所需要的一切运行条件，包括代码、系统工具和库等，它可以解决同一个代码放我这里能跑放别人电脑跑不了的情况。
  ```

+ 有没有用过集成持续部署的软件，比如说Jenkins

  ```
  原答：没有用过
  
  修正：用过Gitlab，知道jenkins，Gitlab可以将gitlab仓库的代码持续集成和部署。 
  ```

+ 平常CSS写得多嘛，相对定位和绝对定位解释一下

  ```
  原答：一般是给父盒子相对定位，然后想要使用绝对定位，需要给父元素设置相对定位才能使用绝对定位，绝对定位是相对于父元素的。
  
  修正：相对定位的通过position relative设置，设置之后改动偏移量盒子会偏移，但是它还是占据原来的位置。设置绝对定位是position absolute，需要给他父元素设置相对定位，绝对定位就会完全脱离文档流，不再占据原来的空间。根据偏移量移动。
  ```

+ 用过flex布局嘛，flex布局他的容器上有哪些属性呢？

  ```
  原答：比如说常用的justify-content、align-item。flex-wrap可以对子元素进行换行处理。
  
  修正：用过，比如flex-direction决定主轴方向，flex-wrap决定子元素是否换行，justify-content决定主轴的对齐方式，align-items决定和主轴交叉的那个轴的对齐方式。
  ```

+ 算法题：100~999的水仙花数

  ```js
  //原答：
  for (let i = 100; i < 999; i++){
      let sum = 0
      let temp = i
      while (temp > 0) {
          sum += (temp % 10) ** 3
          temp = parseInt(temp/10)
      }
      if(sum === i)console.log(i);
  }
  
  //（挺好的）
  ```
  
  

