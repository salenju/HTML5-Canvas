#    06-Canvas学习——绘制圆和圆弧

> 2018-12-20

> [参考链接](https://www.w3cplus.com/canvas/drawing-arc-and-circle.html)

> 深圳

Canvas中提供了两个方法：

- `arc()`：绘制**圆**
- `arcTo()`：绘制**圆弧**

## 1、与圆和圆弧相关的基础知识

### 1.1 角度旋转

旋转分为顺时针和逆时针两个旋转方向

![](images\6.1.1角度旋转.png)

### 1.2 角度和弧度

CSS中，旋转用的是**角度**（`deg`），但在Canvas中绘制圆或圆弧时用到的是**弧度**（`rad`）。

​	![](images\6.1.2 角度和弧度.svg)

一个整圆的弧度是`2π`，`2π rad = 360 deg，`1 deg= π/180 rad`，`1 rad = 180°/π deg`

> 弧度：rad = (π  * deg ) / 180 
>
> 角度：deg = (180 * rad ) / π

### 1.3 JavaScript中的弧度与角度换算

在JavaScript中`π`对应的是`Math.PI`

> 弧度：rad = (Math.PI  * deg ) / 180 
>
> 角度：deg = (180 * rad ) / Math.PI

为了后续使用方便，可以将二者间的转换封装为JavaScript函数：

```js
        // 角度（deg）转换为弧度（rad）方法
        function getRads(deg) {
            return (Math.PI * deg) / 180;
        }

        // 弧度（rad）转换为角度（deg）方法
        function getDegs(rad) {
            return (rad * 180) / Math.PI;
        }
```

### 1.4 正切

![](images\6.1.4 正切.svg)

## 2、arc()方法

> **arc(x, y, radius, startRad, endRad, [anticlockwise]);**

- `(x, y)`——圆心
- `startRad`——起始弧度（以`X`轴正向为基准，顺时针旋转的角度来计算得到的弧度）
- `endRad`——结束弧度（以`X`轴正向为基准，顺时针旋转的角度来计算得到的弧度）
-  `anticlockwise`——绘制圆弧或圆时是以顺时针还是逆时针方向开始绘制（`true`：逆时针，`false`：顺时针（默认值））

![](images\6.2.1 arc()方法中的参数.jpg)



## 3、绘制弧线

### 3.1 弧线——fill()

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        // 角度（deg）转换为弧度（rad）方法
        function getRads(deg) {
            return (Math.PI * deg) / 180;
        }

        // 弧度（rad）转换为角度（deg）方法
        function getDegs(rad) {
            return (rad * 180) / Math.PI;
        }

        // 绘制圆弧
        function drawArc(type) {
            var arc = {
                x: c.width / 2,
                y: c.height / 2,
                r: 100
            },
                w = c.width,
                h = c.height;

            ctx.moveTo(arc.x, 0);
            ctx.lineTo(arc.x, h);
            ctx.stroke();

            ctx.moveTo(0, arc.y);
            ctx.lineTo(w, arc.y);
            ctx.stroke();

            ctx.save();
            ctx.lineWidth = 10;
            type === "stroke"
                ? ctx.strokeStyle = "#E3F"
                : ctx.fillStyle = "#E3F"

            ctx.beginPath();
            ctx.arc(arc.x, arc.y, arc.r, getRads(-45), getRads(45));
            type === "stroke"
                ? ctx.stroke()
                : ctx.fill()
            ctx.closePath();

            ctx.beginPath();
            type === "stroke"
                ? ctx.strokeStyle = "#F36"
                : ctx.fillStyle = "#F36"
            ctx.arc(arc.x, arc.y, arc.r, getRads(-135), getRads(135), true);
            type === "stroke"
                ? ctx.stroke()
                : ctx.fill()
            ctx.closePath();
        }

        window.onload = function () {
            drawArc("fill");
        }
    </script>
```

效果图：

![](images\6.3.1 弧线——fill().JPG)

### 3.2 绘制弧线——stroke()

```js
        window.onload = function () {
            drawArc("stroke");
        }
```

效果图：

![](images\6.3.2弧线——stroke().JPG)

### 3.3 绘制超声波雷达图

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        // 角度（deg）转换为弧度（rad）方法
        function getRads(deg) {
            return (Math.PI * deg) / 180;
        }

        // 弧度（rad）转换为角度（deg）方法
        function getDegs(rad) {
            return (rad * 180) / Math.PI;
        }

        // 绘制超声波雷达图
        function drawRadarArc() {
            var arc = {
                x: c.width / 2,
                y: c.height / 2,
                r: 10
            },
                w = c.width,
                h = c.height;

            ctx.save();
            ctx.lineWidth = 2;
            ctx.strokeStyle = "#E3F"

            for (var i = 0; i < 10; i++) {
                ctx.beginPath();
                ctx.arc(arc.x, arc.y, arc.r * i, getRads(-45), getRads(45));
                ctx.stroke();
                ctx.closePath();

                ctx.beginPath();
                ctx.arc(arc.x, arc.y, arc.r * i, getRads(-135), getRads(135), true);
                ctx.stroke();
                ctx.closePath();
            }
        }

        window.onload = function () {
            drawRadarArc();
        }
```

效果图：

![](images\6.3.3  绘制超声波雷达图.JPG)

## 4、绘制圆形（太极图）

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        // 角度（deg）转换为弧度（rad）方法
        function getRads(deg) {
            return (Math.PI * deg) / 180;
        }

        // 弧度（rad）转换为角度（deg）方法
        function getDegs(rad) {
            return (rad * 180) / Math.PI;
        }

        // 绘制圆形(太极图)
        function drawCircle() {
            var arc = {
                x: c.width / 2,
                y: c.height / 2,
                r: 100
            },
                w = c.width,
                h = c.height;

            ctx.save();
            ctx.lineWidth = 1;
            // 绘制白色右半圆
            ctx.beginPath();
            ctx.fillStyle = "#FFF";
            ctx.arc(arc.x, arc.y, arc.r, getRads(-90), getRads(90), false);
            ctx.fill();
            ctx.closePath();

            // 绘制黑色左半圆
            ctx.beginPath();
            ctx.fillStyle = "#000";
            ctx.arc(arc.x, arc.y, arc.r, getRads(-90), getRads(90), true);
            ctx.fill();
            ctx.closePath();

            // 绘制白色小圆
            ctx.beginPath();
            ctx.fillStyle = "#FFF";
            ctx.arc(arc.x, arc.y-arc.r/2, arc.r/2, getRads(0), getRads(360), false);
            ctx.fill();
            ctx.closePath();

            // 绘制黑色小圆
            ctx.beginPath();
            ctx.fillStyle = "#000";
            ctx.arc(arc.x, arc.y+arc.r/2, arc.r/2, getRads(0), getRads(360), false);
            ctx.fill();
            ctx.closePath();

            // 绘制小黑点
            ctx.beginPath();
            ctx.fillStyle = "#000";
            ctx.arc(arc.x, arc.y-arc.r/2, arc.r/8, getRads(0), getRads(360), false);
            ctx.fill();
            ctx.closePath();

            // 绘制小白点
            ctx.beginPath();
            ctx.fillStyle = "#FFF";
            ctx.arc(arc.x, arc.y+arc.r/2, arc.r/8, getRads(0), getRads(360), false);
            ctx.fill();
            ctx.closePath();
        }

        window.onload = function () {
            drawCircle();
        }
    </script>
```

效果图：

![](images\6.4 绘制圆形（太极图）.JPG)

## 5、arcTo()

> **arcTo(x1, y1, x2, y2, radius)**：利用当前端点、端点一`（x1, y1）`和端点二`(x2, y2)`这三点所形成的夹角，然后绘制一段与夹角的两边都相切且半径为`radius`的圆上的弧线

- x1, y1——端点一
- x2, y2——端点二
- radius——弧线所在圆的半径

![](images\6.5.1 arcTo()参数解析.png)

![](images\6.5.2 arcTo()参数解析.png)

实际绘制步骤：

- `moveTo()`给出`P0`点的坐标
- `arcTo()`函数中的参数给出了`P1`和`P2`点的坐标，以及圆形的半径`r`
- 根据半径`r`和直线`P0P1`和`P1P2`计算出对应的切点，记为`S`点和`E`点
- 从`P0`向`S`点画一条线段
- 以半径`r`为半径从`S`点到`E`点画出一段圆弧
- 从`E`点向`P2`点画一条线段
- 至此`arcTo()`的任务已经完成，下来就可以`stroke()`或`fill()`了

### 5.1 绘制月亮





