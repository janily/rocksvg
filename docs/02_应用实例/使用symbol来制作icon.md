这篇文章来讲讲使用svg来代替Icon Font制作icon的应用。

现在在web开发中，使用字体来制作icon应用的越来越多，使用字体来制作图标可以不受于屏幕分辨率的影响，这对于现在各种分辨率的终端设备的互联网时代，比起用图片来说确实有很大的优势。

但是使用字体制作图标也有它的缺陷，CSS Trick的[inline SVG vs Icon Font](http://css-tricks.com/icon-fonts-vs-svg/)这篇文章总结的相当的全面。主要缺陷有下面几条：

* 浏览器将其视为文字进行抗锯齿优化，有时得到的效果并没有想象中那么锐利。 尤其是在不同系统下对文字进行抗锯齿的算法不同，可能会导致显示效果不同。
* Icon Font 作为一种字体，Icon 显示的大小和位置可能要受到font-size、line-height、word-spacing等等 CSS 属性的影响。 Icon 所在容器的 CSS 样式可能对 Icon 的位置产生影响，调整起来很不方便。
* 使用上存在不便。首先，加载一个包含数百图标的 Icon Font，却只使用其中几个图标，非常浪费加载时间。 自己制作 Icon Font 以及把多个 Icon Font 中用到的图标整合成一个 Font 也非常不方便。
* 为了实现最大程度的浏览器支持，可能要提供至少四种不同类型的字体文件。包括TTF、WOFF、EOT 以及一个使用 SVG 格式定义的字体。

所以，开发者们想出了多种使用 SVG 的技巧来解决 / 缓解上述问题。主要有下面几种方法：

* 比如使用img和object标签直接引用svg。这种方法的缺点主要在于要求每个图标都单独保存成一个 SVG 文件，使用时也是单独请求的。
* Inline SVG，直接把 SVG 写入 HTML 中，这种方法简单直接，而且具有最强的可调性。Inline SVG 作为 HTML 文档的一部分，不需要单独请求。临时需要修改某个图标的形状也比较方便。 但是 Inline SVG 使用上比较繁琐，需要在页面中插入一大块 SVG 代码因此不适合手写，图标复用起来也比较麻烦。
* SVG Sprite。这里所说的Sprite技术，没错，类似于CSS中的Sprite技术。图标图形整合在一起，实际呈现的时候准确显示特定图标。基础的 SVG Sprite 其实只是将原来的位图改成了 SVG。

现在，我们着重介绍的是使用svg中的**&lt;symbol&gt;**元素来制作icon，中以前的sprite中，我们需要使用相对位置来控制哪个图标被显示出来， 但是其实 SVG 本身的定义允许你以某一种方式直接引用 SVG 中的某一部分。

将多个图标整合成一个 SVG 中的多个 Symbols 之后是下面这样的：

	<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">

    <symbol id="circle-cross" viewBox="0 0 32 32">
      <title>circle-cross icon</title>
      <path d="M16 1.333q2.99 0 5.703 1.161t4.677 3.125 3.125 4.677 1.161 5.703-1.161 5.703-3.125 4.677-4.677 3.125-5.703 1.161-5.703-1.161-4.677-3.125-3.125-4.677-1.161-5.703 1.161-5.703 3.125-4.677 4.677-3.125 5.703-1.161zm0 2.667q-2.438 0-4.661.953t-3.828 2.557-2.557 3.828-.953 4.661.953 4.661 2.557 3.828 3.828 2.557 4.661.953 4.661-.953 3.828-2.557 2.557-3.828.953-4.661-.953-4.661-2.557-3.828-3.828-2.557-4.661-.953zm3.771 6.885q.552 0 .948.391t.396.943-.396.948l-2.833 2.833 2.833 2.823q.396.396.396.938 0 .552-.396.943t-.948.391-.938-.385l-2.833-2.823-2.823 2.823q-.385.385-.948.385-.552 0-.943-.385t-.391-.938q0-.563.385-.948l2.833-2.823-2.833-2.833q-.385-.385-.385-.938t.391-.948.943-.396.948.396l2.823 2.833 2.833-2.833q.396-.396.938-.396z"/>
    </symbol>

    <symbol id="circle-check" viewBox="0 0 32 32">
      <title>circle-check icon</title>
      <path d="M16 1.333q2.99 0 5.703 1.161t4.677 3.125 3.125 4.677 1.161 5.703-1.161 5.703-3.125 4.677-4.677 3.125-5.703 1.161-5.703-1.161-4.677-3.125-3.125-4.677-1.161-5.703 1.161-5.703 3.125-4.677 4.677-3.125 5.703-1.161zm0 2.667q-2.438 0-4.661.953t-3.828 2.557-2.557 3.828-.953 4.661.953 4.661 2.557 3.828 3.828 2.557 4.661.953 4.661-.953 3.828-2.557 2.557-3.828.953-4.661-.953-4.661-2.557-3.828-3.828-2.557-4.661-.953zm4.49 7.99q.552 0 .943.391t.391.943-.396.948l-5.656 5.656q-.385.385-.938.385-.563 0-.948-.385l-2.833-2.823q-.385-.385-.385-.948 0-.552.391-.943t.943-.391.948.396l1.885 1.885 4.708-4.719q.396-.396.948-.396z"/>
    </symbol>

    <!-- .... -->
	</svg>
	
每个Symbol设置一个id作为引用时的名字。使用id引用这个SVG中的Icon有两种方法。

第一种，将上述 SVG 作为 body 的第一个元素插入在 HTML 中 (Chrome 存在一个 bug 导致不在这里显示不出图像)， 此后，在需要显示某个 Icon 的地方插入下面的代码即可：

	<svg class="icon">
  	<use xlink:href="#circle-cross"></use>
	</svg>
	
第二种是，是使用完整路径引用 Icon。 也就是：

	<svg class="icon">
  	<use xlink:href="/img/posts/svg-icons.svg#circle-check"></use>
	</svg> 
	<svg class="icon">
  	<use xlink:href="/img/posts/svg-icons.svg#circle-cross"></use>
	</svg>
	
这种方法不需要像Sprite那样繁琐的设置图片的位移。使用id命名图标并使用时直接使用id引用既直观又简单。

对于IE则需要使用object标签代替&lt;svg&gt;&lt;use&gt;。关于兼容性讨论详见[这篇文章](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)。

### 自动化合并工具

问题来啦，如果碰到很多的图标，难道我们都要手动去写吗？当然不用。

这里介绍一个专门用于处理SVG Symbols用的glup插件[gulp-svg-symbols](https://github.com/Hiswe/gulp-svg-symbols)。

下面我们就来一步一步来使用下这个插件。

首先是你得有glup环境。

然后运行下面得命令安装插件：

	npm install --save-dev gulp-svg-symbols
	
然后在你的开发目录新建一个**gulpfile.js**文件，写入下面的代码：

	var gulp = require('gulp');
	var svgSymbols = require('gulp-svg-symbols');

	gulp.task('sprites', function () {
  	return gulp.src('assets/svg/*.svg')
    .pipe(svgSymbols())
    .pipe(gulp.dest('assets'));
	});
	
ok。基本的环境搭好啦，正所谓，巧妇难为无米之炊。上哪找svg图标去呢？这里推荐去阿里系的[iconfont.cn](http://iconfont.cn/)下载。

就以iconfont.cn为例，首先是点击某一个图标，然后点击下载按钮：

![image](http://pic.yupoo.com/reicky_v/DYezp8Y4/small.jpg)

点击下载svg：

![image](http://pic.yupoo.com/reicky_v/DYezm6oP/small.jpg)

按照我们上面的配置文件，我们把下载好的svg图标放到svg文件夹中。

一切准备就绪，在你的开发目录中，运行**gulp sprites**命令：

运行命令之后，它会在你的目录中生成一个svg文件，用一个编辑器打开svg文件，可以看到我们的svg图标都被合并到一个文件中。并且根据对应文件到名称生成了ID。

![image](http://pic.yupoo.com/reicky_v/DYeY1IQ4/medium.jpg)

那怎么使用呢？直接在html文件中使用，还可以直接使用css来定义宽高、颜色等属性。如下代码所示：

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
	  <use xlink:href="/assets/svg-symbols.svg#iconfont-appreciate"></use>
	</svg>
	<svg class="icon">
	  <use xlink:href="/assets/svg-symbols.svg#iconfont-discover"></use>
	</svg>
	</body>
	</html>

不过由于浏览器安全限制到原因，我们不能在本地直接打开html文件来预览我们引用的svg文件，需要以服务器的形式来打开，用gulp也很容易搞定一个简单的服务器环境。首先我们需要安装**gulp-connect**这个模块，运行下面的命令：

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

![image](http://pic.yupoo.com/reicky_v/DYeZjwM2/small.jpg)

### 总结

在移动端完全可以普及使用了，主流的安卓和苹果的浏览器都支持。

pc端的话，只有ie8以上的浏览器才支，不过可以使用带fallback的svg sprite。

参考文章：

[Gulp as a Development Web Server](http://code.tutsplus.com/tutorials/gulp-as-a-development-web-server--cms-20903)

[SVG symbol a Good Choice for Icons](http://css-tricks.com/svg-symbol-good-choice-icons/)

[Web 设计新趋势: 使用 SVG 代替 Web Icon Font](http://io-meter.com/2014/07/20/replace-icon-fonts-with-svg/)
	

	



