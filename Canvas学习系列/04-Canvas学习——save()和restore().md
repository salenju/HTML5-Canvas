#    04-Canvas学习——save()和restore()

> 2018-12-18

> [参考链接](https://www.w3cplus.com/canvas/canvas-states.html)

> 深圳

## 1、Canvas状态的保存和恢复

- `save()`：保存当前状态
- `restore()`：还原之前保存的状态

## 2、理解save()和restore()

> `save()`保存的只是`CanvasRenderingContext2D `对象的状态以及对象的所有属性，并不包括这个对象上绘制的图形

`CanvasRenderingContext2D `的当前属性值主要包括：

| 属性                     | 描述                                                         |
| ------------------------ | ------------------------------------------------------------ |
| canvas                   | 取得画布<canvas>元素                                         |
| fillStyle                | 填充路径当前的颜色、模式、渐变                               |
| globalCompositeOperation | 指定颜色如何与画布上已有颜色组合（合成）                     |
| lineCap                  | 线段端点的绘制方式                                           |
| lineJoin                 | 线段连接的绘制方式                                           |
| lineWidth                | 线段的宽度                                                   |
| miterLimit               | 当`lineJoin`为`miter`时，这个属性指定斜连接长度和二分之一线宽的最大比率 |
| shadowColor              | 阴影颜色                                                     |
| shadowBlur               | 阴影模糊度                                                   |
| shadowOffsetX            | 阴影水平偏移值                                               |
| shadowOffsetY            | 阴影垂直偏移值                                               |
| strokeStyle              | 线段颜色                                                     |

![](images/4.2 理解save()和restore().png)

## 3、实例理解save()和restore()

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");

        function drawScreen() {
            ctx.fillStyle = "#FA6900";
            ctx.shadowOffsetX = 5;
            ctx.shadowOffsetY = 5;
            ctx.shadowBlur = 4;
            ctx.shadowColor = "rgba(204, 204, 204, 0.5)";
            ctx.fillRect(10, 10, 15, 150);
            ctx.save(); // 将第一个状态存到堆栈中

            ctx.fillStyle = "#F36";
            ctx.shadowOffsetX = 10;
            ctx.shadowOffsetY = 10;
            ctx.shadowBlur = 4;
            ctx.shadowColor = "rgba(204, 204, 204, 0.5)";
            ctx.fillRect(50, 10, 30, 150);
            ctx.save(); // 将第二个转态存在堆栈中

            ctx.fillStyle = "#A7DBD7";
            ctx.shadowOffsetX = 15;
            ctx.shadowOffsetY = 15;
            ctx.shadowBlur = 4;
            ctx.shadowColor = "rgba(204, 204, 204, 0.5)";
            ctx.fillRect(110, 10, 45, 150);
            ctx.save(); // 将第三个转态存在堆栈中

            ctx.restore();  // 取出堆栈3（第三个状态）
            ctx.beginPath();
            ctx.arc(225,75,22,0,Math.PI*2,true);
            ctx.closePath();
            ctx.fill();

            ctx.restore();  // 取出堆栈2（第二个状态）
            ctx.beginPath();
            ctx.arc(320,75,15,0,Math.PI*2,true);
            ctx.closePath();
            ctx.fill();

            ctx.restore();  // 取出堆栈1（第一个状态）
            ctx.beginPath();
            ctx.arc(400,75,8,0,Math.PI*2,true);
            ctx.closePath();
            ctx.fill();
        }

        window.onload = function () {
            drawScreen();
        }
    </script>
```

效果图：

![](images/4.3 实例理解save()和restore().JPG)

