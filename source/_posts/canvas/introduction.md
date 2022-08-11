---
layout: post
title: Canvas 入门
date: 2022-08-11 10:43:57
categories: Canvas
tags: 
    - Canvas
---

## Canvas是什么？

* Canvas是一个可以使用JavaScript来绘制图形的HTML元素。
* Canvas拥有多种绘制路径、矩形、圆形、字符以及图片的方法。
* Canvas可用于动画、游戏、数据可视化、图片编辑器、实时视频处理等领域。

## Canvas基本用法

1. 在html中创建canvas元素
2. 通过js获取canvas元素
3. 通过使用 getContext() 方法来访问绘画上下文
4. 绘制图形

{% asset_img 1.png %}

~~~ html
<body>
    <!-- 1.创建canvas元素 -->
    <canvas id="lsyCanvas" width="150" height="150"></canvas>
    <script>
        // 2.通过js获取canvas元素
        const contextCanvas = document.getElementById('lsyCanvas')

        // 3.通过使用 getContext() 方法来访问绘画上下文
        if(contextCanvas.getContext) {
            const cxt = contextCanvas.getContext('2d');

            // 4. 绘制图形
            cxt.moveTo(100, 100); // 起点坐标(x,y)
            cxt.lineTo(200, 200); // 终点坐标(x,y)
            cxt.stroke(); // 将起点跟终点连接起来
        }
    </script>
</body>
~~~

> **注意：**如果绘制出来的图形是扭曲的，需要用canvas里面的width、height设置，而不是CSS。

## Canvas 绘制图形

### 坐标系

在绘制基础图形之前，需要先搞清除 Canvas 使用的坐标系。

Canvas 使用的是 W3C 坐标系 ，也就是遵循我们屏幕、报纸的阅读习惯，从上往下，从左往右。

{% asset_img 2.png %}

### 绘制矩形

canvas相比与svg来说只支持两种形式的图形绘制：矩形和路径（由一系列的点连成的线段）。

canvas提供了三种绘制矩形：

1. fillRect(x, y, width, height) 绘制一个填充的矩形
2. strokeRect(x, y, width, height) 绘制一个矩形的边框
3. clearRect(x, y, width, height)  清除指定矩形区域，让清除部分完全透明。

x 与 y 指定了在 canvas 画布上所绘制的矩形的左上角（相对于原点）的坐标。width 和 height 设置矩形的尺寸。

{% asset_img 3.png %}

~~~ html
<body>
    <canvas id="lsyCanvas" width="150" height="150"></canvas>

    <script>
        const contextCanvas = document.getElementById('lsyCanvas')
        if(contextCanvas.getContext) {
            const cxt = contextCanvas.getContext('2d')
            cxt.fillRect(25,25,100,100); // 绘制一个100*100的黑色正方形
            cxt.clearRect(45,45,60,60); // 从黑色正方形的中间擦除 60*60的正方形
            cxt.strokeRect(50,50,50,50) // 绘制一个50*50的正方形边框
        }
    </script>
</body>
~~~

### 绘制路径

绘制路径的步骤：

1. 调用beginPath()方法创建路径起始点。
2. 使用画图命令moveTo，lineTo方法画出路径。
3. 调用closePath()把路径闭合，非必须。如果绘制的图形已经是闭合的，就可以不用调用此方法。
4. 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。

需要用到的canvas的函数

- beginPath()
  - 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径
- closePath()
  - 闭合路径之后图形绘制命令又重新指向上下文中
- stroke()
  - 通过线条来绘制图形轮廓
- fill()
  - 通过填充路径的内容区域生成实心的图形

### 绘制三角形

{% asset_img 4.png %}

~~~ html
<body>
    <canvas id="lsyCanvas" width="150" height="150"></canvas>
    <script>
        const contextCanvas = document.getElementById('lsyCanvas');
        if(contextCanvas.getContext) {
            const cxt = contextCanvas.getContext('2d')
            cxt.beginPath()
            cxt.moveTo(75,25)
            cxt.lineTo(75,75)
            cxt.lineTo(50,50)
            cxt.fill()
        }
    </script>
</body>
~~~

#### 移动笔触

在canvas初始化或者调用beginPath方法之后，使用moveTo()函数设置图形的起点。

#### 线

绘制直线需要用到lineTo()方法

下面的例子绘制两个三角形，一个填充三角形，一个描边三角形

{% asset_img 5.png %}

~~~ html
<body>
    <canvas id="lsyCanvas" width="200" height="200"></canvas>
    <script>
        const contextCanvas = document.getElementById('lsyCanvas')
        if(contextCanvas.getContext) {
            const cxt = contextCanvas.getContext('2d')

            // 绘制填充三角形
            cxt.beginPath()
            cxt.moveTo(25,25);
            cxt.lineTo(125,25);
            cxt.lineTo(25,75);
            cxt.fill();

            // 绘制描边三角形
            cxt.beginPath();
            cxt.moveTo(45, 100);
            cxt.lineTo(145,100);
            cxt.lineTo(145, 45);
            cxt.closePath()
            cxt.stroke()
        }
    </script>
</body>
~~~

在绘制描边三角形的时候，你会发现，如果不使用closePath()，绘制的图形没有闭合。

### 圆弧

绘制圆弧或者圆，使用arc()方法。

arc(x, y, radius, startAngle, endAngle, anticlockwise)

画一个以(x,y)为圆心，以radius为半径画一个从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。

anticlockwise接收以个Boolean类型的数值，为 true 时，是逆时针方向，否则顺时针方向。

> **注意：**arc()函数中表示角的单位是弧度，不是角度。角度与弧度的js表达式：弧度=(Math.PI/180)*角度。

#### 绘制笑脸

{% asset_img 6.png %}

~~~ html
<body>
    <canvas id="lsyCanvas" width="200" height="200"></canvas>
    
    <script>
        const contextCanvas = document.getElementById('lsyCanvas');
        if(contextCanvas.getContext) {
            const cxt = contextCanvas.getContext('2d')

            cxt.beginPath();
            cxt.arc(100, 100, 50, 0, Math.PI * 2, true) // 绘制圆形
            cxt.moveTo(135, 100)
            cxt.arc(100, 100, 35, 0, Math.PI, false) // 绘制嘴
            cxt.moveTo(90,90)
            cxt.arc(85, 90, 5, 0, Math.PI * 2, true) // 绘制左眼
            cxt.moveTo(120,90)
            cxt.arc(115, 90, 5, 0, Math.PI * 2, true) // 绘制右眼
            cxt.stroke();
        }
    </script>
</body>
~~~
