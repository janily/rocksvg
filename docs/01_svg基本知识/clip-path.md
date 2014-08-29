这篇文章来看看svg中的clip－path这个属性也就是剪裁蒙板。裁剪路径是由path, text或者基本图形组成的图形。所有在裁剪路径内的图形都可见，所有在裁剪路径外的图形都不可见。

### clip－path属性

**&lt;clip-path&gt;**属性能在svg中使用任意的形状来剪裁任何的图片。svg中的形状主要有**&lt;rect&gt;**,**&lt;circle&gt;**,**&lt;ellipse&gt;**,**&lt;path&gt;**,**&lt;polygon&gt;**,**&lt;image&gt;**,**&lt;text&gt;**等。我们可以使用这些形状任意组合为剪裁路径来剪裁图形。下面来看一个实例：

css

	img {
  	clip-path: url(#clipping);
  	}
  	
html

	<svg>
 	 <defs>
    	<clipPath id="clipping">
     	 <circle cx="284" cy="213" r="213" />
   		 </clipPath>
  		</defs>
		</svg>

	<img src="image.jpg" width="568">
	
如下面这个实例：

<p data-height="339" data-theme-id="0" data-slug-hash="hbLtn" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/awgreenblatt/pen/hbLtn/'>SVG Clip Path</a> by Alan Greenblatt (<a href='http://codepen.io/awgreenblatt'>@awgreenblatt</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

其实对于一些基础的图形可以直接在css中使用clip-path属性来定义而不需要在html中用svg元素来定义。至于svg中的一些基本图形这里就不再阐述了，可以去看以前关于svg基本图形这一章的介绍。

比如我们使用了**polygon**元素来定义来一个剪裁蒙板：

	img {
  		clip-path: polygon(0px 208px, 146.5px 207px, 147px 141.2px, ...);
	}
	
剪裁蒙板对于视觉元素的表现是非常有用的，下面看些实际的例子：

<p data-height="390" data-theme-id="0" data-slug-hash="AwafG" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/janily/pen/AwafG/'>AwafG</a> by janily (<a href='http://codepen.io/janily'>@janily</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

从上面的例子可以看到剪裁蒙板对于提升UI视觉元素的表现力来说有着不可忽视的作用。

<p data-height="268" data-theme-id="0" data-slug-hash="ujgCH" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/janily/pen/ujgCH/'>ujgCH</a> by janily (<a href='http://codepen.io/janily'>@janily</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

滚动上面的例子中的列表，可以看到剪裁蒙板意外区域的内容都被剪裁掉是不可见掉。

### clip-path与动画

使用clip-path也能制作css3动画效果。

<p data-height="373" data-theme-id="0" data-slug-hash="mdiwv" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/janily/pen/mdiwv/'>mdiwv</a> by janily (<a href='http://codepen.io/janily'>@janily</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

如下面的代码所示：

	img:hover {
  		clip-path: polygon(0px 208px, 146.5px 207px, 147px 141.2px, ...);
  		animate: star 3s;
	}

	@keyframes star {
  		0% {
    		clip-path: polygon(0px 208px, 146.5px 207px, 147px 141.2px, ...);
  		},
  		100% {
    		clip-path: polygon(0px 208px, 146.5px 207px, 147px 141.2px, ...);
  		}
	}
	
这就是clip-path一些基本的知识。使用clip－path与css3动画配合可以制作出很多高级的动画效果，另开一篇文章来讲这个。

主要内容来自下面这篇文章：

[masking](http://www.html5rocks.com/en/tutorials/masking/adobe/)
