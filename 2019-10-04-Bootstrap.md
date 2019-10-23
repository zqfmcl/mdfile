---
title: Bootstrap
date: 2019-10-04 10:00:00
tags: Javascript
---

# 2016年1月3日

## bootstrap

### 网格系统

网格系统的实现原理非常简单，仅仅是通过定义容器大小，平分12份(也有平分成24份或32份，但12份是最常见的)，再调整内外边距，最后结合媒体查询，就制作出了强大的响应式网格系统。

```html 
<div class="col-md-8">//占据十二分之八的宽度，
<div class="col-md-4">

//媒体查询，当宽度大于等于992px的时候，该元素位置变化。向右移动8个网格。
//类名col-nd-pull是向左移动。
@media (min-width: 992px)
.col-md-push-8 {
    left: 66.66666667%;
}
```

**媒体查询**

```html 
/* 超小屏幕（手机，小于 768px） */
@media (max-width: @screen-xs-min) { ... }
/* 没有任何媒体查询相关的代码，因为这在 Bootstrap 中是默认的（还记得 Bootstrap 是移动设备优先的吗？） */
@media (max-width: 767px) {
    /*在小于768像素的屏幕里,这里的样式才生效*/
}


/* 小屏幕（平板，大于等于 768px） */
@media (min-width: @screen-sm-min) { ... }
@media (min-width: 768px) and (max-width: 991px) {
    /*在768和991像素之间的屏幕里,这里的样式才生效*/
}


/* 中等屏幕（桌面显示器，大于等于 992px） */
@media (min-width: @screen-md-min) { ... }
@media (min-width: 992px) and (max-width: 1199px) {
    /*在992和1199像素之间的屏幕里,这里的样式才生效*/
}


/* 大屏幕（大桌面显示器，大于等于 1200px） */
@media (min-width: @screen-lg-min) { ... }
@media (min-width: 1200px) {
    /*在大于1200像素的屏幕里,这里的样式才生效*/
}

```

**清除浮动**

`.clearfix`类名可以清除浮动。

**偏移空间**
`col-md-off-6`可以在一定尺寸（md--中等尺寸）上偏移一定距离。

**隐藏与显示**

`.visible-xs`在特定尺寸（xs--特小尺寸）下显示该元素。

### 下拉菜单

1、使用一个名为“dropdown”的容器包裹了整个下拉菜单元素，示例中为:

`<div class="dropdown"></div>`

2、使用了一个`<button`>按钮做为父菜单，并且定义类名** dropdown-toggle** 和自定义**data-toggle** 属性，且值必须和最外容器类名一致，此示例为:

`data-toggle="dropdown"`

3、下拉菜单项使用一个ul列表，并且定义一个类名为“dropdown-menu”，此示例为:

`<ul class="dropdown-menu">`

**效果如下**

![](C:/Users/Administrator/Desktop/My-study-records-master/2016/1/img/dropdown.jpg)

# 2016年1月4日

## bootstrap

### 导航栏

**基本框架**

```html 
<nav class="navbar navbar-inverse navbar-fixed-top">
            <div class="container">
                <a href="#"  class="navbar-brand"><strong>ninghao</strong>.net</a>
                <ul class="nav navbar-nav">
                    <li class="active"><a href="">课程</a></li>
                    <li><a href="">博客</a></li>
                    <li><a href="">手册</a></li>
                </ul>
                <form action="" class="navbar-form navbar-left">
                    <input type="text" placeholder="search" class="form-control">
                    <button type="submit">
                        <span class="glyphicon glyphicon-search"></span>
                    </button>
                </form>
                <a href="" class="btn btn-primary btn-sm navbar-btn navbar-right">订阅课程</a>
            <div class="profile navbar-right">
                <ul class="nav navbar-nav">
                    <li><a href="">登陆</a></li>
                    <li><a href="">注册</a></li>
                </ul>
                <p class="navbar-text">hello,你好<a href="#" class="navbar-link">niefee</a></p>
            </div>
            </div>          
        </nav>

<!-- 响应式收缩栏  -->
<button class="navbar-toggle" data-toggle="collapse" data-target="#responsive-navbar">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>

    <div class="collapse navbar-collapse" id="responsive-navbar"></div>
```

**.navbar-default**:默认的白色样式。
**.navbar-inverse**:黑色样式。
**.navbar-fixed-top**:固定在顶部。
**.navbar-static-top**:跟随页面滚动。
**.glyphicon .glyphicon-search**:两个一起使用，定义一个icon图标。
**.navbar-form .navbar-left**:添加一个类，浮动在左边。
**.navbar-text**:给导航栏中的文字添加样式。
**.navbar-link**:给导航栏中的链接添加样式。

为了确保适当的绘制和触屏缩放，需要在 `<head>` 之中**添加 viewport 元数据标签**

```
<meta name="viewport" content="width=device-width, initial-scale=1">。
```

### 按钮组件

**html** 里面的** role **本质上是增强语义性，增强组件的可访问性、可用性和可交互性。设置div 的 **role=“button”**，辅助工具就可以认出这实际上是个**button**。

> http://www.zhangxinxu.com/wordpress/2012/03/wai-aria-%E6%97%A0%E9%9A%9C%E7%A2%8D%E9%98%85%E8%AF%BB/

```html 
<!-- Standard button -->
<button type="button" class="btn btn-default">（默认样式）Default</button>

<!-- Provides extra visual weight and identifies the primary action in a set of buttons -->
<button type="button" class="btn btn-primary">（首选项）Primary</button>

<!-- Indicates a successful or positive action -->
<button type="button" class="btn btn-success">（成功）Success</button>

<!-- Contextual button for informational alert messages -->
<button type="button" class="btn btn-info">（一般信息）Info</button>

<!-- Indicates caution should be taken with this action -->
<button type="button" class="btn btn-warning">（警告）Warning</button>

<!-- Indicates a dangerous or potentially negative action -->
<button type="button" class="btn btn-danger">（危险）Danger</button>

<!-- Deemphasize a button by making it look like a link while maintaining button behavior -->
<button type="button" class="btn btn-link">（链接）Link</button>
```

**效果如下：：**

![](C:/Users/Administrator/Desktop/My-study-records-master/2016/1/img/btn-1.jpg)

### 下拉菜单

**一般框架代码**

```html 
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
   <!-- 通过类名添加一个标题 -->
    <li class="dropdown-header">Dropdown header</li>
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
   <!--  通过类名'.disabled'禁用菜单项 -->
    <li class="disabled"><a href="#">Separated link</a></li>
    <!-- 添加分割线 -->
    <li role="separator" class="divider"></li>
  </ul>
</div>
```

> 通过为下拉菜单的父元素设置** .dropup **类，可以让菜单向上弹出（默认是向下弹出的。
> 如需将菜单右对齐，请使用 **.dropdown-menu-right **类。

**aria-expanded**表示展开状态。默认为undefined, 表示当前展开状态未知。其它可选值：true表示元素是展开的；false表示元素不是展开的。

**aria-hidden**字符串。可选值为true和false,true表示元素隐藏(不可见)，false表示元素可见。

**aria-haspopup** :true表示点击的时候会出现菜单或是浮动元素； false表示没有pop-up效果。 

# 2016年1月5日

## bootstrap

### 按钮组

**基本框架**

```html 
<div class="btn-group" role="group" aria-label="...">
  <button type="button" class="btn btn-default">Left</button>
  <button type="button" class="btn btn-default">Middle</button>
  <button type="button" class="btn btn-default">Right</button>
</div>
```

**按钮工具栏**

把一组** < div class="btn-group">** 组合进一个** < div class="btn-toolbar"> **中就可以做成更复杂的组件。

```html 
<div class="btn-toolbar" role="toolbar" aria-label="...">
  <div class="btn-group" role="group" aria-label="...">...</div>
  <div class="btn-group" role="group" aria-label="...">...</div>
  <div class="btn-group" role="group" aria-label="...">...</div>
</div>
```

**效果如下：**

![](C:/Users/Administrator/Desktop/My-study-records-master/2016/1/img/btn-2.jpg)

**尺寸**

只要给** .btn-group **加上 ** .btn-group- **类，就省去为按钮组中的每个按钮都赋予尺寸类了，如果包含了多个按钮组时也适用。

```html 
<div class="btn-group btn-group-lg" role="group" aria-label="...">...</div>
<div class="btn-group" role="group" aria-label="...">...</div>
<div class="btn-group btn-group-sm" role="group" aria-label="...">...</div>
<div class="btn-group btn-group-xs" role="group" aria-label="...">...</div>

```

**嵌套**

想要把下拉菜单混合到一系列按钮中，只须把** .btn-group** 放入另一个** .btn-group **中。

```html 
<div class="btn-group" role="group" aria-label="...">
  <button type="button" class="btn btn-default">1</button>
  <button type="button" class="btn btn-default">2</button>

  <div class="btn-group" role="group">
    <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
      Dropdown
      <span class="caret"></span>
    </button>
    <ul class="dropdown-menu">
      <li><a href="#">Dropdown link</a></li>
      <li><a href="#">Dropdown link</a></li>
    </ul>
  </div>
</div>
```

**垂直排列**

```html 
<div class="btn-group-vertical" role="group" aria-label="...">
  ...
</div>

```

**两端对齐排列的按钮组**

只须将一系列** .btn ** 元素包裹到** .btn-group.btn-group-justified** 中即可。

```
<div class="btn-group btn-group-justified" role="group" aria-label="...">
...
</div>
```

### 下拉菜单

**单按钮下拉菜单**

只要改变一些基本的标记，就能把按钮变成下拉菜单的开关。

```html 
<div class="btn-group">
  <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    Action <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

**分裂式按钮下拉菜单**

相似地，分裂式按钮下拉菜单也需要同样的改变一些标记，但只是多一个分开的按钮。

```html 
<!-- Split button -->
<div class="btn-group">
  <button type="button" class="btn btn-danger">Action</button>
  <button type="button" class="btn btn-danger dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    <span class="caret"></span>
    <span class="sr-only">Toggle Dropdown</span>
  </button>
  <ul class="dropdown-menu">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

**向上弹出式菜单**

给父元素添加** .dropup** 类就能使触发的下拉菜单朝上方打开。

### 表单

单独的表单控件会被自动赋予一些全局样式。所有设置了 .form-control 类的 ** < input>**、** < textarea>** 和**   < select>** 元素都将被默认设置宽度属性为 `width: 100%;`。 将 label 元素和前面提到的控件包裹在** .form-group **中可以获得最好的排列

```html 
<form>
  <div class="form-group">
    <label for="exampleInputEmail1">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email">
  </div>
</form>
```

**内联表单**

为** < form> **元素添加** .form-inline** 类可使其内容左对齐并且表现为** inline-block** 级别的控件。只适用于视口（viewport）至少在 768px 宽度时（视口宽度再小的话就会使表单折叠）。

```html 
<form class="form-inline">
  <div class="form-group">
    <label for="exampleInputName2">Name</label>
    <input type="text" class="form-control" id="exampleInputName2" placeholder="Jane Doe">
  </div>
  <div class="form-group">
    <label for="exampleInputEmail2">Email</label>
    <input type="email" class="form-control" id="exampleInputEmail2" placeholder="jane.doe@example.com">
  </div>
  <button type="submit" class="btn btn-default">Send invitation</button>
</form>
```

**效果如下：**

![](C:/Users/Administrator/Desktop/My-study-records-master/2016/1/img/form.jpg)

**水平排列的表单**

通过为表单添加** .form-horizontal** 类，并联合使用 Bootstrap 预置的栅格类，可以将 label 标签和控件组水平并排布局。这样做将改变 .**form-group **的行为，使其表现为栅格系统中的行**（row）**，因此就无需再额外添加 **.row **了。

```html 
<form class="form-horizontal">
  <div class="form-group">
    <label for="inputEmail3" class="col-sm-2 control-label">Email</label>
    <div class="col-sm-10">
      <input type="email" class="form-control" id="inputEmail3" placeholder="Email">
    </div>
  </div>
    </form>

```

# 2016年1月7日

## bootstrap

### 媒体查询

```html
<!-- 外脸样式 -->
<link href="" rel="stylesheet" media="only screen and (max-width:480px)">
<!-- 内联样式  -->
<style type="text/css">
    @media screen and (min-width: 480px){
        body{
            background: blue;
        }
    }
    </style>

```

# 2016年1月18日

## javascript

### fullPage.js配置

**官网：**

1. http://alvarotrigo.com/fullPage/
2. https://github.com/alvarotrigo/fullPage.js

> 参考：http://www.dowebok.com/77.html

- sectionsColor :

可以为每一个**section**设置**background-color**属性。

- controlArrows

定义是否通过箭头来控制slide幻灯片，默认为**true**。当我们设置为 **false** ，幻灯片左右两侧的箭头就会消失， 在移动设备上我们可以通过滑动来操作幻灯片。

- verticalCentered

每一页的内容是否垂直居中，默认为**true**。一般我们保持默认值。

- resize

字体是否随着窗口缩放而缩放，默认为**false**。

- scrollingSpeed:

滚动时间，默认**700ms**。

- anchors

定义锚链接，默认值为[]。有了锚链接，用户就可以快速打开定位到某一页面。
注意定义锚链接的时候，值不要和页面中任意的**id**或者**name**相同，尤其是在IE浏览器下。而且定义时不需要加**#**。

> 在section中添加**active**可以默认打开此页。

- lockAnchors:

是否锁定锚链接，默认为**false**。如果设置为**true**，那么定义的锚链接，也就是**anchors**属性则没有效果。这个配置项**使用得比较少**。

- easing:

定义页面section滚动的动画方式，默认是**easeInOutCubic**，如果修改此项，需要引入**jQuery.easings**插件，或者**jquery ui**。

- css3：

是否使用**CSS3 transforms**来实现滚动效果，默认为**true**。这个配置项可以提高支持css3的浏览器，比如移动设备等的速度，如果浏览器不支持测css3，,则会使用jquery来代替css3实现滚动效果。

- loopTop:

滚动到最顶部后是否连续滚动到底部， 默认为**false**。

- loopBottom:

滚动到最底部后是否连续滚动回顶部，默认为**false**。

- loopHorizontal:

横向slider幻灯片是否循环滚动，默认为**true**。 

- autoScrolling:

是否使用插件的滚动方式，默认为**true**，如果使用**false**，则会出现浏览器自带的滚动条，将不会按页滚动，而是按照滚动条的默认行为来滚动。

- scrollBar:

是否包含 滚动条，默认为**false**，如果设置为**true**，则浏览器自带的滚动条出现，页面滚动时还是按页滚动，但滚动条是默认行为也有效。

- paddingTop/paddingBottom:

设置每一个**section**顶部和底部的**padding**，默认都为0。一般如果我们需要设置一个固定在顶部或者底部的菜单、导航、元素等，可以使用这两个配置项。

- fixedElements:

固定的元素，默认为**null**，需要配置一个jquery选择器。在页面滚动的时候，**fixedElements**设置的元素固定不动。 

- keyboardScrolling:

是否可以使用键盘方向键导航，默认为**true**。 

- touchSensitivity

在移动设备中滑动页面的敏感度，默认为5，是按百分比来衡量，最高为100，越大则越难滑动。 

- continuousVertical:

是否循环滚动，默认为**false**。如果设置为**true**，则页面会循环滚动，而不像loopTop或者loopBottom那样出项跳动，注意这个属性和loopTop、loopBottom不兼容，不能同时设置。

- animateAnchor：

锚链接是否可以控制滚动动画，默认为**true**。如果设置为**false**，则通过 锚链接定位到某页面显示不再有动画效果。

- recordHistory：

是否记录历史，默认为**true**，可以记录页面滚动的历史，通过浏览器的前进后退来导航。如果设置了**autoScrolling：false**，那么这个配置也将被关闭，即设置为**false **。

- menu：

绑定菜单，设定的相关属性与**anchors**的值对应后，菜单可以控制滚动，默认为**false**。可以设置为菜单的jquery选择器。

```js 
<ul id="myMenu">
    <li data-menuanchor="firstPage" class="active"><a href="#firstPage">First section</a></li>
    <li data-menuanchor="secondPage"><a href="#secondPage">Second section</a></li>
    <li data-menuanchor="thirdPage"><a href="#thirdPage">Third section</a></li>
    <li data-menuanchor="fourthPage"><a href="#fourthPage">Fourth section</a></li>
</ul>


$('#fullpage').fullpage({
    anchors: ['firstPage', 'secondPage', 'thirdPage', 'fourthPage', 'lastPage'],
    menu: '#myMenu'
});
```

- navigation:

是否显示导航，默认为**false**。如果设置为**true**，会显示小圆点，作为导航。

- navigationPosition：

导航小圆点的位置，可以设置为**left**或者**right**。 

- navigationTooltips：

导航小圆点的tooltips设置，默认为[],注意按照顺序设置。 

- showActiveTooltip:

是否显示当前页面的导航的tooltip的信息，默认为**false**。 

- slidesNavigation：

是否显示横向幻灯片的导航，默认为**false**。 

- slidesNavPosition

横向幻灯片导航的位置，默认为**bottom**，可以设置为**top**或**bottom**。  

- scrollOverflow:

内容超过满屏后是否显示滚动条，默认为**false**。如果设置为**true**，则会显示滚动条，如果要滚动查看内容，还需要**jquery.slimscroll**插件的配合。slimscroll插件主要用于模拟传统浏览器滚动条。

- sectionSelector：

section的选择器，默认为**.section**。 

- slideSelector:

slide的选择器，默认为**.slide**。

------

### fullpage.js方法

使用方式：

```
$.fn.fullpage.xxx()
```

- moveSectionUp():

向上滚动一页。

- moveSectionDown():

向下滚动一页

- moveTo(section,slide):

滚动到第几页，第几个幻灯片，注意，页面是从**1**开始，而幻灯片从**0**开始。 

- silentMoveTo(section,slide):

滚动到第几页，和moveTo一样，但是没有动画效果。

- moveSlideRight()

幻灯片向右滚动。

- moveSlideLeft():

幻灯片向左滚动。

- setAutoScrolling(boolean):动态设置**autoScrolling**
- setLockAnchors(boolean):动态设置**lockAnchors**
- setRecordHistory(boolean):动态设置**recordHistory**
- setScrollingSpeed(milliseconds):动态设置**scrollingSpeed**

- setAllowScrolling(boolean,[directions]):

添加或删除鼠标滚轮/滑动控制，第一个参数**true**为启用，**false**为禁用，后面的参数为方向，取值包含**all**、**up**、**down**、**left**、**right**,可以使用多个，逗号分隔。

- destroy(type)

销毁**fullpage**特效，**type**可以不写，或者使用**all**，不写**type**， 
**fullpage**给页面添加的样式和**HTML**元素还在，如果使用**all**，则样式、**HTML**等全部销毁，页面恢复和不使用**fullpage**相同的效果。

- reBuild()

重新更新页面和尺寸，用于通过**Ajax**请求后改变页面结构之后，重建效果。

------

**延迟加载**

如图片标签，**src**地址变成**data-src**，可以达到延迟效果。**video**也可以。

------

### 回调函数

- afterLoad（anchorLink，index）

滚动到某一section处，且滚动结束后，会触发一次此回调函数，函数接收anchorLink和index 两个参数，anchorLink是锚链接，index是序号（从1开始）。
作用：我们可以根据anchorLink和index的参数值的判断，触发相应的事件。

```js 
afterLode：function（anchorLink，index）{
console.log（"afterLode:anchorLink"+anchorLink+";index:"+index）;//将两个参数打印出来，在控制台可以看到
}
```

- onLeave（index，nextIndex，direction）

在离开一个页面时，会触发一次此回调函数，接收**index**（离开时页面的序号，from 1）、**nextIndex**（滚动到的目标页面的序号, from 1）和**direction**（滚动的方向，有**up**和**down**）3个参数

通过**return false**；可以取消滚动

- afterRender（）

页面初始化完成后的回调函数。

- afterResize（）

浏览器窗口尺寸改变后的回调函数。

- afterSlideLode（anchorLink，index，slideAnchor，slideIndex）

滚动到某一**slide**后的回调函数，与**afterLode**类似，接收 **anchorLink**、**index** 、**slideIndex** 、 **direction**4个参数

- onSlideLeave（anchorLink，index，slideIndex，direction，nextSlideIndex）

在离开一个**slide**时会触发此函数，与**onLeave**相似，接收 **anchorLink** 、**index** 、**slideIndex** 、**direction** 4个参数



------

### move.js方法

**move.js**是一个js库，支持css3。

- set(css属性，属性值)
- scale（缩放的倍数）
- rotate（旋转的角度数）；可正可负
- end（）；用于结束move.

js代码片段的结束，标识动画的结束。此方法可接受一个回调函数

给页面添加动画效果可利用回调函数（另外：要实现某一东西从某一方向飞入，则首先给其设置一个较大的**margin**，并设置**overflow：hidden**，使此东西在页面中显示不出来，然后通过回调函数应用**move.js**的 **set（‘margin-方向’，‘使此东西在正确位置的margin值’））**

![]()

# 2016年1月25日

## css

**系统自带中文字体编码：**

- 宋体 **SimSun**
- 黑体 **SimHei**
- 微软雅黑 **Microsoft YaHei**
- 微软正黑 **体Microsoft JhengHei**
- 新宋体 **NSimSun**
- 新细明体 **PMingLiU**
- 细明体 **MingLiU**
- 标楷体 **DFKai-SB**
- 仿宋 **FangSong**
- 楷体 **KaiTi**
- 仿宋 **_GB2312FangSong_GB2312**
- 楷体 **_GB2312KaiTi_GB2312**

# 2016年1月28日

## javascript

**[object Object]**

表示这个对象是一个对象集合。

```javascript
var a = new Object();

a.abc = new Object();

a.abc.a123 = new Object();

这就是[object Object] 

补充：简单的写法：
var a = {
    abc : {
        a123 : {}
    }
};
表示对象的类型是object，这个对象的constructor是Object
```

**toString 方法**返回 **[object objectname]**，其中 **objectname** 是对象类型的名称。

**@font-face**

```javascript
    <!-- 定义字体 -->
   @font-face {
    font-family: 'YourWebFontName';
    src: url('YourWebFontName.eot'); /* IE9 Compat Modes */
    src: url('YourWebFontName.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
             url('YourWebFontName.woff') format('woff'), /* Modern Browsers */
             url('YourWebFontName.ttf')  format('truetype'), /* Safari, Android, iOS */
             url('YourWebFontName.svg#YourWebFontName') format('svg'); /* Legacy iOS */
   }
    <!-- 对内容使用定义的字体。  -->
    h2.neuesDemo {
      font-family: 'NeuesBauenDemo'
   }
```

**HTTP**

HTTP(Hyper Text Transfer Protocol，超文本传输协议)是一种通信协议 ，它允许将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器。

**URI(Uniform Resource Identifier)**，翻译为统一资源标识符，是一个用于标识某
一互联网资源名称的字符串。

**URL(Uniform Resource Location)**，翻译为统一资源定位符，它描述一台特定服
务器上某特定资源的特定位置。

格式：

`http://user:pass@www.example.com:80/home/index.html?age=11#mask`
**http**：协议方案名
**user:pass**：登录信息（认证）
**www.example.com**：服务器地址
**80**：端口号
**/hone/index.html**：文件路径
**age=11**：查询字符串
**mask**：片段标识符

# 2016年1月29日

## json

json的四个基本原则

1. 并列数据之间用逗号（“ , ”半角）分隔
2. 映射用冒号（“ : ”）表示
3. 并列数据的集合（数组，列表）用方括号（“ [] ”）表示
4. 映射的集合（对象）用大括号(“ {} ”)表示

![](C:/Users/Administrator/Desktop/My-study-records-master/2016/1/img/json.jpg)

> json字符集必须是**Unicode**。

JavaScript 程序能够使用内建的 **eval()** 函数，用 JSON 数据来生成原生的 JavaScript 对象。

**eval()**函数接收一个参数s，如果s不是字符串，则直接返回s。否则执行s语句。如果s语句执行结果是一个值，则返回此值，否则返回**undefined**。

如果参数中没有合法的表达式和语句，则抛出** SyntaxError** 异常。
如果非法调用** val()**，则抛出 **EvalError**异常。
如果传递给**eval()** 的** Javascript** 代码生成了一个异常，**eval() **将把该异常传递给调用者。

**JSON.parse()**

```js
语法：
JSON.parse(text [, reviver])

例子：
var jsontext = '{"firstname":"Jesper","surname":"Aaberg","phone":["555-0100","555-0120"]}';
var contact = JSON.parse(jsontext);
document.write(contact.surname + ", " + contact.firstname);
```

**JSON.stringify() **

JSON.stringify()方法可以将任意的 JavaScript 值序列化成 JSON 字符串。

```json
var foo = {};
foo.bar = "new property";
foo.baz = 3;

var jsonString = JSON.stringify(foo);
```

**Ajax**

创建XMLHttpRequest对象

```js
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
```

**Try{}catch(e){}**

```js
基本语法：

　try {
　　// 此处是可能产生例外的语句
　　} catch(error) {
　　// 此处是负责例外处理的语句
　　} finally {
　　// 此处是出口语句
　　}
```

```js
　　try {
　　　　document.writeln("开始执行try块语句 ---> ")
　　　　document.writeln("还没有发生例外 ---> ")
　　 　　alert((prompt("输入一个值：","")))
　　 } catch(err) {
　　 　　document.writeln("捕捉到例外，开始执行catch块语句 --->");
　　 　　document.writeln("错误名称: " + err.name+" ---> ");
　　 　　document.writeln("错误信息: " + err.message+" ---> ");
　　} finally {
　　 　　document.writeln("开始执行finally块语句")
　　}
```

“开始执行try块语句 ---> 还没有发生例外 ---> 捕捉到例外，开始执行catch块语句 ---> 错误名称: TypeError ---> 错误信息: 'abc' 未定义 ---> 开始执行finally块语句”

**Error.name**的取值一共有六种:

1. Error：()的使用与定义不一致
2. RangeError：数值越界
3. ReferenceError：非法或不能识别的引用数值
4. SyntaxError：发生语法解析错误
5. TypeError：操作数类型错误
6. URIError：URI处理函数使用不当

**Throw 语句**

`throw 语句`允许我们创建自定义错误。
正确的技术术语是：创建或抛出异常（exception）。

```js
function myFunction()
{
try
  {
  var x=document.getElementById("demo").value;
  if(x=="")    throw "empty";
  if(isNaN(x)) throw "not a number";
  if(x>10)     throw "too high";
  if(x<5)      throw "too low";
  }
catch(err)
  {
  var y=document.getElementById("mess");
  y.innerHTML="Error: " + err + ".";
  }
}
</script>

<h1>My First JavaScript</h1>
<p>Please input a number between 5 and 10:</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">Test Input</button>
<p id="mess"></p>
```

# 2016年1月30日

## Ajax

创建** XMLHttpRequest** 对象:

```js 
var xmlhttp;
if (window.XMLHttpRequest)
    {// code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp=new XMLHttpRequest();
    }
else
    {// code for IE6, IE5
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
    }

或者：

xmlhttp=new XMLHttpRequest()||ActiveXObject("Microsoft.XMLHTTP");
```

**GET**请求：

```js 
function ajax(){
        var xml=new XMLHttpRequest()||ActiveXObject("Microsoft.XMLHTTP");
        xml.onreadystatechange=function(){
            if  (xml.readyState==4&&xml.status==200){
            document.getElementById("myDiv").innerHTML=xml.responseText;
        }
    }
        xml.open("get","/ajax_info.txt?t="+ Math.random(),true);
        xml.send();
}
```

**post请求**
如果需要像 HTML 表单那样 POST 数据，请使用 **setRequestHeader()** 来添加 HTTP 头。然后在 **send()** 方法中规定您希望发送的数据：

```js 
xmlhttp.open("POST","ajax_test.html",true);

xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");

xmlhttp.send("fname=Henry&lname=Ford");
```

**GET**与**POST**的区别

- 无法使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

**Async = false**

不推荐使用**async=false**，但是对于一些小型的请求，也是可以的。JavaScript 会等到服务器响应就绪才继续执行。如果服务器繁忙或缓慢，应用程序会挂起或停止。

使用**async=false** 时，请不要编写 **onreadystatechange** 函数 - 把代码放到 **send()** 语句后面即可。

**responseXML 属性**

```js 
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
  {
  txt=txt + x[i].childNodes[0].nodeValue + "<br>";
  }
document.getElementById("myDiv").innerHTML=txt;
```

**回调函数**

回调函数是一种以参数形式传递给另一个函数的函数。
如果您的网站上存在多个 AJAX 任务，那么您应该为创建** XMLHttpRequest **对象编写一个标准的函数，并为每个 AJAX 任务调用该函数。
该函数调用应该包含 **URL** 以及发生 **onreadystatechange** 事件时执行的任务（每次调用可能不尽相同）：

```js 
var xmlhttp;
function loadXMLDoc(url,cfunc)
{
if (window.XMLHttpRequest)
  {// IE7+, Firefox, Chrome, Opera, Safari 代码
  xmlhttp=new XMLHttpRequest();
  }
else
  {// IE6, IE5 代码
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
xmlhttp.onreadystatechange=myFunction();
xmlhttp.open("GET",url,true);
xmlhttp.send();
}
function myFunction()
{
loadXMLDoc("ajax_info.txt",function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  });
}
```

**readyState**表示**XMLHttpRequest**对象的处理状态：

- 0:XMLHttpRequest对象还没有完成初始化。(准备司机、车、货物)
- 1:XMLHttpRequest对象开始发送请求。(需要送十车货物，当前正在送第几车)
- 2:XMLHttpRequest对象的请求发送完成。(十车货送完毕)
- 3:XMLHttpRequest对象开始读取服务器的响应。(准备把这十车加工的货拉回来，当前第几车)
- 4:XMLHttpRequest对象读取服务器响应结束。(十车货全部拉回完毕)

**status状态：**

- 1xx:信息响应类，表示接收到请求并且继续处理。(所有拉去的货，工厂还没有加工完毕)  
- 2xx:处理成功响应类，表示动作被成功接收、理解和接受。。(所有拉去的货工厂全部加工完毕)  
- 3xx:重定向响应类，为了完成指定的动作，必须接受进一步处理 。(所有拉去的货，工厂设备不够，让其他工厂帮忙加工)  
- 4xx:客户端错误，客户请求包含语法错误或者是不能正确执行 。(这十车货有质量问题，工厂不能正常加工)
- 5xx:服务端错误，服务器不能正确执行一个正确的请求。(工厂在加工到一半过程中断电，不能继续加工)

**json**

```js 
var jsondata='{staff:[{"name":"洪七","age":"70"},{"name":"郭靖","age":"35"},{"name":"黄蓉","age":"30"}]}';

//容易解释执行语句，不考虑字符串是否合法。
var jsonobj=eval('('+jsondata+')');
alert(jsonobj.staff[0].name);

//推荐使用
var jsonobj_2=JSON.parse(jsondata);

```



