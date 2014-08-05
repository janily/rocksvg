前面介绍svg绘制相关图形的知识，接下来，就是给它们上色。在SVG绘图中，可以使用若干方法上色，比如给图形对象增加指定的属性，使用行间CSS，使用CSS嵌入段落，或者使用外部引用的CSS文件。

#### 填充颜色 － fill属性

这个属性可以用来填充图形内部的颜色，使用非常简单，直接把颜色值赋给这个属性就可以来，如下面这个例子所示：

<a class="jsbin-embed" href="http://jsbin.com/hilikizo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

此外，在SVG中你可以分别定义填充色和边框色的透明度，它们分别由 fill-opacity 和 stroke-opacity 两个属性控制。

#### 使用css

上面我们是直接使用定义对象的属性来制定fill和stroke的。当然也可以通过CSS来定义fill和stroke。语法和在html里使用CSS一样，只不过你要把background-color、border改成fill和stroke。注意，不是所有的属性都能用CSS来设置。上色和填充的部分一般是可以用CSS来设置的，比如fill，stroke，stroke-dasharray等，但是不包括下面会提到的渐变和模式等功能。另外，宽、高，以及路径的d命令，都不能用css设置。

SVG规范将属性区分成properties和其他attributes，前者是可以用CSS设置的，后者不能。CSS可以通过style属性插入到元素的行间:

	<rect x="10" height="180" y="10" width="180" style="stroke: black; fill: red;"/>
	
或者通过<style>设置一段样式段落。在html里这样的段落一般放在里，在svg则放在<defs>标签里。<defs>表示定义，这里可以定义一些不会在SVG图形中出现的元素，但是它们可以被其他元素使用。

	<?xml version="1.0" standalone="no"?>
	<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  	<defs>
    <style type="text/css"><![CDATA[
       #MyRect {
         stroke: black;
         fill: red;
       }
              
    ]]></style>
  	</defs>
  	<rect x="10" height="180" y="10" width="180" id="MyRect"/>
	</svg>
	
通过使用style段落你可以更轻易地调整一大组元素的样式，同样你也可以通过hover这样的伪类来创建翻转之类的效果:

<a class="jsbin-embed" href="http://jsbin.com/bumiyuwo/1/embed?html,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

当然，你也可以定义一个外部的样式表，但是要符合normal XML-stylesheet syntax的CSS规则:

	<?xml version="1.0" standalone="no"?>
	<?xml-stylesheet type="text/css" href="style.css"?>
	<svg width="200" height="150" xmlns="http://www.w3.org/2000/svg" version="1.1">
  	<rect height="10" width="10" id="MyRect"/>
	</svg>
	
是不是很熟悉，就是这么简单的。

下篇接着来讲讲stroke这一属性即边框。

