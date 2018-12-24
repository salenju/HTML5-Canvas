#    11-Canvas学习——图像合成

> 2018-12-21

> [参考链接](https://www.w3cplus.com/canvas/compositing.html)

> 深圳

## 0、基础知识

**合成**是指精确控制画布上对象的**透明度、分层效果**。默认情况下，在Canvas中，如果物体A（源）在物体B（目标）之上，那么浏览器就会简单的把A物体的图像叠放在B物体图像上面。

在Canvas中，把图像源和目标图像通过`globalCompositeOperation`操作，可以得到不同的效果：

![](images\11.0.1.png)

## 1、控制图像合成操作

- `globalAlpha`：设置图像的透明度。0（完全透明）——>1（完全不透明），默认值为1。该属性值必须设置在图形绘制之前
- `globalCompositeOperation`：在所有变换都生效后控制当前Canvas中绘制图形

## 2、图像合成类型

在Canvas中，`globalCompositeOperation`属性的值共有**26**种

详情见`11-Canvas学习——图像合成 .html`文件展示效果。

## 3、合成图像示例——刮刮卡

