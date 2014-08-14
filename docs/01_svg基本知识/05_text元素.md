SVG的强大能力之一是它可以将文本控制到标准HTML页面不可能有的程度，而无须求助图像或其它插件。任何可以在形状或路径上执行的操作（如绘制或滤镜）都可以在文本上执行。

这里我们来说说**&lt;text&gt;**这一元素。

当我们直接在html文件中使用**&lt;text&gt;**元素的时候，需要把它放置在**&lt;svg&gt;**元素里面。我们可以使用相关的属性来定义文字的排版方向，字体等表现形式。

先来看看下面这个例子：

<a class="jsbin-embed" href="http://jsbin.com/lifafapo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

在上面的例子中，我们设置来下面这些属性：

* x,y是文本位置坐标。在上面的例子中，我们定义来文字开始的位置是x轴往右30px，y轴方向往下30px。
* fill,stroke：填充和描边颜色。
* font的相关属性：font-family, font-style, font-weight, font-variant, font-stretch, font-size, font-size-adjust, kerning, letter-spacing, word-spacing and text-decoration。

### tspan元素

这个元素是text元素的强力补充；它用于渲染一个区间内的文本；它只能出现在text元素或者tspan元素的子元素中。典型的用法就是强调显示部分文本。

例如下面这个例子：

<a class="jsbin-embed" href="http://jsbin.com/jidowudoneza/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

tspan元素有下面这些属性可以设置：

* x,y用于设置包含的文本的绝对坐标值，这个值会覆盖默认的文本位置。这些属性可以包含一系列数字，这些数字会应用到每个对应的单个字符。没有对应设置的字符会紧跟前一个字符。
* dx,dy用于设置包含的文本相对于默认的文本位置的偏移量。这些属性同样可以包含一系列数字，每个都会应用到对应的字符。没有对应设置的字符会紧跟前一个字符。你可以把上面的例子中的x换成dx看看效果。

通过设置dx，dy可以单独的移动每个字符的位置，我们来看下面这个例子：

<a class="jsbin-embed" href="http://jsbin.com/tamupiyugiqo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

我们给**are**这个单词的dy属性指定了三个字符，可以看到are的每个字符都有偏移。

### rotate属性

rotate用于设置字体的旋转角度。这个属性页可以包含一系列数字，应用到每个字符。没有对应设置的字符会使用最后设置的那个数字。

当然我们也可以通过设置**transform**属性来旋转，下面这个例子是通过设置**rotate**属性来旋转字符串的：

<a class="jsbin-embed" href="http://jsbin.com/zejonizatuwi/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

### textLength 和 lengthAdjust

**textLength**属性是用来指定文字的长度的。

SVG将适合文本到给定的空间。它是通过调节字形之间的空间，留下不变的字形本身，或者它可以为适合的话，通过调整的间距和字形大小。如果你想只调整空间，设置间距（这是默认的）lengthAdjust的价值。如果你想SVG调整间距和字形大小，以适应到一个给定长度的话，设置lengthAdjust到spacingAndGlyphs。

<a class="jsbin-embed" href="http://jsbin.com/cojeqefijaca/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

下面是设置了**lengthAdjust**属性值为spacingAndGlyphs的情形：

<a class="jsbin-embed" href="http://jsbin.com/hepiqijusale/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>



