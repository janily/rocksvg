上篇文章我们说到了fill这个属性，这篇来说说stroke属性。这个属性是用来定义形状和paths边框用当。先来看看下面这个实例：

<a class="jsbin-embed" href="http://jsbin.com/jayoreya/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

stroke设置的是对象的边框颜色，你可以使用在HTML中设置CSS颜色的方式定义它们的颜色，比如颜色名（red），rgb值，hex值，rgba值。

### stroke-width

**stroke-width**是用来设置边框当宽度的，比如我们上面的例子边框的宽度是6px。

边框是围绕路径绘制的。stroke-width属性定义了边框的粗细，路径的每一侧都有均匀分布的边框。

### stroke－linecap

**stroke－linecap**属性，它控制边框终点的形状。stroke-linecap属性的值有三种，butt表示用直边结束边框，square的效果差不多，但是会稍微超出path的范围，超出的大小是stroke-width控制的。round表示边框的终点是圆角，圆角的半径也是stroke-width控制的。

如下图所示：

![image](http://jonibologna.com/content/images/2014/Jun/Screen-Shot-2014-06-29-at-3-24-33-PM.png)

我们稍微修改下上面的例子，把葡萄的根设置为square，如下说是：

<a class="jsbin-embed" href="http://jsbin.com/kahuhumo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

### stroke-linejoin

**stroke-linejoin**属性，用来控制两条边框线段之间，用什么方式连接。

![image](http://jonibologna.com/content/images/2014/Jun/Screen-Shot-2014-06-29-at-5-23-14-PM.png)

折线是由两个线段连接起来的，连接处的样式由stroke-linejoin属性控制，它有三个可用的值，miter是默认值，表示用方形画笔在连接处形成直角，round表示用圆角连接，实现平滑效果。最后还有一个值bevel，连接处会形成一个斜线。

还是上一个例子，我们把**linejoin**的值由**round**改为**bevel**：

<a class="jsbin-embed" href="http://jsbin.com/sakuzazu/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

### stroke-miterlimit

当我们定义stroke－linejoin的值为miter的时候，stroke－miterlimit这个属性可以允许我们来定义描边相交（锐角）的表现方式。

1.0是允许的最小的值。

下面还是看实际的例子来感受下，第一张图设置为**stroke－miterlimit="1.0"**，形成的效果跟设置linejoin的值为bevel的效果差不多。第二张图设置为**stroke－miterlimit="4.0"**，效果图下图所示：

<a class="jsbin-embed" href="http://jsbin.com/wesugibe/1/embed">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

### stroke-dasharray

**stroke－dasharray**属性用来定义将边框定义成虚线。

<a class="jsbin-embed" href="http://jsbin.com/tiqijope/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

stroke-dasharray属性的参数，是一组用逗号分割的数字组成的序列。需要注意的是，这里的数字必须用逗号分割，虽然也可以插入空格，但是数字之间必须用逗号分开。每一组数字，第一个用来表示实线，第二个用来表示空白。所以在上面的例子里，第二个路径会先画5px实线，紧接着是5px空白，然后又是5px实线，从而形成虚线。如果你想要更复杂的虚线模式，你可以定义更多的数字。上面例子里的第一个，就定义了3个数字，这种情况下，数字会循环两次，形成一个偶数的虚线模式。所以该路径首先是5px实线，然后是10px空白，然后是5px实线，接下来循环这组数字，形成5px空白、10px实线、5px空白。然后这种模式会继续循环。

通过下面的例子来感受下：

<a class="jsbin-embed" href="http://jsbin.com/nurotiwo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

### stroke-dashoffset

**stroke-dashoffset**表示虚线的起始偏移。可选值为：<percentage>, <length>, inherit. 百分比值，长度值，继承。

在上面的例子中，我们设置来虚线的长度为40px，以及虚线的开始位置是35px。所以，我们可以发现第一条虚线非常短，因为设置来stroke－dashoffset的值为35px。

### stroke-opacity

**stroke－opacity**表示描边透明度。默认是1。

### stroke与动画

stroke能够设置动画效果，得需要**stroke－dashoffset**和**stroke－dasharray**这两个属性来达成。

我们现在都试想一下，如果stroke-dasharray和stroke-dashoffset值都很大，超过了描边路径的总长度，会怎么样？
用中文解释就是，一根火腿肠12厘米，要在上面画虚线，虚线间隔有15厘米，如果没有dashoffset，则火腿肠前面15厘米会被辣椒酱覆盖！实际上只有12厘米，因此，我们看到的是整个火腿肠都有辣椒酱。现在，dashoffset也是15厘米，也就是虚线要往后偏移15厘米，结果，辣椒酱要抹在火腿肠之外，也就是火腿肠上什么辣椒酱也没有。如果换成上面的直线SVG，也就是直线看不见了。我们把dashoffset值逐渐变小，则会发现，火腿肠上的辣椒酱一点一点出现了，好像辣椒酱从火腿肠根部涂抹上去一样。

这就是SVG路径绘制动画的原理。[上面这段话来自张鑫旭的博客，解释的非常形象啦。]

我们来看下面的动画的例子：

<a class="jsbin-embed" href="http://jsbin.com/rovexoqu/1/embed">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

没有做不到，只用想不到。

参考文章：

[Using SVG stroke Attributes](http://jonibologna.com/using-svg-stroke-attributes/)


