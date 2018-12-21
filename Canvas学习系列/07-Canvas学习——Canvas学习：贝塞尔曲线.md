#    07-Canvas学习：贝塞尔曲线

> 2018-12-21

> [参考链接](https://www.w3cplus.com/canvas/drawing-curve.html)

> 深圳

# 1、贝塞尔曲线基础

## 1.1 二次方贝塞尔曲线

![](images\canvas-10-14.gif)

## 1.2 三次方贝塞尔曲线

![](images\canvas-10-16.gif)

### 1.3 贝塞尔曲线绘制原理

第一步：在平面内任选3个不共线的点，并依次连接

![](images\7.1.3.1.png)

第二步：在`AB`上任选一个点D，计算`AD`与线段总长`AB`的比例

![](images\7.1.3.2.png)

第三步：在`BC`上找出对应的点E使得`AD:AB = BE:BC`

![](images\7.1.3.3.png)

第四步：连接点D和点E，在`DE`上找到相同比例的点F，使得`DF:DE = AD:AB = BE:BC`

![](images\7.1.3.4.png)

点F即为贝塞尔曲线上的一个点，利用极限的知识，当点D从点A移动到点B的时候，所找出的所有点F连接即形成了贝塞尔曲线。

![](images\7.1.3.5.png)

## 2、Canvas中使用贝塞尔曲线

### 2.1 二次贝塞尔曲线

**quadraticCurveTo(cp1x, cp1y, x, y)**

二次贝塞尔曲线有：`1`个起始点（可以通过`moveTo()`或`lineTo()`来定义）、`1`个终止点、`1`个控制点。

- (cp1x, cp1y)：唯一个控制点
- (x, y)：终止点

#### 2.1.1 绘制二次贝塞尔曲线

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        // 绘制二次贝塞尔曲线
        function drawQuadraticCurve() {
            ctx.lineWidth = 1;
            ctx.strokeStyle = "#F36";
            ctx.fillStyle = "red";

            // 绘制起始点
            ctx.fillRect(100 - 4, 50 - 4, 8, 8);
            ctx.fillRect(100 - 4, 200 - 4, 8, 8);
            ctx.fillRect(300 - 4, 200 - 4, 8, 8);

            // 用直线连接两个参考点
            ctx.beginPath();
            ctx.strokeStyle = "red";
            ctx.moveTo(100,50);
            ctx.lineTo(100,200);
            ctx.lineTo(300,200);
            ctx.stroke();
            ctx.closePath();

            // 调用quadraticCurveTo()绘制二次贝塞尔曲线
            ctx.beginPath();
            ctx.strokeStyle="blue";
            ctx.moveTo(100,50);
            ctx.quadraticCurveTo(100,200,300,200);
            ctx.stroke();
            ctx.closePath();
        }

        window.onload = function () {
            drawScreen();
        }
    </script>
```

效果图：

![](images\7.2.1 二次贝塞尔曲线.JPG)

#### 2.1.2 绘制气泡

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d")；

        // 绘制气泡
        function drawBubble() {
            ctx.lineWidth = 1;
            ctx.strokeStyle = "#F36";
            ctx.fillStyle = "red";

            ctx.beginPath();
            ctx.moveTo(75, 25);
            ctx.quadraticCurveTo(25, 25, 25, 62.5);
            ctx.quadraticCurveTo(25, 100, 50, 100);
            ctx.quadraticCurveTo(50, 120, 30, 125);
            ctx.quadraticCurveTo(60, 120, 65, 100);
            ctx.quadraticCurveTo(125, 100, 125, 62.5);
            ctx.quadraticCurveTo(125, 25, 75, 25);
            ctx.stroke();
            ctx.closePath();
        }

        window.onload = function () {
            drawBubble();
        }
    </script>
```

效果图：

![](images\7.2.1.2 绘制气泡.JPG)

## 3、三次贝塞尔曲线

**bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)**

三次贝塞尔曲线有：`1`个起始点（可以通过`moveTo()`或`lineTo()`来定义）、`1`个终止点、`2`个控制点。

- (cp1x, cp1y)：控制点`cp1`
- (cp2x, cp2y)：控制点`cp2`
- (x, y)：终止点`(x, y)`

### 3.1 绘制三次贝塞尔虚线

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        // 绘制三次贝塞尔曲线
        function drawBezierCurve() {
            ctx.lineWidth = 1;
            ctx.strokeStyle = "#F36";
            ctx.fillStyle = "red";

            // 绘制起始点/控制点
            ctx.fillRect(100 - 4, 50 - 4, 8, 8);
            ctx.fillRect(100 - 4, 200 - 4, 8, 8);
            ctx.fillRect(300 - 4, 200 - 4, 8, 8);
            ctx.fillRect(400 - 4, 150 - 4, 8, 8);

            ctx.beginPath();
            ctx.strokeStyle = "red";
            ctx.moveTo(100, 50);
            ctx.lineTo(100, 200);
            ctx.stroke();
            ctx.save();

            ctx.beginPath();
            ctx.restore();
            ctx.moveTo(300, 200);
            ctx.lineTo(400, 150);
            ctx.stroke();
            ctx.closePath();

            // 绘制三次贝塞尔曲线
            ctx.beginPath();
            ctx.strokeStyle = "purple";
            ctx.moveTo(100, 50);
            ctx.bezierCurveTo(100, 200, 300, 200, 400, 150);
            ctx.stroke();
            ctx.closePath();
        }

        window.onload = function () {
            drawBezierCurve();
        }
    </script>
```

效果图：

![](images\7.3.1 绘制三次贝塞尔曲线.JPG)

### 3.2 绘制心形

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        // 绘制心形
        function drawHeart() {
            ctx.lineWidth = 1;
            ctx.fillStyle = "pink";

            ctx.beginPath();
            ctx.moveTo(75, 40);
            ctx.bezierCurveTo(75, 37, 70, 25, 50, 25); 
            ctx.bezierCurveTo(20, 25, 20, 62.5, 20, 62.5); 
            ctx.bezierCurveTo(20, 80, 40, 102, 75, 120); 
            ctx.bezierCurveTo(110, 102, 130, 80, 130, 62.5); 
            ctx.bezierCurveTo(130, 62.5, 130, 25, 100, 25); 
            ctx.bezierCurveTo(85, 25, 75, 37, 75, 40); 
            ctx.fill();
        }

        window.onload = function () {
            drawHeart();
        }
    </script>
```

效果图：

![](images\7.3.2 绘制心形.JPG)

