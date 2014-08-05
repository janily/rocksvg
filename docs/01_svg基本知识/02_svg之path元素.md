#### 路径－path元素

这个是最通用和最牛逼的元素；使用这个元素可以实现任何的图形，不仅包括上面说到的基本图形，还可以绘制像贝塞尔曲线那样复杂的形状；此外，使用path还可以绘制实现平滑的过渡线段。并且path元素控制位置和形状的只有一个参数：d：一系列绘制指令和绘制参数组合成。

SVG中path的元素，也就是路径绘制，属性名称是d, 具体值是由专门的“指令字母+坐标值”实现的，例如下面这个简单代码示意：

`<path d="M10 10L90 90" stroke="#000000" style="stroke-width: 5px;"></path>`

绘制指令分为绝对坐标指令和相对坐标指令两种，这两种指令使用的字母是一样的，就是大小写不一样，绝对指令使用大写字母，坐标也是绝对坐标；相对指令使用对应的小写字母，点的坐标表示的都是偏移量。

绘制指令如下所示：

<table cellspacing="1" cellpadding="0">
<thead>
<tr>
<th>命令</th>
<th>名称</th>
<th>参数</th>
</tr>
</thead>
<tbody>
<tr>
<td>M</td>
<td>moveto  移动到</td>
<td>(x y)+</td>
</tr>
<tr>
<td>Z</td>
<td>closepath  关闭路径</td>
<td>(none)</td>
</tr>
<tr>
<td>L</td>
<td>lineto  画线到</td>
<td>(x y)+</td>
</tr>
<tr>
<td>H</td>
<td>horizontal lineto  水平线到</td>
<td>x+</td>
</tr>
<tr>
<td>V</td>
<td>vertical lineto  垂直线到</td>
<td>y+</td>
</tr>
<tr>
<td>C</td>
<td>curveto  三次贝塞尔曲线到</td>
<td>(x1 y1 x2 y2 x y)+</td>
</tr>
<tr>
<td>S</td>
<td>smooth curveto  光滑三次贝塞尔曲线到</td>
<td>(x2 y2 x y)+</td>
</tr>
<tr>
<td>Q</td>
<td>quadratic Bézier curveto  二次贝塞尔曲线到</td>
<td>(x1 y1 x y)+</td>
</tr>
<tr>
<td>T</td>
<td>smooth quadratic Bézier curveto  光滑二次贝塞尔曲线到</td>
<td>(x y)+</td>
</tr>
<tr>
<td>A</td>
<td>elliptical arc  椭圆弧</td>
<td>(rx ry x-axis-rotation large-arc-flag sweep-flag x y)+</td>
</tr>
<tr>
<td>R</td>
<td><a href="http://en.wikipedia.org/wiki/Catmull–Rom_spline#Catmull.E2.80.93Rom_spline">Catmull-Rom curveto</a>*  Catmull-Rom曲线</td>
<td>x1 y1 (x y)+</td>
</tr>
</tbody>
</table>

其中，有5个指定属于基本指令，如下表所示：

<table border="0" cellspacing="1" cellpadding="0">
<tbody><tr>
<th scope="col">指令字母（绝对坐标）</th>
<th scope="col">中文含义</th>
<th scope="col">参数示意</th>
<th scope="col">具体说明</th>
</tr>
<tr>
<td>M</td>
<td>移动到(moveTo)</td>
<td>x,y</td>
<td>路径起始点坐标</td>
</tr>
<tr>
<td>Z</td>
<td>闭合路径(closepath)</td>
<td>&nbsp;</td>
<td>将路径的开始和结束点用直线连接</td>
</tr>
<tr>
<td>L</td>
<td>直线(lineTo)</td>
<td>x,y</td>
<td>当前节点到指定(x,y)节点，直线连接</td>
</tr>
<tr>
<td>H</td>
<td>水平直线</td>
<td>x</td>
<td>保持当前点的y坐标不变，x轴移动到x, 形成水平线</td>
</tr>
<tr>
<td>V</td>
<td>垂直直线</td>
<td>y</td>
<td>保持当前点的x坐标不变，y轴移动到y, 形成垂直线</td>
</tr>
</tbody></table>

移动画笔指令M，画直线指令：L，H，V，闭合指令Z都比较简单；下面重点看看跟贝塞尔曲线相关的几个指令。

#### **绘制三次贝塞尔曲线指令：C  x1 y1, x2 y2, x y**

那三次贝塞尔曲线是什么样子的呢？

如下图所示：

![image](https://developer.mozilla.org/@api/deki/files/159/=Cubic_Bezier_Curves.png)

相信各位设计师对这个应该很熟悉啦。比如photoshop中对钢笔工具，或者是其它矢量绘图工具中对曲线工具本质上都是贝塞尔曲线。

一般而言，“三次贝塞尔曲线”的指令是：

` C x1 y1, x2 y2, x y `

三次贝塞尔曲线有两个控制点，就是(x1,y1)和(x2,y2)，最后面(x,y)代表曲线的终点。控制点是用来控制曲线的弧度。体会下面的例子：

<a class="jsbin-embed" href="http://jsbin.com/qizonage/1/embed">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

从上面的例子中，我们可以看到控制点控制啦曲线的弧度。

#### **特殊版本的三次贝塞尔曲线：S  x2 y2, x y**

![image](https://developer.mozilla.org/@api/deki/files/363/=ShortCut_Cubic_Bezier.png)

很多时候，为了绘制平滑的曲线，需要多次连续绘制曲线。这个时候，为了平滑过渡，常常第二个曲线的控制点是第一个曲线控制点在曲线另外一边的映射点。这个时候可以使用这个简化版本。这里要注意的是，如果S指令前面没有其他的S指令或C指令，这个时候会认为两个控制点是一样的，退化成二次贝塞尔曲线的样子；如果S指令是用在另外一个S指令或者C指令后面，这个时候后面这个S指令的第一个控制点会默认设置为前面的这个曲线的第二个控制点的一个映射点，体会一下下面这个实例：

<a class="jsbin-embed" href="http://jsbin.com/jimidomi/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

#### **绘制二次贝塞尔曲线指令：Q  x1 y1, x y ， T x y  (特殊版本的二次贝塞尔曲线)**

二次贝塞尔曲线只有一个控制点(x1,y1)，通常如下图所示：

![image](https://developer.mozilla.org/@api/deki/files/326/=Quadratic_Bezier.png)

如果是连续的绘制曲线，同样可以使用简化版本T。同样的，只有T前面是Q或者T指令的时候，后面的T指令的控制点会默认设置为前面的曲线的控制点的映射点，体会一下：

<a class="jsbin-embed" href="http://jsbin.com/saqumode/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

同样的，如果T指令前面不是Q或者T指令，则认为无控制点，画出来的是直线。

**相对坐标绘制指令**

与绝对坐标绘制指令的字母是一样的，只不过全部是小写表示。这组指令的参数中涉及坐标的参数代表的是相对坐标，意思就是参数代表的是从当前点到目标点的偏移量，正数就代表向轴正向偏移，负数代表向反向偏移。不过对Z指令来说，大小写没有区别。
　　
这里要注意，绝对坐标指令与相对坐标指令是可以混合使用的。有时混合使用可以带来更灵活的画法。

**SVG path绘制注意事项：**

绘制带孔的图形时要注意：外层边的绘制需要是逆时针顺序的，里面的洞的边的顺序必须是顺时针的。只有这样绘制的图形填充效果才会正确。




