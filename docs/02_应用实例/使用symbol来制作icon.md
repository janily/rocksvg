### 前言 ###

随大屏幕分辨率的普及以及各种移动设备层出不穷的移动互联网时代，我们在网站设计时更应该关心内容在各种设备上的阅读性和显示效果。我们都希望能在任何时间，任何设备上都能清楚的，高效的传递信息给用户。

而随着各种高清视网膜屏幕的出现，现在web设计也需要考虑各种高清屏幕的显示效果，同样前端在代码实现的时候也需要根据屏幕的不同来输出不同分辨率的图片。为了使我们的网页能够适配视网膜屏幕上的高分辨率，在前端开发中一般需要准备两套不同尺寸的图片来应对，一套在普通屏幕上显示；一套在高清屏幕上显示。

而为了应对屏幕分辨率对图标影响的问题，字体图标即icon font顺势而生。字体图标是一种全新的设计方式。更重要的是相比图片而言，使用字体来制作图标可以不受于屏幕分辨率的影响，这对于现在各种分辨率屏幕的移动互联网时代，比起用图片来说确实有很大的优势。所以现在在web开发中，使用字体来制作icon应用的也越来越多。

难道我们只有这一种选择么？No，追根溯源，其实字体图标也是一种基于矢量图形的一种技术封装而已。这篇文章我们就来看看使用正宗的矢量图形SVG来制作icon的应用，看过之后相信你会有一种“拈花微笑,飞叶伤人”的体验。

### 开始 ###

虽然字体图标应用越来越广泛，但是使用字体制作图标也有它的缺陷。主要缺陷有下面几条：

* 字体图标由于是以字体的形式来引用的。所以浏览器将其视为文字进行抗锯齿优化，有时得到的效果并没有想象中那么锐利。尤其是在不同系统下对文字进行抗锯齿的算法不同，可能会导致显示效果不同，有时候锯齿会很明显。
* Icon Font作为一种字体，Icon显示的大小和位置可能要受到font-size、line-height、word-spacing等等CSS属性的影响。Icon所在容器的CSS样式可能对Icon的位置产生影响，调整起来不是很方便。
* 制作上也不是很方便，自己制作Icon Font以及把多个Icon Font中用到的图标整合成一个Font也非常不方便。
* 使用上存在不便。首先，加载一个包含数百图标的 Icon Font，却只使用其中几个图标，非常浪费加载时间。
* 为了实现最大程度的浏览器支持，可能要提供至少四种不同类型的字体文件。包括TTF、WOFF、EOT以及一个使用SVG格式定义的字体。

所以，开发者们想出了多种使用SVG的技巧来解决/缓解上述问题。主要有下面几种方法：

* 使用img和object标签直接引用svg。这种方法的缺点主要在于要求每个图标都单独保存成一个SVG文件，使用时也是单独请求的，增加了HTTP请求。
* Inline SVG，直接把SVG写入 HTML 中，这种方法简单直接，而且具有非常好的可调性。Inline SVG 作为HTML文档的一部分，不需要单独请求。临时需要修改某个图标的形状也比较方便。但是Inline SVG使用上比较繁琐，需要在页面中插入一大块SVG代码不适合手写，图标复用起来也比较麻烦。
* SVG Sprite。这里所说的Sprite技术，没错，类似于CSS中的Sprite技术。图标图形整合在一起，实际呈现的时候准确显示特定图标。其实基础的SVG Sprite也只是将原来的位图改成了SVG而已。
* 最后就是本文的主角啦。使用svg中的**&lt;symbol&gt;**元素来制作icon。

现在，我们着重介绍的是使用svg中的**&lt;symbol&gt;**元素来制作icon，在上面说到的SVG Sprite中，我们需要使用相对位置来控制哪个图标被显示出来，但是SVG本身的定义是允许你可以使用**&lt;use&gt;**的方式直接引用SVG中的某一部分。

那么**&lt;symbol&gt;**元素是什么呢？按字面意思的话是符号的意思，如果把一个SVG文件比喻成一个书柜的话，那么&lt;symbol&gt;则就表示书柜中一本本不同类别的书籍。这些一本本不同类别的书本就是我们要使用的&lt;symbol&gt;图标。

下面的代码就是将多个SVG图标整合成一个SVG文件之后的样子，可以看到代码中有不同类别的**&lt;symbol&gt;**元素，它们就是我们要引用的图标：

	<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
    <symbol id="film" viewBox="0 0 32 32">
      <title>film icon</title>
      <path stroke="#449FDB" d="M0 0"/><path d="M0 4v24h32V4H0zm6 22H2v-4h4v4zm0-8H2v-4h4v4zm0-8H2V6h4v4zm18 16H8V6h16v20zm6 0h-4v-4h4v4zm0-8h-4v-4h4v4zm0-8h-4V6h4v4zm-18 0v12l8-6z"/>
    </symbol>

    <symbol id="home" viewBox="0 0 32 32">
      <title>home icon</title>
      <path stroke="#449FDB" d="M0 0"/><path d="M16 2L0 18l3 3 3-3 2 12h6v-6h4v6h6l2-12 3 3 3-3L16 2zm0 12.828c-1.562 0-2.83-1.266-2.83-2.828S14.438 9.172 16 9.172c1.562 0 2.828 1.266 2.828 2.828S17.562 14.828 16 14.828z"/>
    </symbol>

    <symbol id="quill" viewBox="0 0 32 32">
      <title>quill icon</title>
      <path stroke="#449FDB" d="M0 0"/><path d="M12 18.333s6.373-3.824 9.96-2.313c.745-1.133 1.478-2.354 2.195-3.6-3.51-.86-8.155-.087-8.155-.087s5.944-3.566 9.583-2.45c.73-1.316 1.44-2.614 2.124-3.822-2.9-.195-5.707.273-5.707.273S25.723 4.1 29.08 3.72C30.138 2.008 31.12.663 32 0 14.47 0 4 20 0 32h2l6-10s2 2 8 0c1.42-.474 2.842-1.79 4.237-3.56-3.52-.892-8.237-.106-8.237-.106z"/>
    </symbol>
	</svg>
	
每个Symbol设置一个id作为引用时的名字。使用id引用这个SVG中的Icon有两种方法。

第一种，将上述SVG作为body的第一个元素插入在HTML中， 此后，在需要显示某个 Icon 的地方插入下面的代码即可：

	<svg class="icon">
  		<use xlink:href="#film"></use>
	</svg>
	
第二种是，是使用完整路径引用Icon。 也就是：

	<svg class="icon">
  		<use xlink:href="/img/posts/svg-icons.svg#film"></use>
	</svg> 
	<svg class="icon">
  		<use xlink:href="/img/posts/svg-icons.svg#home"></use>
	</svg>
	<svg class="icon">
  		<use xlink:href="/img/posts/svg-icons.svg#quill"></use>
	</svg>
	
这种方法不需要像Sprite那样繁琐的设置图片的位移。使用id命名图标并使用时直接使用id引用既直观又简单。

### 自动化合并工具 ###

问题来啦，如果碰到很多的图标，难道我们都要手动去合并为一个SVG吗？当然不用。

这里介绍一个专门用于处理SVG Symbols用的glup插件[gulp-svg-symbols](https://github.com/Hiswe/gulp-svg-symbols)。

下面我们就来以一个实例一步一步来使用下这个插件。

首先新建一个文件夹，目录如下图所示：

![image](http://pic.yupoo.com/reicky_v/DYHtDkbE/VMwfr.png)

当然首先是你得有glup环境，至于glup环境的安装这里就不再阐述了，详细的安装使用教程可以去[这篇文章](http://blog.segmentfault.com/laopopo/1190000000372547)看看。

然后在你的项目目录下运行下面得命令安装插件：

	npm install --save-dev gulp-svg-symbols
	
然后在你的开发目录新建一个**gulpfile.js**文件，写入下面的代码：

	var gulp = require('gulp');
	var svgSymbols = require('gulp-svg-symbols');

	gulp.task('sprites', function () {
  	return gulp.src('assets/svg/*.svg')
    .pipe(svgSymbols())
    .pipe(gulp.dest('assets'));
	});
	
ok。基本的环境搭好啦，正所谓，巧妇难为无米之炊。上哪找svg图标去呢？这里推荐去[icomoon.io](https://icomoon.io/app/#/select)这个专门提供矢量图标网站下载矢量图像，重要的是它提供SVG格式的图形下载。

就以icomoon.io为例，首先是点击你需要下载的图形，选中它，然后点击下载按钮：

![image](http://pic.yupoo.com/reicky_v/DYHtDRYF/medium.jpg)

点击下载svg：

![image](http://pic.yupoo.com/reicky_v/DYHtDFQF/13yakk.png)

然后按照我们上面的配置文件，我们把下载好的svg图标放到svg文件夹中。

一切准备就绪，在你的开发目录中，运行**gulp sprites**命令：

![image](http://pic.yupoo.com/reicky_v/DYHAjkHF/BQSF.png)

运行命令之后，它会在你的目录中生成一个svg文件，用一个编辑器打开svg文件，可以看到我们的svg图标都被合并到一个文件中。并且根据对应SVG文件的名称生成了ID，如下图所示：

![image](http://pic.yupoo.com/reicky_v/DYHtDXXX/custom.jpg)

那怎么使用呢？直接在html文件中使用，还可以直接使用css来定义宽高、填充颜色等属性。如下代码所示：

	<!DOCTYPE html>
	<html lang="en">
	<head>
	<meta charset="UTF-8">
	<title>svg icon</title>
	<style>
		.icon {
			fill: black;
			width: 32px;
			height: 32px;
		}
	</style>
	</head>
	<body>
	<svg class="icon">
	  <use xlink:href="/assets/svg-symbols.svg#film"></use>
	</svg>
	<svg class="icon">
	  <use xlink:href="/assets/svg-symbols.svg#home"></use>
	</svg>
	</body>
	<svg class="icon">
  	  <use xlink:href="/assets/svg-symbols.svg#quill"></use>
	</svg>
	</html>

不过由于浏览器安全策略限制的原因，我们不能在本地直接打开html文件来预览我们引用的svg文件，需要以服务器的形式来打开，用gulp也很容易搞定一个简单的服务器环境。首先我们需要安装**gulp-connect**这个模块，运行下面的命令：

	npm install --save-dev gulp-connect
	
然后在gulpfile.js文件中配置一下：

	var gulp = require('gulp');
	var svgSymbols = require('gulp-svg-symbols');
	var connect = require('gulp-connect');

	gulp.task('webserver',function(){
	connect.server();
	});

	gulp.task('sprites', function () {
  	return gulp.src('assets/svg/*.svg')
    .pipe(svgSymbols())
    .pipe(gulp.dest('assets'));
	});
	
运行**gulp webserver**命令，打开localhost:8080，就可以看到我们引入的svg图标了：

![image](http://pic.yupoo.com/reicky_v/DYHtEeN8/jI1QA.png)

### 总结

综上所述，使用SVG Symbols的方式来制作图标比使用字体图标有着无可比拟的优势。更重要的是SVG中的每一个path元素都可以单独控制，这可以给我们带来什么呢？看看下面的实例你就知道使用SVG来制作图形元素带来的魅力啦。

<p data-height="487" data-theme-id="0" data-slug-hash="yxInL" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/Dianatomic/pen/yxInL/'>SVG icon animations</a> by Dianatomic (<a href='http://codepen.io/Dianatomic'>@Dianatomic</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

我觉的在移动端完全可以普及使用了，主流的安卓和苹果的浏览器都支持SVG。

pc端的话，只有ie8以上的浏览器才支，不过可以使用带fallback的svg sprite的技术来处理。

参考文章：

[Gulp as a Development Web Server](http://code.tutsplus.com/tutorials/gulp-as-a-development-web-server--cms-20903)

[SVG symbol a Good Choice for Icons](http://css-tricks.com/svg-symbol-good-choice-icons/)

[Inline SVG vs Icon Fonts](http://css-tricks.com/icon-fonts-vs-svg/)

[replace-icon-fonts-with-svg](http://io-meter.com/2014/07/20/replace-icon-fonts-with-svg/)
	

	



