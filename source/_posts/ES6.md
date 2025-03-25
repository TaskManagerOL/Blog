---
title: ES6
date: 2023-06-24 18:01:27
tags: [笔记,迁移,前端]
excerpt: Javascript自我进阶
categories: 技术栈
---

ES 是脚本语言的规范，而平时经常编写的 JS 是 ES 的一种体现，所以 ES 的新特性其实指的就是 JS 的新特性

### let

相当于局部变量

### const

常量，不可修改

### 解构赋值

可以用 let [ ...... ] = 数组名、let { ....... } = 对象名 ，这样的方式来快速取值

### 模板字符串

通常情况下你str是没办法换行的，想要换行的话就要用"" + 这样 但是 ES6 中给到了``反引号 在反引号中可以随便换行 :laughing:

### 对象的简便写法

如果对象的名字和值一样 就可以直接写一个

还有就是对象函数 可以省略function 直接写 名字(){} 这样

### 箭头函数

函数声明 变成了

> let fn = (a,b) => {
> 	return a+b;
> } 

这样 省略了function

+ this 是静态的 this 始终指向函数声明时所在作用域下的 this 的值
+ 不能作为构造函数实名化对象
+ 不能使用 arguments 变量

+ 当形参只有一个的时候可以省略小括号，当代码体只有一个的时候可以省略花括号

### 函数参数的默认值设置

在小括号里可以直接等于

> add = (c=1) => 
> 	return c;
>
> 结果是1 

与结构赋值结合

> connect = (username,password)  => {
> 	console.log(username)
> }
> connect({
> 	username:"111"
> 	password:"222"
> })

可以这样使用

### rest参数

ES6引用 rest 参数，用于获取函数的实参，用来代替 arguments 

用法如下

> fn = (a,b,...args){
> 	输出...
> }
> fn(传值)

值得一提的是 rest 函数必须要放到参数最后

### 扩展运算符

... 运算符可以把数组转化为逗号分割的参数序列

### symbol

symbol是一种类似于字符串的数据类型

### 迭代器 interator

一个用于快速遍历数组的 新属性 
next()会迭代调用数组元素，每次迭代一个，直到用完

> const num = [1,2,3,4];
> let it = num[Symbol.interator] ();//调用必须
> console.log(it.next());
> console.log(it.next());
> console.log(it.next());
> console.log(it.next());// 这样就会快速生成四个对象 value 会遍历 对象中还有一个 done 值 如果被遍历完了 done 就会变成true

### 生成器

其实就是一个特殊的函数，异步编程 纯回调函数

> function * gen(){
> 	part1;
> 	yield 'sign1';
> 	part2;
> 	yield 'sign2';
> 	part3;
> }
>
> let it = gen();
> it.next();
> it.next();
> it.next();

这样的话会逐渐执行part1，然后part2，然后part3

甚至可以用 yield 来传参，这里截取片段来展示

>let one = yield 111;
>console.log(one);
>
>...
>
>it.next('AAA') //这样就会输出AAA

### Promise (比较重要 面试常问)

Promise 是 ES6 引入的异步编程的新解决方案。语法上 Promise 是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果

使用Promise方案主要有以下好处

+ 可以很好的解决回调地狱的问题（避免了层层嵌套的回调函数
+ 语法非常简洁。promise对象提供了简洁的API 使得控制异步操作更加容易

==简单学学 如果想要了解还可以再看==

### Set

ES6提供了新的数据结构 Set (集合)。类似于数组，但是成员的值都是唯一的，集合实现了 iterator 接口 所以可以使用扩展运算符和for of进行遍历

会自动去重 类似数学中的集合 

.size是个数 .add增加 .delete删除 .has检测 .clear清空

### Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map也实现了 iterator 接口，所以可以使用 扩展运算符 和 for  of 进行遍历

### class

ES6 提供了更接近传统语言的写法，引入了 Class 这个概念，作为对象的模板。通过 class 关键字，可以定义类。基本上 ES6 的 class 可以看作 只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象原型的写法更加清晰、更面向对象编程的语法而已。

### 对象方法扩展

+ Object.assign(a,b) 对象的合并 
  该方法可以使两个对象合并 由后面的覆盖前面的 

+ Object.setPrototypeOf 设置原型对象 可以放到_proto_中去

### 模块化

模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小的文件组合起来

模块化的优势有以下几点：

+ 防止命名冲突
+ 代码复用
+ 高维护性

##### ES6模块化语法

模块化语法主要由两个命令构成：export 和 import

+ export 命令用于规范模块的对外接口

```javascript
let name = "name";
let teach = () => {
	console.log(name);
}
export {name,teach};
```

```JS
export default {
	name:"name";
    teach:function(){
	console.log(name);
	}
}
```



+ import 命令用于输入其他模块提供的功能

```JS
import {name,teach} from "url"
```

==ES7~ES11没学==

