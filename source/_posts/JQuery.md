---
title: JQuery
date: 2023-06-24 18:01:47
tags: [笔记,迁移,前端]
excerpt: 一个便于使用的JavaScript库
categories: 技术栈
---

# JQuery

但是他已经过时了，不建议去学，了解即可（2024）

<a href="https://jquery.cuishifeng.cn/">jQuery API 中文文档链接</a>

### JavaScript库

即library，是一个封装好的特定的集合（方法和函数）。从封装一大堆函数的角度理解库，就是在这个库中，封装了很多预先定义好的函数在里面，比如动画animate、hide、show。

简单理解：就是一个JS文件，里面对我们原生的JS代码进行了封装，存放到里面。这样我们可以快速高效的使用封装好的功能。

### jQuery的优点

+ 轻量级。
+ 跨浏览器兼容
+ 链式编程、隐式迭代
+ 对事件、样式、动画支持，大大简化了DOM操作。
+ 支持插件扩展开发。有着丰富的第三方插件，例如：树形菜单、日期控件、轮播图等。
+ 免费开源。

### jQuery的顶级对象$

1.$是jQuery的别称，在代码中可以使用jQuery代替它，但一般为了方便都是直接使用。

2.$是jQuery的顶级对象，相当于原生JavaScript中的window。把元素利用它包装成jQuery对象，就可以调用jQuery的方法。

### jQuery对象和DOM对象

DOM对象与jQuery对象之间是可以相互转换的。

因为原生JS比jQuery更大，原生的一些属性和方法jQuery没有给我们封装，想要使用这些属性和方法需要把jQuery对象转换为DOM对象才能使用。

+ DOM对象转换为jQuery对象

  + $('div')
+ jQuery对象转化为DOM对象（两种方式）

  + $('div')[index]		index是索引号
  + $('div').get(index)      index是索引号


### jQuery选择器

##### jQuery基础选择器

原生JS获取元素的方式有很多、很杂，而且兼容情况不一样，因此jQuery给我们做了封装，使获取元素统一标准。

$("选择器")//里面选择器直接写CSS选择器即可，但要加引号

##### jQuery设置样式

$("div").css("属性","值")

##### 隐式迭代（重要）

遍历内部DOM元素（伪数组形式存储）的过程就叫做隐式迭代。

简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用。

##### jQuery筛选选择器

用法如$("li:first")

+ :first  	获取第一个元素
+ :last       获取最后一个元素
+ :eq(index)      获取到的元素中，选择索引号为2的元素，index从0开始。
+ :odd      获取到的元素中，索引号为奇数的元素
+ :even      获取到的元素中，索引号为偶数的元素

##### jQuery筛选方法

用法如$("li").parent()

+ parent()  查找父级
+ children(selector)  相当于$("ul>li"),最近一级（亲儿子）
+ find(selector)   相当于$("ul li"), 后代选择器
+ siblings(selector)      查找兄弟节点，不包括自己本身
+ nextAll([expr])      查找当前元素之后所有的同辈元素
+ prevAll([expr])       查找当前元素之前所有的同辈元素
+ hasClass(class)       检查当前的元素是否含有某个特定的类，如果有，返回true
+ eq(index)       相当于$("li:eq(2)"),index从0开始.

##### 链式编程

链式编程是为了节省代码量，看起来更优雅。

### jQuery样式操作

##### 操作CSS方法

jQuery可以使用css方法来修改简单元素样式；也可以操作类，修改多个样式。

+ 参数只写属性名，则是返回属性值。
+ 参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号。
+ 参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开，属性可以不用加引号。如$("div").css({width:400,height:400})

##### 设置类样式方法

+ 添加类：$("div").addClass("current");
+ 移除类：$("div").removeClass("current");
+ 切换类：$("div").toggleClass("current");

##### 类操作与className区别

原生JS中className会覆盖元素原先里面的类名

jQuery里面类操作只是对指定类进行操作，不影响原先的类名。

### jQuery效果

##### 显示隐藏

+ 显示语法规范：show([speed],[easing],[fn])
+ 显示参数：
  + 参数都可以省略，无动画直接显示
  + speed：三种预定速度之一的字符串("slow","normal","fast")或是表示动画时长的毫秒数值
  + easing：用于指定切换效果，默认是"swing"
  + fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

+ show()
+ hide()
+ toggle()

##### 滑动

+ 滑动语法规范：slideDown([speed],[easing],[fn])
+ 滑动参数：
  + 参数都可以省略，无动画直接显示
  + speed：三种预定速度之一的字符串("slow","normal","fast")或是表示动画时长的毫秒数值
  + easing：用于指定切换效果，默认是"swing"
  + fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

+ slideDown()
+ slideUp()
+ slideToggle()

##### 淡入淡出

+ 淡入淡出语法规范：fadeIn([speed],[easing],[fn])
+ 淡入淡出参数：
  + 参数都可以省略，无动画直接显示
  + speed：三种预定速度之一的字符串("slow","normal","fast")或是表示动画时长的毫秒数值
  + easing：用于指定切换效果，默认是"swing"
  + fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

+ fadeIn()
+ fadeOut()
+ fadeToggle()
+ fadeTo()
  + 渐进方式调整到指定的不透明度：fadeTo([speed],opacity,[easing],[fn])
  + opacity透明度必须写，取值0~1之间。
  + speed：三种预定速度之一的字符串("slow","normal","fast")或是表示动画时长的毫秒数值
  + easing：用于指定切换效果，默认是"swing"
  + fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

##### 自定义动画

+ animate(params,[speed],[easing],[fn])
+ 参数
  + params:想要更改的样式属性，以对象形式传递，必须写。属性名可以不用带引号，如果是复合属性则需要采取驼峰命名法
  + speed：三种预定速度之一的字符串("slow","normal","fast")或是表示动画时长的毫秒数值
  + easing：用于指定切换效果，默认是"swing"
  + fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

##### 事件切换

+ hover([over],out);
  + over:鼠标移到元素上要触发的函数（相当于mouseenter）
  + out:鼠标移出元素要触发的函数（相当于mouseleave）

##### 动画队列以及停止排队的方法

+ 动画或效果队列：动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。
+ 停止排队
  + stop()
  + stop()方法用于停止动画或效果
  + 注意：stop()写到动画或者效果的前面，相当于停止结束上一次的动画。

### jQuery属性操作

##### 设置或获取元素固有属性值prop()

所谓元素固有属性就是元素本身自带的属性，比如<a>元素中的href

+ 获取属性语法：prop("属性")
+ 设置属性语法：prop("属性"，"属性值")

##### 设置或获取元素自定义属性值attr()

用户自己给元素添加的属性

+ 获取属性语法：attr("属性")  //类似原生getAttribute()
+ 设置属性语法：attr("属性"，"属性值")

### jQuery内容文本值

主要针对元素的内容还有表单的值操作

##### 普通元素内容html()（相当于inner HTML）

html()---->获取元素的内容

html("内容")---->设置元素的内容

##### 普通元素文本内容text()（相当于inner Text）

text()---->获取元素的文本内容

text("内容")---->设置元素的文本内容

##### 表单的值val()（相当于原生value）

val()---->获取表单的值

val("内容")---->设置表单的值

### jQuery元素操作

主要是遍历、创建、添加、删除元素操作。

##### 遍历元素

jQuery隐式迭代是对同一类元素做了同样的操作。如果想要给同一类元素做不同操作，就要用到遍历。

+ $("div").each(function(index,domEle){xxx;})
  + each()方法遍历匹配的每一个元素。主要用DOM处理。
  + 里面的回调函数有两个参数：index是每一个元素的索引号；domEle是每一个DOM元素对象，不是jQuery对象
  + 所以要想使用jQuery方法，需要给这个dom元素转换为jQuery对象$(domEle)

##### 创建元素

+ $("<li></li>")
+ 动态创建了一个<li>

##### 添加元素

+ 内部添加
  + element.appent("内容")  把内容放入匹配元素后面，类似原生appendChild
+ 外部添加
  + element.after("内容")
  + element.before("内容")

##### 删除元素

+ element.remove()   //删除匹配的元素
+ element.empty()    //删除匹配的元素集合中所有的子节点
+ element.html("")    //清空匹配的元素内容

### jQuery尺寸、位置操作

##### jQuery尺寸

+ width()/height()	取得匹配元素宽度和高度值 只算width/height

+ innerWidth()/innerHeight()	取得匹配元素宽度和高度值 包含padding

+ outerWidth()/outerHeight()	取得匹配元素宽度和高度值 包含padding、border

+ outerWidth(true)/outerHeight(true)	取得匹配元素宽度和高度值 包含padding、border、margin
+ 以上参数为空，则是获取相应值，返回的是数字型
+ 如果参数为数字，则是修改相应值
+ 参数可以不必写单位

##### jQuery位置

位置主要有三个：offset()、position()、scrollTop()/scrollLeft()

+ offset()设置或获取元素偏移
  + 此方法设置或返回被选元素相当于文档的偏移坐标，跟父级没有关系。
  + 该方法有两个属性left、top。
  + 可以设置元素的偏移：offset({top:10,left:10})
+ position()获取元素偏移
  + position()方法用于被选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为标准
+ scrollTop()/scrollLeft()设置或获取元素被卷去的头部和左侧
  + scrollTop()方法设置或返回被选元素被卷去的头部。

### jQuery事件

##### 单个事件注册

+ 语法：element.事件(function(){})

#####  单个事件处理

事件处理on()绑定事件---->on()方法在匹配元素上绑定一个或多个事件的事件处理函数。

element.on(events,[selector],fn)

+ events:一个或多个用空格分隔的事件类型，如"click"或"keydown"

+ selector:元素的子元素选择器。
+ fn:回调函数，即绑定在元素上的侦听函数
+ 优势
  + 一：可以绑定多个事件，多个处理事件处理程序。$("div").on({mouseover:function(){},mouseout:function(){}})
  + 二：可以事件委派操作。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。
  + 三：动态创建的元素，click()没有办法绑定事件，on()可以给动态生成的元素绑定事件

off()方法可以移出通过on()方法添加的事件处理程序。

如果有的事件只想触发一次，可以使用one()来绑定事件

##### 自动触发事件trigger()

有些事件希望自动触发，比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发

element.trigger("type")

### jQuery事件对象

事件被触发，就会有事件对象的产生。

阻止默认行为：event.preventDefault() 或者 return false

阻止冒泡：event.stopPropagation()

### jQuery其他方法

##### jQuery对象拷贝

如果想要把某个对象拷贝给另一个对象使用，此时可以使用$.extend()方法

$extend([deep],target,object1,[objectn])

+ deep:如果设为true为深拷贝，默认为false浅拷贝
+ target:要拷贝的目标对象
+ object1:待拷贝到的第一个对象
+ objectn:待拷贝到的第N个对象
+ 浅拷贝是把拷贝的对象复杂数据类型中的地址拷贝给目标对象，修改目标对象会影响被拷贝对象。

##### jQuery多库共存

+ 问题概述：jQuery使用$作为标识符，随着jQuery的流行，其他js库也会用其作为标识符，这样一起使用会起冲突。

+ 客观需求：需要一个解决方案，让jQuery和其他的js库不存在冲突，可以同时存在，这就叫做多库共存。

+ jQuery解决方案：
  + 把里面的$符号统一改为jQuery，例如jQuery("div")
  + jQuery变量规定新的名称：$.noConflict()

##### jQuery插件

jQuery功能比较有限，想要更复杂的特技效果，可以借助jQuery插件完成。

注意这些插件也是依赖jQuery来完成的，所以必须要先引入jQuery文件，因此页被称为jQuery插件。

+ 常用网站：
  + <a href="https://www.jq22.com/">jQuery插件库</a>
  + <a href="https://www.htmleaf.com/">jQuery之家</a>
+ jQuery插件使用步骤
  + 引入相关文件。(jQuery文件和插件文件)
  + 复制相关html、css、js（调用插件）
+ 插件演示
  + 瀑布流
  + 懒加载：页面滑动到可视区域，再加载图片。我们使用jQuery插件库EazyLazyLoad。注意，此时的js引入文件和js调用必须写到DOM元素（图片）后面 
  + 全屏滚动（明日方舟）（fullpage.js）：github:https://github.com/alvarotrigo/fullPage.js

+ bootstrap JS插件：bootstrap插件也是依赖于jQuery开发的，因此里面的js插件使用，也必须引入jQuery文件。<a href="https://v3.bootcss.com">Bootstrap中文文档</a>

