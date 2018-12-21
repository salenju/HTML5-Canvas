#    09-Canvas学习——坐标变换

> 2018-12-21

> [参考链接](https://www.w3cplus.com/canvas/transformation-coordinates.html)

> 深圳

## 0、基础知识

Canvas坐标系：左上角为原点（0,0）

![](images\9.0 Canvas坐标系.png)

但在很多场景中，C	anvas坐标变化可以更为方便快捷的实现需求。

## 1、移动——Translating

**translate(x, y)**

- `x`：左右偏移量
- `y`：上下偏移量

![](images\9.1 translate.png)

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");
        var w = c.width,
            h = c.height;

        // translate
        function drawTanslate() {
            for (var i = 0; i < 4; i++) {   // x
                for (var j = 0; j < 4; j++) {   // y
                    ctx.fillStyle = "rgba(" + (120 + j * 10) + "," + (185 - i * 10) + "," + (10 + j * 3) + ",1)";
                    ctx.save();

                    // 通过translate移动坐标
                    ctx.translate(i * (w - 50) / 4 + (i + 1) * 10, j * (h - 50) / 4 + (j + 1) * 10);
                    // 每一个矩形的起点都是(0,0)
                    ctx.fillRect(0, 0, (w - 50) / 4, (h - 50) / 4);
                    ctx.restore();
                }
            }
        }

        window.onload = function () {
            drawTanslate();
        }
    </script>
```

效果图：

![](images\9.1. translate绘制方格.JPG)

## 2、旋转Rotating

**rotate(angle)**

- `angle`：弧度（顺时针方向旋转）

> **注意**：对某个图形元素做旋转，默认情况下会以Canvas坐标系统的原点（0,0）进行旋转。但实际上，需要围绕元素中心点做旋转

![](images\9.2 rotate.png)

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");
        var w = c.width,
            h = c.height;

        // rotate
        function drawRotate(ctx, w, h) {
            // 将Canvas画布坐标原点移动到画布中心位置
            ctx.translate(w / 2, h / 2);
            for (var i = 0; i < 10; i++) {  // 圈数
                ctx.save();
                ctx.fillStyle = "rgba(" + ( i * 50) + "," + (255 - i * 50) + ",255)";
                
                for (var j = 0; j < i * 10; j++) {  // 每圈圆点个数
                    // 旋转坐标
                    ctx.rotate(Math.PI *2/(i * 10));
                    ctx.beginPath();
                    ctx.arc(0,i*20,5,0,Math.PI*2,true);
                    ctx.fill();
                    ctx.closePath();
                }
                ctx.restore();
            }
        }

        window.onload = function () {
            drawRotate(ctx,w,h);
        }
    </script>
```

效果图：

![](images\9.2.1 rotate实例.JPG)

## 3、缩放Scaling

**scale(x,y)**

- `x`：横轴（x轴）的缩放因子
- `y`：纵轴（y轴）的缩放因子

缩放因子默认是`1`，如果`< 1`是缩小，如果`> 1`是放大

> **注意**：围绕元素中心进行缩放

![](images\9.3 scale.png)



## 4、小结

|      方法       |                             描述                             |
| :-------------: | :----------------------------------------------------------: |
|  rotate(angle)  |                   按照给定的弧度顺时针旋转                   |
|   scale(x, y)   | 在x和y周方向上分别按照给定的数值来缩放坐标系，默认值是1，>1是放大，<1是缩小 |
| translate(x, y) |                  将坐标平移到（x, y）坐标处                  |

