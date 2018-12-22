#    10-Canvas学习——绘制文本

> 2018-12-21

> [参考链接](https://www.w3cplus.com/canvas/drawing-text.html)

> 深圳

## 0、基础知识

Canvas对象提供了两种方法来渲染文本：

- `fillText(text, x, y, [maxWidth])`：绘制填充文本
- `strokeText(text, x, y, [maxWidth])`：绘制描边文本

Canvas提供了类似CSS的一些`font`属性，用来修饰Canvas中绘制的文本：

- `font = value`：修饰绘制文本的样式
- `textAlign = value`：文本对齐设置
- `textBaseLine = value`：文本基线对齐设置
- `direction = value`：文本方向的设置

## 1、文本的填充和描边

### 1.1  文本填充——fillText()

**fillText(text, x, y, [maxWidth])**

- `text`：需要绘制的文本内容
- `x`：绘制文本在Canvas画布中起始位置的`X`轴坐标
- `y`：绘制文本在Canvas画布中起始位置的`Y`轴坐标
- `maxWidth`：绘制文本的最大宽度，如果绘制文本的内容超过了`maxWidth`则会压缩文本至`maxWidth`宽

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");
        var w = c.width,
            h = c.height;

        // 绘制填充文本
        function drawFillText(ctx, text, w, h) {
            ctx.fillStyle = "#F90";
            ctx.textAlign = "center";
            ctx.font = "48px Airal";

            ctx.fillText(text, w / 2, h / 2);
        }

        window.onload = function () {
            drawFillText(ctx, "Hello,Salen!", w, h);
        }
    </script>
```

效果图：

![](images\9.1.1 fillText.JPG)

### 1.2 文本描边——strokeText()

**strokeText(text, x, y, [maxWidth])**

- `text`：需要绘制的文本内容
- `x`：绘制文本在Canvas画布中起始位置的`X`轴坐标
- `y`：绘制文本在Canvas画布中起始位置的`Y`轴坐标
- `maxWidth`：绘制文本的最大宽度，如果绘制文本的内容超过了`maxWidth`则会压缩文本至`maxWidth`宽

```js
    <script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");
        var w = c.width,
            h = c.height;

        // 绘制描边文本
        function drawStrokeText(ctx, text, w, h) {
            ctx.strokeStyle = "#F90";
            ctx.textAlign = "center";
            ctx.font = "48px Airal";

            ctx.strokeText(text, w / 2, h / 2);
        }

        window.onload = function () {
            drawStrokeText(ctx, "Hello,Salen!", w, h);
        }
    </script>
```

效果图:

![](images\9.1.2 strokeText.JPG)

## 1.3 strokeText() + fillText()

```js
<script>
        var c = document.getElementById("myCanvas");
        var ctx = c.getContext("2d");
        var w = c.width,
            h = c.height;

        // 绘制填充 + 描边文本
        function drawText(ctx, text, w, h) {
            ctx.strokeStyle = "#0081CC";
            ctx.fillStyle = "#F40";
            ctx.lineWidth = 2;
            ctx.font = "48px Airal";
            ctx.textAlign = "center";

            ctx.fillText(text, w / 2, h / 2);
            ctx.strokeText(text, w / 2, h / 2);
        }

        window.onload = function () {
            drawText(ctx, "Hello,Salen!", w, h);
        }
    </script>
```

效果图：

![](images\9.1.3 fillText + strokeText.JPG)



### 1.4 环形文字

