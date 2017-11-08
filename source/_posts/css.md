---
title: css鲜为人知的属性1
date: {{date}}
categories: 前端
tags: 前端
---
# pointer-events
##### 属性：auto | none | visiblepainted | visiblefill | visiblestroke | visible | painted | fill | stroke | all

#####  默认值：auto

#####  取值：
1. auto：与pointer-events属性未指定时的表现效果相同。在svg内容上与visiblepainted值相同
2. none：元素永远不会成为鼠标事件的target。但是，当其后代元素的pointer-events属性指定其他值时，鼠标事件可以指向后代元素，在这种情况下，鼠标事件将在捕获或冒泡阶触发父元素的事件侦听器。
3. ++其他值只能应用在SVG上。++

##### 说明：设置或检索在何时成为属性事件的target。
使用pointer-events来阻止元素成为鼠标事件目标不一定意味着元素上的事件侦听器永不会触发。如果元素后代明确指定了pointer-events属性并允许其成为鼠标事件的目标，那么指向该元素的任何事件在事件传播过程中都将通过父元素，并以适当的方式触发其上的事件侦听器。当然位于屏幕上在父元素上但不在后代元素上的鼠标活动都不会被父元素和后代元素捕获（将会穿过父元素而指向位于其下面的元素）。

对应的脚本特性为pointerEvents。

---
# attr

```
[data-unit]:after{
    content:attr(data-unit);
    color:red;
}
```
```
<p data-unit="元">余额3</p>
```

![效果](https://raw.githubusercontent.com/zhangtingqian/img/master/yu.png)

---
# currentColor 
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
# user-select
> 禁止选择文本

---
# ::selection
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

![默认效果](https://raw.githubusercontent.com/zhangtingqian/img/master/1.png)![选中效果](https://raw.githubusercontent.com/zhangtingqian/img/master/1-1.png)

---
# image-set() 
> 可以根据用户设备的分辨率匹配合适的图像。

```
div {
	background-image: image-set( "test.png" 1x, "test-2x.png" 2x, "test-print.png" 600dpi );
}
//上述代码将会为普通屏幕使用 test.png，为高分屏使用 test-2x.png，如果更高的分辨率则使用 test-print.png，比如印刷。
```

---

# object-fit
> 解决图片变形问题
##### 属性:fill / contain / cover / none / scale-down / inherit / initial / unset
##### 默认值：fill;
1. fill: 中文释义“填充”。默认值。替换内容拉伸填满整个content box, 不保证保持原有的比例。
2. contain: 中文释义“包含”。保持原有尺寸比例。保证替换内容尺寸一定可以在容器里面放得下。因此，此参数可能会在容器内留下空白。
3. cover: 中文释义“覆盖”。保持原有尺寸比例。保证替换内容尺寸一定大于容器尺寸，宽度和高度至少有一个和容器一致。因此，此参数可能会让替换内容（如图片）部分区域不可见。
4. none: 中文释义“无”。保持原有尺寸比例。同时保持替换内容原始尺寸大小。
5. scale-down: 中文释义“降低”。就好像依次设置了none或contain, 最终呈现的是尺寸比较小的那个。

---

# object-position
> 控制图片的显示位置
##### 默认值：50% 50%;(居中)

```
//支持如下写法
object-position: 100% 100%;
object-position: right 20px bottom 10px;
object-position: calc(100% - 20px) calc(100% - 10px);
```

[object-position/object-fit img sprites与数字翻动demo](http://www.zhangxinxu.com/study/201503/css3-object-position-object-fit-img-sprites.html)

---
# contain 
> 性能优化新属性
##### 属性：none | strict | layout | style | paint | size | contain
##### 属性值的解释：
- none 无
- layout 开启布局限制
- style 开启样式限制
- paint 开启渲染限制
- size 开启size限制
- content 开启除了size外的所有限制
- strict开启 layout, style 和 paint 三种限制组合
##### 使用场景：以将一个元素标志为和页面上其它元素是相对独立的元素；
#####  栗子：
###### a.页面小饰件(widgets)
通常在页面上添加第三方小饰件时，我们几乎对它们没有什么太多的控制，比如分享工具，它们可能会因为具有相当耗资源的布局、样式、渲染操作等大幅度的降低整个页面的执行效率。为了将它们同我们的网站隔离开来，使用 contain: strict; 将第三方的小饰件同页面上的其它内容隔离开来。
###### b.屏幕外的内容
如果你有一个导航栏或其它类似的东西并不在屏幕可现实范围内出现，浏览器同样会为这些不可见的元素进行渲染。通过使用 contain: paint; 浏览器就会忽略渲染这些屏幕外不可见的元素，从而能更快的渲染其它内容。
###### c.计算容器尺寸
我在文字开头提到过这个问题，使用 contain: strict; 可以 免去很多关于容器尺寸控制的问题。比如，子元素的内容会影响容器的大小，使用 contain 属性就可以避免这样的问题产生。

###### *为什么浏览器不能自动的实现 contain 的功能*
浏览器已经尽可能的在页面下做了最大的优化，但每个浏览器引擎的实现方法并不尽相同。而 contain 属性可以提供一种标准的方式让开发人员告诉 浏览器 某些方面可以这样优化，哪些不能优化。
###### *什么时候应该使用contain*
如果你的页面很简单，没有复杂的DOM节点和小饰件(widgets)，那就没必要考虑使用这种CSS的contain技术。而如果你开发的页面非常复杂，那么，这个CSS的contain技术可以帮助你优化页面的性能。而对于第三方的小饰件，始终使用contain: strict;是很好的习惯，它可以保护你的页面不受它们的干扰而出现性能问题。

---
# text-transform
> 控制文本中的字母
##### 属性：none | capitalize（每个单词以大写字母开头） | uppercase(仅有大写字母) | lowercase（仅有小写字母） | inherit 

---
# direction 
> 定文本书写方向(个人理解和text-align:left/right;差不多)
##### 属性：ltr(靠左) | rtl(靠右) | inherit

---
# position:sticky；
> 表现类似position:relative和position:fixed的合体，在目标区域在屏幕中可见时，它的行为就像position:relative;而当页面滚动超出目标区域时，它的表现就像position:fixed，它会固定在目标位置。**有兼容性**。
##### 自己js实现：

```
    .box{
        width: 100%;
        height: 100px;
        background: pink;
        text-align: center;
        //position:sticky; top: 0; 不写js加这个也可实现
    }
    .sticky{
        position: fixed;
        top: 0;
    }
    .bottom{
        height: 2000px;
    }
```


```
<p style="margin-bottom: 100px"></p>
<div class="box">测试盒子</div>
<div class="bottom"></div>
```


```
<script>
    var box=document.querySelector('.box');
    var offsetY=box.offsetTop;
    console.log(offsetY)
    document.addEventListener('scroll',function () {
        window.scrollY>offsetY?box.classList.add('sticky'):box.classList.remove('sticky');
    })
</script>
```

---
### 多列属性

属性 | 描述
---|---
column-count | 规定元素应该被分隔的列数。
column-fill | 规定如何填充列。
column-gap | 规定列之间的间隔。
column-rule | 设置所有 column-rule-* 属性的简写属性。
column-rule-color | 规定列之间规则的颜色。
column-rule-style | 规定列之间规则的样式。
column-rule-width | 规定列之间规则的宽度。
column-span | 规定元素应该横跨的列数。
column-width | 规定列的宽度。
columns | 规定设置 column-width 和 column-count 的简写属性。


====
















































