###svg概述

可缩放矢量图形(Scalable Vector Graphics，简称SVG)是一种使用XML来描述二维图形的语言(SVG严格遵从XML语法)。 SVG允许三种类型的图形对象：矢量图形形状（例如由直线和曲线组成的路径）、图像和文本。 可以将图形对象（包括文本）分组、样式化、转换和组合到以前呈现的对象中。 SVG 功能集包括嵌套转换、剪切路径、alpha 蒙板和模板对象。

SVG绘图是交互式和动态的。 例如，可使用脚本来定义和触发动画。这一点与Flash相比很强大。Flash是二进制文件，动态创建和修改都比较困难。而SVG是文本文件，动态操作是相当容易的。而且，SVG直接提供了完成动画的相关元素，操作起来非常方便。

SVG与其他Web标准兼容，并直接支持文档对象模型DOM。这一点也是与HTML5中的canvas相比很强大的地方(这里注意，SVG内部也是用一个类似的canvas这样的东西来展示SVG图形，到后面你会发现很多特性和HTML5的canvas还有点像；文中如果没明确说明是SVG的canvas的话，都代指HTML5中的canvas元素)。因而，可以很方便的使用脚本实现SVG的很多高级应用。而且SVG的图形元素基本上都支持DOM中的标准事件。可将大量事件处理程序(如“onmouseover”和“onclick”)分配给任何SVG图形对象。 虽然SVG的渲染速度比不上canvas元素，但是胜在DOM操作很灵活，这个优势完全可以弥补速度上的劣势。

###SVG与其它图片格式的比较

#### **与分辨率无关** ####

位图跟分辨率有很大的关系-位图是以像素为基础构建的。放大缩小位图都能引起图像质量的变化。但是对于矢量图像来说没有这个问题，与分辨率无关。SVG 图像可在任何的分辨率下被高质量地显示。[Retina Display](http://www.hongkiat.com/blog/mbp-retina-blurry-text/)。

#### **减少HTTP请求** ####

SVG格式的图片可以直接以*svg*文本节点的形式插入到HTML文档中，所以浏览器不需要再额外的向服务器发送请求来取得图片。这对于提高网站的性能有很大的帮助。

#### **可以用样式和脚本控制** ####

由于SVG是以文本节点的形式插入操网页中，所以我们可以通过样式来控制矢量图形的表现形式，比如背景颜色、边框、透明度等等，就像我们平时定义HTML文档的样式一样简单。同样，我们也可以使用javascript来控制它。

#### **可以使用动画和编辑** ####

我们可以使用一些第三方的库比如jQuery来操作SVG对象，从而产生动画效果。还可以使用文本编辑器来编辑SVG文件，比如[inkscape](http://inkscape.org/)和[Adobe illustrator](http://www.adobe.com/products/illustrator.html)。

#### **更小的文件体积** ####

SVG 与 JPEG 和 GIF 图像[压缩](http://www.hongkiat.com/blog/jpeg-optimization-guide/)比起来，尺寸更小，且可压缩性更强。

###SVG的呈现方式

现在大部分的浏览器都支持svg格式都文件，不过IE只有在IE9以上的版本才支持。

svg在html文件中主要的呈现方式有以下两种，看下面的例子:

####内联到html

SVG是标准的HTML元素，直接写到HTML中就可以了，如下所示：

<a class="jsbin-embed" href="http://jsbin.com/yuneruzu/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

####独立svg文件

1、独立的svg文件，定义的模板就像下面这样：

`<svg width="100%" height="100%">   
  <!-- SVG markup here. -->    
</svg>`

不过现在很少这样使用。

2、html引用外部的svg文件。

使用object或者是img元素嵌入svg图形就可以了，如下所示：

`<!DOCTYPE html>`
`<html>`
`<head>`
 `<title> My First SVG Page</title>`
`</head>`
`<body>`
  `<object data="sun.svg" type="image/svg+xml"`
          `width="300px" height="300px">`
    `<p>Your browser does not support SVG - please upgrade to a modern browser.</p>`
  `</object>`

`  <img src="sun.svg" alt="svg not supported!" />`
`</body>`
`</html>`

**注意：SVG是以XML定义的，所以是大小写敏感的，这点与HTML不一样。**

svg简单的介绍就到这里啦！




	