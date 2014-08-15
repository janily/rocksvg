SVG存在两套坐标系统：视窗坐标系与用户坐标系。默认情况下，用户坐标系与视窗坐标系的点是一一对应的，都为原点在视窗的左上角，x轴水平向右，y轴竖直向下；如下图所示： 

![image](https://developer.mozilla.org/@api/deki/files/78/=Canvas_default_grid.png)

SVG的视窗位置一般是由CSS指定，尺寸由SVG元素的属性width和height设置，但是如果SVG是存储在embedded对象中(例如object元素，或者其他SVG元素)，而且包含SVG的文档是用CSS或者XSL格式化的，并且这些外围对象的CSS或者其他指定尺寸的值已经可以计算出视窗的尺寸了，则此时会使用外围对象的尺寸。

这里需要区分视窗，视窗坐标系，用户坐标系的概念：

视窗：指的是网页上面可视的矩形局域，长度和宽度都是有限的，这个区域一般与外围对象的尺寸有关。

视窗坐标系：本质是一个坐标系，有原点，x轴与y轴；而且在两个方向上是无限延伸的。默认情况下，原点在视窗的左上角，x轴水平向右，y轴竖直向下。可以对这个坐标系的点进行变换。

用户坐标系：本质是一个坐标系，有原点，x轴与y轴；而且在两个方向上是无限延伸的。默认情况下，原点在视窗的左上角，x轴水平向右，y轴竖直向下。可以对这个坐标系的点进行变换。

默认情况下，视窗坐标系与用户坐标系是重合的，但是这里需要注意，视窗坐标系属于的是创建视窗的元素，视窗坐标系确定好以后，整个视窗的坐标基调就确定了。但是用户坐标系是属于每个图形元素的，只要图形进行了坐标变换，就会创建新的用户坐标系，这个元素中所有的坐标和尺寸都使用这个新的用户坐标系。

简单点说：视窗坐标系描述了视窗中所有元素的初始坐标概况，用户坐标系描述了每个元素的坐标概况，默认情况下，所有元素都使用默认的与视窗坐标系重合的那个用户坐标系。

### viewBox

所有的能建立一个视窗的元素(svg,symbol,image)，再加上marker,pattern,view元素，都有一个viewBox属性。

用法viewBox(xmin, ymin, width, height)。
查看文档可知道viewBox作用是拉伸图形。它是如何控制拉伸的？要想拉伸的话，指定长宽比例就可以了，怎么会用到xmin, ymin, width, height这些值，它们是和拉伸有什么关系？怎么理解？
实际上拉伸只是它的一个功能，换一种叫法就很好理解: 取景框. 它使用xmin,ymin,width,height这些参数确定取景范围，然后将取到的景象，放到svg中，并且充满整个svg。如果取到的景象比svg可视范围小，则景象会被放大再充满svg；如果取到的景象比svg可视范围大，取景会被缩小再充满svg. 所以viewbox有两个功能：一是填充功能；二是拉伸。
### preserveAspectRatio
preserveAspectRatio属性只有在该元素设置了viewBox以后才会起作用。如果没有设置viewBox，则preserveAspectRatio属性会被忽略。
有些时候，特别是当使用viewBox的时候，我们期望图形占据整个视窗，而不是两个方向上按相同的比例缩放。而有些时候，我们却是希望图形两个方向是按照固定的比例缩放的。使用属性preserveAspectRatio就可以达到控制这个的目的。

属性的语法如下：preserveAspectRatio="[defer] <align> [<meetOrSlice>]"。

注意3个参数之间需要使用空格隔开。

* defer:可选参数，只对image元素有效，如果image元素中preserveAspectRatio属性的值以"defer"开头，则意味着image元素使用引用图片的缩放比例，如果被引用的图片没有缩放比例，则忽略"defer"。所有其他的元素都忽略这个字符串。
* align:该参数决定了统一缩放的对齐方式，可以取下列值：
  none - 不强制统一缩放，这样图形能完整填充整个viewport。
  xMinYMin - 强制统一缩放，并且把viewBox中设置的<min-x>和<min-y>对齐到viewport的最小X值和Y值处。
  xMidYMin - 强制统一缩放，并且把vivewBox中X方向上的中点对齐到viewport的X方向中点处，简言之就是X方向中点对齐，Y方向与上面相同。
  xMaxYMin - 强制统一缩放，并且把viewBox中设置的<min-x> + <width>对齐到viewport的X值最大处。
  类似的还有其他类型的值：xMinYMid,xMidYMid,xMaxYMid,xMinYMax,xMidYMax,xMaxYMax。这些组合的含义与上面的几种情况类似。
* meetOrSlice：可选参数，可以去下列值：
  meet - 默认值，统一缩放图形，让图形全部显示在viewport中。
  slice - 统一缩放图形，让图形充满viewport，超出的部分被剪裁掉。
  
下图诠释了各种填充的效果：

![image](http://images.cnblogs.com/cnblogs_com/dxy1982/preserveAspectRatio.png)

下面我们来看一些实际的例子。

在第一个例子中，我们把viewBox的宽高设置和svg本身的尺寸一致。刚好填充满整个svg文档，如下所示：

<a class="jsbin-embed" href="http://jsbin.com/luhewequvoge/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

如果我们把viewBox的宽高设置为50和140，由于比svg可视范围小，所以图形会放大并填充svg。如下所示：

<a class="jsbin-embed" href="http://jsbin.com/lifenulitoge/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

而viewBox前面的两个参数xmin，ymin则使用移动用户坐标点的，负数表示往y轴的下方或者是x轴的右方移动。反之亦然，如下例所示：

<a class="jsbin-embed" href="http://jsbin.com/qawubupotili/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

理解svg的坐标系统对于我们更好的控制svg和创建svg是非常有用的。

参考文章：

[http://jonibologna.com/svg-viewbox-and-viewport/](A Look At SVG viewBox and viewport)







