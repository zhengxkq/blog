---
title: css鲜为人知的属性
---
### pointer-events
###### 属性：auto | none | visiblepainted | visiblefill | visiblestroke | visible | painted | fill | stroke | all

######  默认值：auto

######  取值：
1. auto：与pointer-events属性未指定时的表现效果相同。在svg内容上与visiblepainted值相同
2. none：元素永远不会成为鼠标事件的target。但是，当其后代元素的pointer-events属性指定其他值时，鼠标事件可以指向后代元素，在这种情况下，鼠标事件将在捕获或冒泡阶触发父元素的事件侦听器。
3. ++其他值只能应用在SVG上。++

###### 说明：设置或检索在何时成为属性事件的target。
使用pointer-events来阻止元素成为鼠标事件目标不一定意味着元素上的事件侦听器永不会触发。如果元素后代明确指定了pointer-events属性并允许其成为鼠标事件的目标，那么指向该元素的任何事件在事件传播过程中都将通过父元素，并以适当的方式触发其上的事件侦听器。当然位于屏幕上在父元素上但不在后代元素上的鼠标活动都不会被父元素和后代元素捕获（将会穿过父元素而指向位于其下面的元素）。

对应的脚本特性为pointerEvents。

---
### attr

```
[data-unit]:after{
    content:attr(data-unit);
    color:red;
}
```
```
<p data-unit="元">余额3</p>
```
###### 效果：
![image](https://raw.githubusercontent.com/zhangtingqian/img/master/yu.png)

---
### currentColor 
> 是clolr属性的值


```
.box{
    width: 100px;
    height: 100px;
    color: red;
    border: 1px solid currentColor;
    //border: 1px solid;和currentColor效果一样，都是color的值；
}
```
```
<div class="box">测试</div>
```

---
### user-select
> 禁止选择文本

---
### ::selection
> 可设置文字被选择时的样式

```
.box1::selection{
            background: red;
            color: yellow;
        }
```

```
<div class="box1">测试</div>
```
###### 效果：
![image](https://raw.githubusercontent.com/zhangtingqian/img/master/1.png)![image](https://raw.githubusercontent.com/zhangtingqian/img/master/1-1.png)

---
### image-set() 
> 可以根据用户设备的分辨率匹配合适的图像。

```
div {
	background-image: image-set( "test.png" 1x, "test-2x.png" 2x, "test-print.png" 600dpi );
}
//上述代码将会为普通屏幕使用 test.png，为高分屏使用 test-2x.png，如果更高的分辨率则使用 test-print.png，比如印刷。
```
### object-fit
> 解决图片变形问题
###### 属性:fill / contain / cover / none / scale-down / inherit / initial / unset
###### 默认值：fill;
1. fill: 中文释义“填充”。默认值。替换内容拉伸填满整个content box, 不保证保持原有的比例。
2. contain: 中文释义“包含”。保持原有尺寸比例。保证替换内容尺寸一定可以在容器里面放得下。因此，此参数可能会在容器内留下空白。
3. cover: 中文释义“覆盖”。保持原有尺寸比例。保证替换内容尺寸一定大于容器尺寸，宽度和高度至少有一个和容器一致。因此，此参数可能会让替换内容（如图片）部分区域不可见。
4. none: 中文释义“无”。保持原有尺寸比例。同时保持替换内容原始尺寸大小。
5. scale-down: 中文释义“降低”。就好像依次设置了none或contain, 最终呈现的是尺寸比较小的那个。
### object-position
> 控制图片的显示位置
###### 默认值：50% 50%;(居中)

```
//支持如下写法
object-position: 100% 100%;
object-position: right 20px bottom 10px;
object-position: calc(100% - 20px) calc(100% - 10px);
```
###### demo:
[object-position/object-fit img sprites与数字翻动demo](http://www.zhangxinxu.com/study/201503/css3-object-position-object-fit-img-sprites.html)











































