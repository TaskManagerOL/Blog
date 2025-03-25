---
title: Canvas
date: 2023-07-21 15:53:10
tags: [笔记,前端]
excerpt: Canvas画布学习，很多特殊效果都是用这个实现的。
categories: 技术栈
---

# canvas画布使用——CSS进阶

​		在大一的时候学的一些高数、线性代数都可以用于canvas画布，所以还是很重要的，能好好学就好好学。

​		文章参考：[在canvas上绘制3d图形 - 简书 (jianshu.com)](https://www.jianshu.com/p/e3ebe08dddad)(写得真的很好，少见的好文章)

### 简单绘制三维图形

​		因为canvas是一个二维的东西，所以我们想要画出三维的图形就要考虑把这个三维图形给投影到二维上，进而给造成一种三维的错觉。所以首先需要学习的是如何表示三维坐标轴上的任意一个点。通过文章中的推导我们可以看到：

​		从空间内的任意点A(xA，yA，zA)观察空间内的任一点G(xG，yG，zG)，它在xy平面内的投影H的坐标为：

​		 $x = ((xG-xA)*zA)/(zA-zG) ;  y = ((yG-yA)*zA)/(zA-zG)$

###  三维图形 的旋转

​		对于一个图形，如果要对其进行y轴的旋转（从观察点更为明显且符合逻辑），则从y轴向下俯视xz平面可以使用一个极坐标的逻辑从而确定我们变换之后的坐标点。
​		主要就是确定每个点（控制旋转的是角度）

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMDk2NTEyMi1kMmM1NWUzNTFhMmQ0Zjc1LnBuZz9pbWFnZU1vZ3IyL2F1dG8tb3JpZW50L3N0cmlwfGltYWdlVmlldzIvMi93LzMxMS9mb3JtYXQvd2VicA?x-oss-process=image/format,png)

​		这个时候假定D点与x轴的夹角是α，圆的半径为R，将D点绕着y轴旋转β旋转至D'点，这个时候D'与x轴夹角为α+β，此时D'的x坐标为cos(α+β)*R，D'的z坐标为sin(α+β)*R

​	D'的x坐标:

​		$cos(α+β)*R=R*cosα*cosβ-R*sinα*sinβ$

D'的z坐标sin(α+β)*R=R*sinα*cosβ+R*cosα*sinβ
而R*sinα就是旋转之前D点的z坐标，R*cosα就是旋转之前D点的x坐标，
D'的x坐标为x*cosβ-z*sinβ
D'的z坐标为z*cosβ+x*sinβ
将结论代入到我们的立方体的8个顶点ABCDEFGH中
对于任一点D(xD，yD，zD)，其绕y轴旋转β角的时候，它的三维坐标变为(xD*cosβ-zD*sinβ，yD，zD*cosβ+xD*sinβ)

### 正弦曲线阵（含代码）

​		博客中写的是vue2的，我自己用的是vue3，所以以下是我已经写好的正弦曲线阵代码。

```html
<canvas ref="wave" :width="canvasWidth" :height="canvasHeight"></canvas>
```

```javascript
//绘制正弦波浪canvas
import { ref, watch } from 'vue'; 
const wave = ref('')
const canvasWidth = ref(1920)
const canvasHeight = ref(800)
//构建一个结构体 方便后期绘制多条正弦曲线
class Line {
    constructor (a, b, c, d, z, start, end, gap) {
        this.a = a
        this.b = b
        this.c = c
        this.d = d  //以上四个控制正弦函数振幅周期之类的
        this.z = z  //三维坐标
        this.start = start //绘画开始点
        this.end = end  //绘画结束点
        this.gap = gap //间距
        this.pointList = []
        this.computePointList()
    }
    computePointList () {
        this.pointList = []
        for (let i = this.start; i <= this.end; i = i + this.gap) {
            let x = i
            let y = this.a * Math.sin((this.b * x + this.c) / 180 * Math.PI) + this.d   // 即y = A sin(ωx + φ) + B
            let offset = i //偏移量用来让他运动
            this.pointList.push({
                x,
                y,
                z: this.z,
                originX: x,
                offset
            })
        }
    }
}
const lineList = [
    new Line(20, 2, 0, 0, -390, -300, 300, 10),
    new Line(20, 2, 0, 0, -360, -300, 300, 10),
    new Line(20, 2, 0, 0, -330, -300, 300, 10),
    new Line(20, 2, 0, 0, -300, -300, 300, 10),
    new Line(20, 2, 0, 0, -270, -300, 300, 10),
    new Line(20, 2, 0, 0, -240, -300, 300, 10),
    new Line(20, 2, 0, 0, -210, -300, 300, 10),
    new Line(20, 2, 0, 0, -180, -300, 300, 10),
    new Line(20, 2, 0, 0, -150, -300, 300, 10),
    new Line(20, 2, 0, 0, -120, -300, 300, 10),
    new Line(20, 2, 0, 0, -90, -300, 300, 10),
    new Line(20, 2, 0, 0, -60, -300, 300, 10),
    new Line(20, 2, 0, 0, -30, -300, 300, 10),
    new Line(20, 2, 0, 0, 0, -300, 300, 10),
    new Line(20, 2, 0, 0, 30, -300, 300, 10),
    new Line(20, 2, 0, 0, 60, -300, 300, 10),
    new Line(20, 2, 0, 0, 90, -300, 300, 10),
    new Line(20, 2, 0, 0, 120, -300, 300, 10),
    new Line(20, 2, 0, 0, 150, -300, 300, 10),
    new Line(20, 2, 0, 0, 180, -300, 300, 10),
    new Line(20, 2, 0, 0, 210, -300, 300, 10),
    new Line(20, 2, 0, 0, 240, -300, 300, 10),
    new Line(20, 2, 0, 0, 270, -300, 300, 10),
    new Line(20, 2, 0, 0, 300, -300, 300, 10),
    
]//整个类的列表出来

const draw = (visual) => { //这是个绘制正弦点的函数
    const context = wave.value.getContext("2d");
    context.clearRect(0, 0, canvasWidth.value, canvasHeight.value) //清空像素
    lineList.forEach(line => {
        line.pointList.forEach(item => {
            const pointSize = 1.5 * visual.z / (visual.z - item.z) //整个近大远小
            context.beginPath()
            context.arc(item.canvasX  + canvasWidth.value / 2, item.canvasY  + canvasHeight.value / 2, pointSize, 0, 2 * Math.PI) //arc(x, y, radius, startAngle, endAngle, counterclockwise);
            context.closePath()
            context.fill()
        })
    })
}
const updatePointList = (rotationAngleSpeed, visual) => { //这是个更新点的位置而使正弦函数移动的函数
    lineList.forEach(line => {
        line.pointList.forEach(item => {
            let x = item.x
            let z = item.z
            item.x = x * Math.cos(rotationAngleSpeed / 180 * Math.PI) - z * Math.sin(rotationAngleSpeed / 180 * Math.PI) 
            item.z = z * Math.cos(rotationAngleSpeed / 180 * Math.PI) + x * Math.sin(rotationAngleSpeed / 180 * Math.PI) 
            item.y = line.a * Math.sin((line.b * item.originX + line.c + item.offset) / 180 * Math.PI) + line.d //绕y轴旋转所以y比较特别
            item.canvasX = (item.x - visual.x) * visual.z / (visual.z - z)
            item.canvasY = (item.y - visual.y) * visual.z / (visual.z - z)
            })
    })
}

const animationFrame = (visual) => { //正弦函数动画
    window.requestAnimationFrame(() => {
        lineList.forEach((line,index) => {
            line.pointList.forEach(item => {
            line.c = item.offset + index * 30 //index控制偏移量更美观
            item.offset = item.offset + 1
            })
            updatePointList(.003,visual)
        })
        draw(visual)
        animationFrame(visual)
    })
}
//监听canvas标签创建、因为JS比标签创建更快，所以需要监听。
watch(wave, (newValue, oldValue) => {
    const visual = { //观察点设置
        x: 0,
        y: -70,
        z: 500
    }
    draw(visual);
    animationFrame(visual)
})

```

