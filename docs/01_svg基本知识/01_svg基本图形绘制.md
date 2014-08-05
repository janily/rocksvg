svg提供了一些常见的形状，可以直接使用它们来绘制图形。

svg提供来诸如：矩形、带圆角的矩形、圆形、椭圆形、直线、多边形以及路径等基本图形元素。

下面就每一个图形等使用结合实例来说明基本属性等使用。

#### 矩形－rect元素

矩形元素有6个控制位置和形状等属性，分别是：

* x：矩形左上角的坐标(用户坐标系)的x值
* y：矩形左上角的坐标(用户坐标系)的y值
* width：矩形宽度
* height：矩形高度
* rx：实现圆角效果时，圆角沿x轴的半径
* ry：实现圆角效果时，圆角沿y轴的半径

下面是一个关于矩形等实例：

<a class="jsbin-embed" href="http://jsbin.com/pudakoxa/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

你可以看到在这个例子中，通过设置rx,ry实现来圆角等效果。

#### 圆－circle元素和椭圆－ellipse元素

circle元素主要有以下三个参数：

* r：半径
* cx：圆心坐标x值
* cy：圆心坐标y值

ellipse元素有4个参数，你可以通过控制长半轴和短半轴等长度，来实现不同等椭圆，当两个半轴相等时，就是一个正圆啦。

* rx：长半轴(x半径)
* ry：短半轴(y半径)
* cx：圆心坐标x值
* cy：圆心坐标y值

下面是一个关于圆和椭圆的实例：

<a class="jsbin-embed" href="http://jsbin.com/huxojezu/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

#### 直线－line和折线－polyline

直线只需要定义起点和终点即可：

* x1：起点x坐标。
* y1：起点y坐标。
* x2：终点x坐标。
* y2：终点y坐标。

折线主要是定义每条线段的端点即可，所以只需要一个点的集合作为参数：

points：一系列的用空格，逗号，换行符等分隔开的点。每个点必须有2个数字：x值和y值。所以下面3个点 (0,0), (1,1)和(2,2)可以写成："0 0, 1 1, 2 2"。

下面来看一个关于折线和直线的实例：

<a class="jsbin-embed" href="http://jsbin.com/wiwesavo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

下面是path元素，我认为它是svg最牛逼，最强大的元素。有来它我们就可以制作出令css3望尘莫及的动画效果。所以这个要单独列出来讲讲。






