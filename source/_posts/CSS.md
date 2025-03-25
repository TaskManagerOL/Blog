---
title: CSS
date: 2023-06-24 18:01:20
tags: [笔记,迁移,前端]
excerpt: 前端三剑客之一
categories: 技术栈
---





CSS参考手册：<a href="https://www.w3school.com.cn/cssref/index.asp">Ctrl+单击</a>

# 特殊样式制作方案

这里是一些CSS特殊样式设计的方案。

## CSS三角形绘制

+ 方案一🎯：**使用边框实现三角形**：

  原理：设置一个高宽为0的div，然后设置border-方向即可。

  ```css
  div {
    border-top: 50px solid yellowgreen;
    border-bottom: 50px solid deeppink;
    border-left: 50px solid bisque;
    border-right: 50px solid chocolate;
  }
  ```

  优点：快捷简单。

  缺点：只能实现45deg的三角形。

+ 方案二🎯：**使用背景渐变颜色实现三角形**

  原理：使用渐变色让其颜色变成固定的两种颜色，也可以是透明。

  ```css
  /* 线性渐变 */
  div {
    width: 100px;
    height: 100px;
    background: linear-gradient(45deg, deeppink, deeppink 50%, yellowgreen 50%, yellowgreen 100%);
  }
  
  /* 角向渐变 */
  div {
     width: 100px;
     height: 100px;
     background: conic-gradient(from 90deg at 50% 0, deeppink 0, deeppink 45deg, transparent 45.1deg);
  }
  ```

  优点：可以多角度自由斜角。

  缺点：三角形形态比较难以调试。

+ 方案三🎯：**使用盒子旋转实现三角形**

  原理：通过伪元素或内置盒子旋转和隐藏子元素溢出来实现三角形。

  ```css
  .triangle {
      width: 100px;
      height: 100px;
      position: relative;
      overflow: hidden;
      
      &::before {
          content: "";
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          background: deeppink;
          transform-origin: left bottom;
          transform: rotate(45deg);
      }
  }
  ```

  优点：直观、可塑性高。

  缺点：盒子容易偏移。

+ 方案四🎯：**使用容器剪裁实现三角形**

  原理：有一个css属性叫做clip-path，适用于创建一个只有元素部分区域可以显示的剪切区域。

  ```css
  div {
      background: deeppink;
      clip-path: polygon(0 0, 100% 0, 0 100%, 0 0);
  }
  ```

  优点：不只是三角形，能剪裁出任何想要的图形。

  缺点：操作量大。

+ 方案五🎯：**使用icon实现三角形**

  原理：直接使用字体中的icon。

  优点：太快了，什么都不用想直接输入一个字符即可。

  缺点：三角形不可调整，三角形可能随着不同字体变形。

## 缺角盒子实现

+ 方案一：**盒子遮挡实现**

  原理：做两个同背景颜色的三角形进行遮挡。

  优点：快速。

  缺点：颜色死板，背景是图片则没办法。

+ 方案二：**使用背景渐变颜色实现三角形**

  原理：同三角形绘制。

  优点：不用定位。

  缺点：同上方案。

+ 方案三：**使用盒子旋转实现缺角盒子**

  原理：使用一个较长的div和元素溢出隐藏样式。

  优点：可以设置缺角的边框。

  缺点：调试麻烦。

## 计算器类型数码字体实现

+ 方案：**直接去寻找对应字体**

  原理：使用字体更改数字字体比自己手写js+css容易太多了。

  ```markdown
  1.可以在https://www.dafont.com/上找到喜欢的字体。
  2.字体的文件一般都是以.tff为后缀，可以改成.eot或者.woff格式，兼容浏览器。
  3.在style.css中使用@font-face配置，如
  @font-face{font-family: 'digital';src:url('/public/DS-DIGIT.woff') format('woff')}
  4.在需要使用的地方使用font-family属性。
  ```

  优点：快速有效。
  
  缺点：字体寻找花费时间。

## 毛玻璃

+ 方案：

  ```css
  width: 400px;
  height: auto;
  background: rgba(255, 255, 255, .7);
  webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  ```

## 文字颜色渐变

+ 方案一：静态渐变。

  ```css
  background: linear-gradient(to right, #颜色, #颜色); 
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  ```

+ 方案二：动态渐变。

  ```css
  background: -webkit-linear-gradient(
    0deg,
    #颜色1,
    #颜色2 25%,
    #颜色3 50%,
    #颜色4 75%,
    #颜色1
  );
  -webkit-background-clip: text;
  color: transparent;
  ```

  

## 自由图形制作

+ 方案：使用`clip-path`属性，搭配figma或者其他工具效果更佳。

# CSS规范

[组织CSS](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Organizing)

## 基本样式

CSS规则由两个主要的部分构成：选择器及一条或多条声明，属性和属性值以”键值对“的形式出现，属性和属性值之间用英文冒号来分割，多个”键值对“之间用英文分号进行区分。

## 书写顺序

无论是原子类还是原始CSS写法，为了方便后期维护，也是为了让代码更加优雅。我们遵循下面书写顺序：

+ 位置属性(position, top, right, z-index, display, float等)
+ 大小(width, height, padding, margin)
+ 文字系列(font, line-height, letter-spacing, color- text-align等)
+ 背景(background, border等)
+ 其他(animation, transition等)

> 尽量缩写，例如margin-left、margin-right可以合并成一句margin-inline。

CSS规范不是必须的，而是为了让你代码更具有条理性。如果按照一个已经由很多人使用过，诸多项目检测过的代码编写习惯去编写代码，那么团队中的其他成员有可能会更容易理解你的代码。

## 注释跳转

写CSS的时候（特别是大项目）会发现CSS越堆越多。可以考虑使用以下方法划区：

```css
/* ☁️:part1 */
...
/* ☁️:part2 */
...
```

好处是可以用`ctrl+F`搜索`☁️:`在多个块中快速跳转。

## OOCSS

OOCSS（面向对象的CSS）基本理念是将CSS分解成可复用的对象，然后在一个div中使用多个类。

# CSS选择器

```css
/* 群组选择器：同时编写多个选择器 */
p,.nav {z-index:1}

/* 后代选择器：用于命中某一块选择器,注意后代选择器是可以跨盒子的，如
<h1>
	<p>样式生效</p>
	<div>
		<p>样式生效</p>
	</div>
</h1>
*/
h1 p {font-size:1.5rem}

/* 子代选择器：用于精确命中某一块选择器,后代选择器不可跨盒子，如
<h1>
	<p>样式生效</p>
	<div>
		<p>样式不生效</p>
	</div>
</h1>
*/
h1>p {font-size:1.5rem}

/* 兄弟选择器：同时选中所有兄弟盒子 */
h1~p {font-size:1.5rem}

/* 相邻兄弟选择器：同时选中两个兄弟盒子,只选择h1后紧挨着的p标签 */
h1+p {font-size:1.5rem}
```

## 选择器权重

|        选择器        |   优先级   |
| :------------------: | :--------: |
|      !important      | 最高优先级 |
|       内联样式       | 1，0，0，0 |
|       id选择器       | 0，1，0，0 |
| 类、属性、伪类选择器 | 0，0，1，0 |
|      元素选择器      | 0，0，0，1 |
|      通配选择器      | 0，0，0，0 |
|      继承的样式      | 最低优先级 |

## 标签选择器

```css
p {z-index:1;}
```

用HTML标签名称作为选择器，按标签名称分类，为页面中某一类标签指定。

## 类选择器

```css
.nav {z-index:1;}
```

如果想要差异化选择不同的标签，单独选择一个或者某几个标签，可以使用类选择器。

> 不能使用标签名作为类选择器的类名，可以使用中横线命名，不使用纯数字、中文、包括下划线（部分浏览器不兼容情况）进行命名。

## ID选择器

```css
#user {z-index:1;}
```

在HTML中只能调用一次，如果有调用一次后，别的标签不允许再次使用。（可以考虑与JS结合使用）

## 通配选择器

```css
* {z-index:1;}
```

对所有的标签进行修改（可结合后代选择器使用）

## 属性选择器

```css
/* 有该属性改变样式 */
a[title][lang]{color:black}

/* 属性值匹配zh改变样式 */
a[lang="zh"]{color:black}

/* 属性值以en开头改变样式 */
a[lang^="en"]{color:black}

/* 属性值以en开头改变样式 */
a[lang^="en"]{color:black}

/* 属性值以en结尾改变样式 */
a[class$="en"]{color:black}

/* 属性值有en改变样式 */
a[class*="en"]{color:black}

/* 属性值存在完整en改变样式 */
a[class~="en"]{color:black}

/* 属性值只有en或者以en-开头改变样式 */
a[class|="en"]{color:black}
```

## 伪类选择器

```css
/* 第一个子元素 */
li:first-child{color:black}

/* 最后一个子元素 */
li:last-child{color:black}

/* 第n个子元素，括号可以填n、2n、2n+1 */
li:nth-child(){color:black}

/* 第一类子元素 */
li:first-of-type{color:black}

/*最后一类子元素 */
li:last-of-type{color:black}

/* 第n类子元素 */
li:nth-of-type(){color:black}

/* 未访问过的a标签 */
a:link{color:black}

/* 访问过的a标签，只能改变链接颜色 */
a:visited{color:black}

/* 鼠标移入 */
div:hover{color:black}

/* 鼠标点击 */
div:active{color:black}

/* 鼠标选定 */
div:focus{color:black}
```

## 伪元素选择器

```css
/* 第一个字母 */
div::first-letter{font-size:32px}

/* 第一行 */
div::first-line{font-size:32px}

/* 选中的元素 */
div::selection{font-size:32px}

/* 元素开始的位置前 */
div::before{font-size:32px}

/* 元素开始的位置后 */
div::after{font-size:32px}
```

伪元素一般用于做盒子的遮罩。

# CSS引入方式

## 行内样式表

在某个标签内写入style，优先级非常高。原子类同理。

## 内部样式表

放在head的style 新手练习时使用的方式

## 外部样式表

单独写一个CSS文件，再将此文件引入到HTML中。（使用方法为建一个CSS的文件，直接在里面写样式，但要在引用的HTML文件中加入link标签） 

# CSS背景相关处理

```css
/* 复合写法 */
background:：<background-clip> <background-color> <background-image> <background-origin> <background-position> <background-repeat> <background-size> <background-attachment>

/* 设置背景延伸情况 */
background-clip: border-box(延伸到边框外沿，在边框下方)/padding-box(到内边距外沿)/content-box(到内容外沿)/text(剪影成文字);

/* 设置背景颜色 */
background-color: value(对应颜色的英文)/#xxxxxx(对应颜色的十六进制码)/rgba(x,x,x,x)(对应颜色的RGBA值)/hsla(x,x,x,x)(对应颜色的HSLA值);

/* 设置背景图像 */
background-image: url()(图片url，可以使用多个，靠前的z-index值大)/linear-gradient()(特殊的image格式，颜色渐变)

/* 设置背景起始点 */
background-origin: border-box(延伸到边框外沿，在边框下方)/padding-box(到内边距外沿)/content-box(到内容外沿)

/* 设置背景位置 */
background-position: X/Y X/Y.Client Y/X Y/X.Client (X/Y指关键字top/left/bottom/right/center X/Y.Client指对应偏移量)

/* 设置背景重复设置 */
background-repeat: repeat-x(X轴平铺)/repeat-y(Y轴平铺)/repeat(重复平铺)/space(尽可能重复，不会被剪裁)/round(尽可能重复，允许图像改变尺寸)/no-repeat(不重复)

/* 设置背景大小 */
background-size: value(实际取值)/auto/cover(缩放，尽可能覆盖)/contain(缩放，尽可能完全装入)

/* 设置背景固定 */
background-attachment: fixed(表示背景相对于视口固定)/local(表示背景相对于元素的内容固定)/scroll(表示背景相对于元素本身固定)
```

> `background-attachment` `scroll-padding` 这些属性一般用于视差滚动。

对于背景图片我们一般使用background-size的cover和contain有时候都不是很符合我们的要求，现代化的CSS新属性`object-fit`和`aspect-ratio`解决这个问题。

这两个属性是对于img标签来说的：

```css
object-fit:cover(覆盖整个元素)/scale-down(保持原来的大小)
aspect-ratio: value(屏幕的长宽比)
```

# CSS的三大特性

## 层叠性

+ 相同选择器给设置相同的样式，此时一个样式就会覆盖另一个冲突的样式。

+ 样式冲突，遵循的是就近原则，哪个样式离结构近，就执行哪个样式。
+ 样式不冲突，不层叠。

## 继承性

+ 子标签会继承父标签中的某些样式。（恰当使用可以降低CSS的复杂性）

+ 通常继承：text font line color这些属性
+ 特殊继承：font: 12px/24px;表示行高为24px，但可以写成font:12px/1.5;表示行高为当前字体的1.5倍，子代继承同样适用1.5倍。

## 优先级

+ 当同一个元素指定多个选择器，就会有优先级的产生

+ 选择器相同，则执行层叠性
+ 优先级为：！important>行内样式（直接在标签里面写style）>id>类>伪类=标签=属性选择>继承>通配符；

+ 复合选择器有权重叠加的问题，如子元素选择器就会相当于两个标签选择器的叠加。

# 网页布局

[CSS 布局手册](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Layout_cookbook)

## 常见网页布局

常见布局有 流式布局/网格布局/弹性布局.

> 流式布局中 行/块/行内块级元素的区别：
>
> 行级元素可以与其他元素保持在同一行，不可以自动换行，但是不能设置他的宽高(例如a\span\strong\u\em\i\sub\sup)；
>
> 块级元素不可以和其他元素保持在同一行（独占一行），可以自动换行，可以设置宽高(例如div\p\h1~6\ui\li)；
>
> 行内块元素可以与其他元素保持在一行，还能设置宽高(例如textarea\input\img\button)

```css
/* 关键值可以被分为六个种类 */
/* 外部表现，指这个盒子和这个盒子之外的元素的布局情况 */
display: block(该元素之前和之后产生换行)/inline(该元素之前和之后不产生换行)

/* 内部表现，指这个盒子内的元素布局情况 */
display: flow(使用流式布局)/flow-root(生成一个块级元素盒，会建立一个新的区块格式化上下文[1])/table(类似于table标签)/flex(使用弹性布局)/grid(使用网格布局)/ruby(同ruby标签，用于注音)

```

> [1]:**区块格式化上下文**（Block Formatting Context，BFC），是为了解决外边距折叠(区块上下外边距折叠为单个边距，取上下两个的最大值)、浮动元素覆盖、高度塌陷(子元素为浮动且高于父元素就会撑出去)而出现的，触发BFC的方式有浮动元素、绝对定位、overflow不为visible、display为flow-root等。
>
> 

### 盒子模型

+ 所谓盒子模型：就是将HTML页面中的布局元素看作是一个矩形的盒子，也就是一个盛装内容的容器

+ CSS盒子模型本质上是一个盒子，封装周围的HTML元素，它包括：边框、外边距、内边距和实际内容

+ 盒子模型的组成 每个元素都可以只设置上下左右 在元素后加-top/bottom/left/right即可
  + border边框 可以使用复合写法 边框会影响盒子实际大小 测量要减去边框宽度
    + border-width设置边框粗细
    + border-style设置边框样式 solid实线边框 dashed虚线边框 dotted点线边框  outset3D边框
    + border-color设置边框颜色
    + border-collapse用于合并相邻的边框  

  + content内容

  + padding内边距（内边距影响盒子的大小，当有宽度和高度属性时使用padding会撑大盒子，解决方法用宽度、高度减去padding*2 ）（当高、宽未指定时padding不再影响）  
    + 改变盒子边框和盒子内容距离
    + 可单写也可上下左右一起
    + 值个数为1一圈，值个数为2上下 左右，值个数为3上 左右 下，值个数为4顺时针

  + margin外边距
    + 改变盒子与盒子之间的距离

    + 输入方式和padding基本一样 

    + 常见应用：块级盒子居中对齐 条件：有宽度、左右外边距写为auto；行内、行内块元素水平居中给其父级元素添加text-align:center;即可。

    + <a href="https://blog.csdn.net/weixin_43334673/article/details/107177421">嵌套块元素塌陷</a>：父元素和子元素的外边距会合并 解决方案：为父元素添加overflow:hidden或定义上内边距或定义上边框

+ CSS第一行代码就是清除内外边距即*{padding:0;margin:0;}且行内元素尽量只设置左右边距（因为上下不起作用）。

##### 圆角边框

+ 样式：border-radius:...;

+ radius意为半径后面输入的值越大盒子越圆；

+ 可以输入4个值表示四个角

##### 盒子阴影

+ 样式为 box-shadow:...; 盒子的阴影不占空间。

+ h-shadow 表示水平位置的阴影
+ v-shadow 表示竖直方向的阴影
+ blur 表示阴影的模糊距离
+ spread 表示阴影的尺寸
+ color 表示阴影的颜色
+ inset 改为内部阴影

#####   文字阴影

+ 样式为 text-shadow:...;
+ 属性值为盒子阴影的前三个和color

### 浮动

+ 页面由标准流（普通流/文档流）、浮动、定位构成。
+ 为什么需要浮动？1.将多个块级盒子在一行显示且不留空隙。2.实现两个盒子的左右对其。
+ 网页布局第一准则：多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。
+ 样式为 float:属性值; 属性值可以为left和right和none float是用于创建浮动框的，将其移动到一边，直到左边缘或右边缘触及块或者另一个浮动框的边缘。
+ 浮动元素经常和标准流父级搭配使用 先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置

##### 浮动特性

+ 浮动的元素会脱离标准流
  + 脱离标准普通流的控制（浮）移动到指定位置（动）（俗称脱标）
  + 浮动的盒子不再保留原先的位置

+ 浮动的元素会一行内显示并且元素顶部对齐
  + 当父级元素装不下时，多出的盒子会另起一行。  

+ 浮动的元素会具有行内块元素的特性
  + 任何种类的元素都可以加浮动，但是加了浮动之后就会变成行内块元素。
  + 如果块级元素没有设置宽度，默认宽度是和父级一样宽，但是添加浮动后，它的大小根据内容决定。

##### 浮动布局的注意点

  + 通常是规定父级元素是标准流，然后子元素再规定为浮动。

  + ==理论上一个元素浮动了，其他兄弟元素也需要浮动。==

  + 浮动的盒子只会影响后面的标准流

##### 清除浮动

+ 由于父级盒子很多情况下不方便给高度，但是盒子浮动又不占有位置，最后父级盒子高度为0时，就会影响下面的标准流盒子
+ 由于浮动元素不再占有原文档流的位置，所以它会对后面的元素排版产生影响
+ 样式 选择器{clear:left/right/both;}
+ 清除浮动方法
  + 额外标签法（隔墙法 不常用）：在需要清除浮动的最后一个元素后写一个盒子（必须是块级元素  div最好），加上clear both。
  + 父级添加overflow：可以给父级元素添加overflow属性，将其属性值设置为hidden、auto、或scroll。hidden可以清除浮动。
  + after伪元素法：在父元素后面插入一个新盒子。
  + 双伪元素清除浮动：在新盒子的内部前面后面都插入一个盒子。

### 定位

##### 定位的应用

用于使盒子自由的在某个盒子内移动位置或者固定屏幕中的某个位置，并且可以压住盒子。

##### 定位的组成

+ 定位模式 属性为position
  + static为静态定位 相当于无定位 按照标准流摆放 通常不使用
  + ==relative为相对定位== 相对于自己原来的位置进行移动 只与自己原来的位置有关系 且原来在标准流的位置继续占有（人飞了，但是后面的人还给他留空）用于限制绝对定位（父相子绝）
  + ==absolute为绝对定位== 要看祖先元素 
    + 若无祖先 以浏览器界面对齐 
    + 若祖先元素有定位 以最近一级的有定位祖先元素对齐
    + 绝对定位的位置不再进行保留 
  + ==fixed为固定定位== 固定住盒子 即使滑动页面也不会改变盒子  以可视窗口的距离来移动位置
    + 让固定的盒子以版心对其：先让固定的盒子left50%，然后margin版心宽度的一半
  + sticky为粘性定位 刚开始相对定位 拉到盒子即将出可视空间时就变成固定定位
+ 边偏移 是定位的一个属性 有top/bottom/left/right 后面可以直接加距离

##### 定位的叠放次序

+ 使用z-index属性值可以控制盒子的叠放顺序 
+ 数值可以时正整数、负整数、或是0，默认是auto，数值越大，盒子越靠上
+ 如果属性值相同，则按照书写顺序，后来者居上
+ 数字后面不可以加单位
+ 只有定位的盒子才有z-index属性

##### 定位的扩展

+ 加了绝对定位的盒子不可以通过margin水平居中 但是可以通过left50%＋margin-left半个盒子的距离来实现居中（垂直居中同理）
+ 行内元素添加固定或者绝对定位，可以直接设置高度和宽度
+ 浮动元素、绝对定位元素都不会触发外边距合并的问题
+ 浮动元素只会压住其底下标准流的盒子，但是不会压住下面标准流盒子里面的文字和图片，但绝对定位会完全压住下面标准流中的所有内容。（浮动不会压住文字图片的原因是，浮动本来就是用于文字围绕图片的）

如果一个盒子既有left属性又有right属性，则会默认执行left属性 同理有top bottom属性会执行top属性

### 属性的显示与隐藏

本质是让一个元素显示或者隐藏

+ ==display显示隐藏元素==
  + 属性值为none时表示隐藏对象
  + 属性值为block时表示转换为块级元素，同时还有显示元素的意思
  + 隐藏元素后盒子消失且占有的位置消失
+ visibility可见性
  + 属性值为visible元素可视
  + 属性值为hidden元素隐藏
  + 隐藏元素的盒子消失但是占有的位置还在
+ overflow溢出
  + 对内容超过盒子宽度高度的内容进行影响
  + 属性值visible显示
  + 属性值hidden隐藏
  + 属性值scroll溢出部分显示滚动条
  + 属性值auto自动添加滚动条（溢出显示滚动条，不溢出不显示）
  + 有定位的盒子慎用hidden属性值，因为其会隐藏多余的部分

# 滚动

有不少专门处理滚动行为的属性，在这里特别列出来：

```css
/* 一整块一整块的滑动 */
scroll-padding/scroll-margin: 0;

/* 元素竖向采用滑动格式 */
overflow-y: scroll;

/* 滑动条调色，前面是滑条颜色，后面是背景色 */
scrollbar-color: #007 #bada55;

/* 在内嵌滑动条元素滑到底时大滑动条不跟随滑动 */
overscroll-behavior: contain;

/* 留出滑动条位置，不让出现滑动条改变样式 */
scrollbar-gutter: stable both-edges;
```

# 其他

## 精灵图

为了有效的减少服务器接受和发送请求的次数，提高页面的加载速度，出现了CSS精灵技术（也称CSS Sprites）核心原理 将全部图片加载到一个大图片中 包含所有需要请求的小图片

##  字体图标

主要用于显示网页中通用的、常用的一些小图标，一般采用SVG/Unicode格式

+ 轻量：一个字体图标要比一系列的图像要小。一旦字体加载了，图标就会马上渲染出来，减少了服务器请求
+ 灵活性：本质其实是文字，可以很随意的改变颜色、产生阴影、透明效果、旋转等
+ 兼容性：几乎支持所有浏览器

## 计算规格

`calc`函数可以允许宽度进行运算：

```css
width:calc(100%-30px);
```

如果需要同时设置最大最小值，可以使用`clamp`函数解决：

```css
<style>
  h1 { font-size: clamp(2.2em, 3vw + 1em, 2.5em) }
</style>
```

## 阶梯值函数

在2023年年底增加的`round()`、`rem()`、`mod()`阶梯值函数适用于流体设计，流体设计概念则建议使用相对单位和 CSS 数学函数，根据视口大小动态调整整个网站元素。

```css
<style>
:root { --width: 527px }
/* round函数让容器更新为可以被25px整除的像素值 */
.round {
  width: round(var(--width), 25px); /* 525px */
}

/* rem函数取余 */
.rem {
  width: rem(var(--width), 25px); /* 2px */
}

/* mod函数取模，同取余，但符号取除数的符号 */
.mod {
  width: mod(var(--width), -25px); /* -2px */
}
</style>   
```

## 主题切换

除了使用`:root`选择器设置初值一点一点更改之外，浏览器提供了一种简单的方式用于适配光暗主题颜色：

```css
:root {
    color-scheme: dark/light;
}
```

可以在单个元素上使用这个属性。

## 表单元素颜色定制

对于表单元素而言我们可以用`accent-color`值来控制主题色：

```css
:root {
    accent-color: mediumvioletred;
}
```

## 大小自适应包裹

有时候遇到需要盒子里面有文字，希望直接进行一个包裹的，将其宽度自动调整为恰好适应其内容的大小，可以使用以下属性：

```css
width: fit-content;
```

## 边框图片

边框如果需要用到背景图片，可以采用`border-image`相关属性。

```css
border-image: <border-image-outset> <border-image-repeat> <border-image-slice> <border-image-source> <border-image-width>
```



## CSS计数器

随容器出现次数而增长的计数器。

```css
:root { counter-reset: references }

/* 带href的a标签出现过几次after伪元素就会显示对应的值 */
a[href]:empty::after {
    counter-increment: references;
    content: '[' counter(references) ']';
}
```

## 盒子模型计算

通过`box-sizing`来指定盒子模型：

```css
box-sizing:content-box(默认值，盒子大小按照width和height计算)/border-box(算上padding&border，便于布局用);
```

## 图片滤镜

```css
filter: url()/blur()(高斯模糊)/constrast()(对比度)/brightness()(亮度)/drop-shadow()(沿图像的轮廓生成阴影效果，语法类box-shadow)/grayscale()(转灰度图)/hue-rotate()(应用色相旋转)/invert()(反转输入图像)/opacity()(透明度)/saturate()(饱和度)/sepia()(改为深褐色)
```

## 过渡

盒子执行动作更加自然。

```css
transition: <transition-property> <transition-duration> <transition-timing-function> <transition-delay>
```

## 转换

转换`transform`是CSS3中具有颠覆性的特征之一，可以实现元素的位移、旋转、缩放等效果

[transform](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)

> 如果想要在网页中产生3D效果需要透视（理解成3D物体投影在2D平面中）
>
> ```css
> /* 两个写法作用一样 */
> perspective: val;
> transform: perspective();
> ```
>
> 透视我们也称为视距：视距就是人的眼睛到屏幕的距离，距离视觉点越近的在电脑平面成像就越大，越远成像越小，==透视写在被观察元素的父盒子上==

> ```css
> transform-style: flat/preserve-3d;
> ```
>
> 设置元素的子元素是位于 3D 空间中还是平面中.

## 动画

动画是CSS3中具有颠覆性的特征之一，可通过设置多个节点来精确控制一个或一组动画，通常用于实现复杂的动画效果、相比较过渡，动画可以实现更多变化，更多控制，连续自动播放等效果。

动画分两步，先**定义**动画，再**使用**动画

```css
/* 定义动画 */
@keyframes 动画名称{
0%{... : ... ;}
100%{... : ... ;}
}
```

```css
/* 使用动画 */
animation: <animation-name> <animation-duration> <animation-timing-function> <animation-delay> <animation-iteration-count> <animation-direction> <animation-fill-mode> <animation-play-state>
```

我们也可以在关键帧中更新css变量`@property`，这样就可以快速动画化多个元素，无需自己手写多个关键帧。

```css
/* 定义--t */
@property --t {
  syntax: "<number>";
  initial-value: 0;
  inherits: true;
}

/* 写--t动画逻辑 */
@keyframes tick {
  from { --t: 0 }
  to   { --t: 100000 }
}

/* 使--t动画一直运行 */
:root { animation: tick 86400s linear infinite }

/* 进而使盒子位置平滑发生循环移动 */
 div > div:first-child { translate: calc(sin(var(--t)) * 200px + 200px) }
 div > div:last-child { translate: calc(cos(var(--t)) * 200px + 200px) }
```

# 项目规划

### 样式的模块化开发

可以写部分CSS用于多个HTML文件 每当使用时就引用

### 制作网站favicon图标

将准备的图标切成png图片

将png图片转化为ico图标，这需要借助第三方的转化网站

将制作好的图标放在网页根目录下

在head标签中复制网站上的代码粘贴即可

### 网站TDK三大标签SEO优化

SEO汉译为搜索引擎优化，是一种利用搜索引擎的规则提高网站在有关搜索引擎内自然排名的方式。

前端人员不做SEO但是也要符合TDK三大标签优化

T：title 

+ title具有不可替代性，是我们内页的第一个重要标签，是搜索引擎了解网站的入口和对网页主题归属的最佳判断点

+ 建议：网站名（产品名）-网站的介绍（尽量不要超过30个汉字）

D：description

+ 简要说明网站是干什么的
+ 提倡description作为网站的总体业务和主题概括
+ 前端人员只需要准备好meta name="description" content=""/单标签给准备好就行 接下来交给SEO开发人员

K：keywords

+ keywords是网站的关键词，是搜索引擎的关注点之一
+ keywords最好限制在6~8个关键词，关键词之间用英文逗号隔开
+ meta name="keywords" content=""/

###   LOGO SEO 优化

+ logo中首先放一个h1标签，目的是提权，告诉搜索引擎，这个地方很重要

+ h1里面再放一个链接 可以返回首页的 把logo的背景图片给链接即可
+ 为了搜索引擎收录我们 我们来链接里面要放文字（网站名称），但是名字不要显示出来
  + 方法是font-size:0; 这样就看不见文字了
+ 最后给链接一个title属性，这样鼠标放在logo上就有提示文字了

# Flex布局原理

+ flex是“弹性布局”，用来为盒装模型提供最大的灵活性，任何一个容器都可以指定为flex布局

+ 当为父元素设置flex布局之后，子元素的float、clear、vertical-align属性将失效
+ 定义为display:flex；

### 常见父项属性

+ flex-direction：设置主轴的方向
  + 主轴与侧轴 默认主轴为x 侧轴为y
  + 属性值为row（x轴）/row-reverse（从右到左）/column（y轴）/column-reverse（从下到上）
+ justify-content：设置主轴上子元素的排列方式
  + 属性值为flex-start（默认）/flex-end（从尾部开始）/center（居中）/space-around（平分空间）/==space-between（先两边贴边 再平分剩余空间）==
+ flex-wrap：设置子元素是否换行
  + flex布局中 默认的子元素是不换行的 如果装不开 会缩小子元素的宽度 放到父元素里面
+ align-items：设置侧轴上的子元素的排列方式（单行）
  + 属性值为flex-start（默认）/flex-end（从尾部开始）/center（居中）/stretch（拉伸）-->变得和父级一样
+ align-content：设置侧轴上的子元素的排列方式（多行）
  + 设置子项在侧轴上的排列方式并且只能用于子项出现换行的情况，在单行下是没有效果的
  + flex-start（默认）/flex-end（从尾部开始）/center（居中）/space-around（平分空间）/space-between（先两边贴边 再平分剩余空间）/stretch（设置子项元素高度平分父元素高度）
+ flex-flow：复合属性

### 常见子项属性

+ flex子项目占的份数

  + 分配的是==剩余空间==

  + 样式为flex:数字;

+ align-self控制子项自己在侧轴的排列方式

  + align-self允许某单个项目有与其他项目不同的对齐方式 可以覆盖align-items

+ order属性定义子项的排列顺序（先后顺序）

  + 数值越小 排列越靠前 默认为0

