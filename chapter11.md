# JavaScript Dom编程艺术

- [第11章 HTML5](chapter11.md)
  - [11.1 HTML5简介](chapter11.md#111)
  - [11.2 来自朋友的忠告](chapter11.md#112)
  - [11.3 几个示例](chapter11.md#113)
    - [11.31 Canvas](chapter11.md#1131)
    - [11.32 音频和视频](chapter11.md#1132)
    - [11.33 表单](chapter11.md#1133)
  - [11.4 HTML5还有其他特性吗](chapter11.md#114)
  - [11.5 小结](chapter11.md#115)
  11.2来自朋友的忠告
如果你今天就想用HTML5,那太好了，赶紧吧！在作出决定之后，我想向你推荐一个工具: Moderaizr® 〇
Modemizr (

http://www.modemizr.com/)是一个开源的JavaScript库，利用它的富特性检测功能， 可以对HTML5文档进行更好的控制。Modemizr不会给你添加浏览器不支持的特性，比如，在IE6 中就没有办法使用本地存储。Modemizr能做的是为你提供一些不同的CSS类名以及特性检测 (feature-detection)属性。要想现在使用HTML5，Modemizr是必不可少的，它的用途也不止于此。
在文档中嵌入Modemizr之后，它会随着页面加载变一些小戏法。
首先，它会修改<咕(111>的Class属性，基于可用的HTML5特性添加额外的类名。要使用 Modemizr编写文档，通常都要给<html>元素添加一个no)类：	"
chtml class="no-jsn>
利用这个类，可以在浏览器不支持JavaScript的情况下应用CSS样式。
奏
•nojs selector { style properties
}
然后，Modemizr会检测浏览器可能支持的各种特性，并相应地添加类名。如果浏览器支持 某些特性，经它修改后的类名大致如下所示：
<html class=Mjs canvas canvastext geolocation crosswindowmessaging websqldatabase indexeddb hashchange historymanagement draganddrop websockets rgba hsla multiplebgs backgroundsize borderimage borderradius boxshadow opacity cssanimations csscolumns cssgradients cssreflections csstrans干orms csstransforms3d csstransitions video audio localstorage sessionstorage webworkers applicationcache svg smil svgclippaths fontfaceu>
如果浏览器不支持某些特性，经它修改后的类名应该如下所示：
<h;tml class=irjs no-canvas no垂canvastext nogeolocation no-crosswindowmessaging no- websqldatabase no-indexeddb no-hashchange no-historymanagement no-draganddrop no-websockets no-rgba no-hsla no-multiplebgs no-backgroundsize no-borderimage no-borderradius no-boxshadow no-opacity no-cssanimations no-csscolumns no-cssgradients no-cssreflections no-csstrans千orms no-csstransformsBd no-csstransitions no-video no-audio no-local$torage no-sessionstorage no- webworkers no-applicationcache no-svg no-smil no-svgclippaths no-fontface">
当然，实际情况是浏览器可能会支持部分特性，而不支持另一些特性。这时候，类名中就会 间或出现 feature 和I no-feature。
根据这些类名，可以在CSS中定义相应的增强和退化版本，改善用户体验：
•multiplebgs article p {
/*为支持多背景浏览器编写的样式*/
}
•no-multiplebgs article p {
/*为不支持多背景的浏览器编写的后备样式V
①读者也可以从 GitHuly (

https://github.com/Modemizr/Modemizr)下载 Modemizr。	译者注

204 第 11 章 HTML5
类似地，Moderaizr库也提供了 JavaScript特性检测对象，可以在DOM脚本中直接使用：
if ( !Modernizr.inputtypes•date ) {
/*不支持本地数据，使用自定义的数据选择脚本*/ createDatepicker(document.getElementById('birthday1));
}
Modemizr还可以帮一些老旧的浏览器处理<sect1orP^<art1cle>^样的新元素。有的读者可 能还不知道，其实你可以在大多数浏览器中创建类似<f〇〇>3t样的元素，然后再为该元素应用样 式——只要你不在乎验证结果就无所谓。对于这些浏览器来说，新的HTML5元素（如<sect1on>) 也照样可以拿来就用。为使用这些新元素，你要做的就是为它们指定一些基本的样式，以便浏览 器可以把它们当做块元素来呈现：
article, aside, footer, header, hgroup, nav, section { display: block;
} .)
唯一的特例就是IE。要在IE中添加未知元素，必须先使用类似下面的JavaScript代码来创 建该元素：
document•createElement(1 article1);
Modemizr可以帮我们来做这件事；但是，这并不意味着你就可以放心地使用〜1(^〇>元素嵌 入视频了。Modemizr不会为我们添加底层的JavaScript及DOM API，或者与这些元素相关的其
他特性。
使用Modemizr非常简单，从

http://www.modemizr.com/下载它，将在文档的<1^(1>中添加该 脚本：
〈script sro"moderniz：n5 JirujsM></script>
一定要把这个脚本放在<1163(>元素中。虽然这与第5章建议的不一致，但这样做有特殊的原 因。把Moderaizr放在文档开头，可以在加载其他标记之前先加载它，以便它在文档呈现之前能 够创建好新的HTML5元素。要是把它放到了文档的末尾，那么等不到Modemizr发挥作用，浏 览器就已经开始呈现文档并应用样式了。
11.3几个示例
为了让读者朋友尝尝鲜，下面我们就介绍一些有关Canvas、视频/音频以及表单的例子，看 一看HTML5都提供了什么API。要想试验以下的示例，需要下列浏览器。
□苹果 Safari 5+
Q 谷歌 Chrome 6+
Mozilla Firefox 3.6+
Opera 10.6+
□微软IE 9+

Canvas
11.3 几个示例	205
每个浏览器都可以显示静态图片。通过GIF可以实现一些动画，或者使用CSS加JavaScript
也能变化一些样式，但仅此而已。要想与静态图片交互可就难上加难了。HTML5的<canvas>元素
让这一切成为了历史，通过它可以动态创建和操作图形图像。
在网页中支起一块“画布”（canvas)很简单：
〈canvas id=ndraw-in-me" width="l2〇" height="4〇">
<p>Powered By HTML5 canvas</p>
</canvas>
在这张“画布”上作画嘛，可就是另外一回事了。要了解详细的绘画方法，请参考<^_5>
元素的规范（h郎://

www.whatwg.org/specs/web-apps/current-work/multipage/the-canvas-element.
html)。不过从本质上来讲，<canvas>涉及的数学及定位的概念与Adobe Illustrator等基于矢量的 图形软件或者基于矢量的编程语言没有太大的差别。
注意如果读者使用过 Dlustrator，可以试试使用 Ai_>Canvas插件(

http://visitmix.com/labs/ai2canvas/)， 虽然作为“所见即所得”的编辑器，免不了会在输出中生成一些冗余的东西，但通过手 工编辑还是能得到最佳效果的。
下面这个例子利用<canvas>画一个圆角小黑盒子，带有2像素宽的白色描边效果。
function draw() {
var canvas = document^getEleinentById('draw-in-me* 1); if (canvas•getContext) { var ctx : canvas*getContext(l2d,); ctx^beginPath(); ctx.moveTo(i2CL〇, 32.0);
ctx.bezierCurveTo(l20.0, 36^4, 116.4, 40*0^ 112.0, 40*0)； ctx.lineTo(8.0, 40.0);
1 ctx.bezierCurveTo(B^6j 40*0, 〇•〇> 36.4, 〇•〇> 32*0)； ctx.lineTo(0,0, 8,0);
ctx.bezierdurveTo(〇,〇,	夂6^ 〇•〇,	〇•〇);
ctx.lineTo(112.〇, 0•0);
ctx#bezierCurveTo(ll6.4> 〇♦〇, 120.0, 3^6, 120.0, 8.0);
ctx.lineTo(l20^0> 32.0);
ctx^closePath();
ctx.fill();
ctx.lineWidth = 2*0；
ctx.strokeStyle = "rgb(255, 255, 255)";
ctx^stroke();
}
}
window^onload ^ draw;
在这个例子中，变量ctx引用的是画布的绘图空间（context)。所谓绘图空间，在这里就是 一个平面二维的绘图表面，其原点(0,0)位于左上角。在这个绘图表面的坐标系里，越 往右x的值越大，右往下y的值越大。通过在绘图空间中指定坐标点，可以绘制出各种二维的形 状和线条。在绘制线条时，还可以添加不同的填充及描边样式。

206 第 11 章 HTML5
图11-1是在Chrome中显示的结果:



当然，这个例子还很简陋。例子中的<canvas>元素使用了与其他2D绘图库相似的API。这里 使用了几个点和曲线从一个点到另一个点创建并绘制出了一条路径，但<〇3^35>可不仅仅能够用 来绘制矢量路径；还可以通过它来显示和操作位图图像。
比如说，我们可以使ffl<canvas>对象在浏览器中把一幅彩色图片变成灰度图片。然后，当用 户的鼠标悬停到图片上面时，再把它切换回原始的彩色图片。
先创建一个HTML文件，命名为gmySCale.html，其中有一幅图像，与脚本位于同一个域中。 这个页面里也使用了 Modemizr:
<!D0CTYPE html>
<html lang="en">
<head>
<meta charset=,futf-8M />
<title>Grayscale Canvas Example</title>
〈script src=Mscripts/inodernizr-i.6^min〇sn></script>
</head>
<body>
<img src="images/avatar,png" id="avatar" title=”]effrey Sambells"	Avatar"/〉
<script src=,fscripts/grayscale^jsnx/script>
</body>
</html>
再创建一个grayscale.js文件，并在其中添;(j卩如下脚本:
function convertToGS(img) {
//如果浏览器不支持<canvas>就返回 if (IModernizr^canvas) return:

11,3 几个示例 207
//存储原始的彩色版 img•color = img.src;
//创建灰度版
img^grayscale = createGSCanva s(img);
//在mouseover/out事件发生时切换图片 img.onmouseover = function() { this.sic - this•color;
>
img.onmouseout = function() {
this^src = this•grayscale;
img.onmouseout();
function createGSCanvas(img) {
var canvas=document.createElement(l,canvasH); canvas.width= img.width; canvas.height=img^ height;
var ctx=canvas • getContext(’’2cT); ctx.drawImage(img,〇,〇);
//注意：getlmageData只能操作与脚本位于同一个域中的图片 var c = ctx.getlmageData^o, 0, img,width, img^height); for (i=0; i<。heightj i++) { for (]、0; j<c^width; j++) { var x = (i*4) * c.width + (j*4)； var r = c.data[x];
var g
var b
c.data
c.data
x+l
x+2
c」ata[x] = c.data[x+i]
c.data[x+2] = (r+g+b)/3;



ctx^putImageData(c,0,0,0,0, c.width, c^height); return canvas.toDataURL();
//添加load事件。如果有其他脚本，可以使用addLoadEvent函数 window*onload =十unction().
convertToGS(document•getElementById(,avatar1));
注意在从图片之类的文件中读取数据时，不同浏览器有不同的安全考虑。为了保证这个例子 正常运行，必须在同一个站点中提供图片和文挡。而且，就算在本地硬盘中使用file协 议加载这个页面，例子也无法运行。虽然可以彳參改浏览器的安全设置，但我还是建议把 这个例子的相关文件都上传到Web服务器中。
11
页面加载后，脚本通过在convertToGS函数中应用mouseover和mouseout事件处理函数来修改

208 第 11 章 HTML5
avatar.png 图片。
img,color = img^src; img.grayscale = createGSCanvas(img); img.onmouseover = function() { this•src^this•color;
>
img.onmouseout = function() {
this^src=this•grayscale;
}
上述事件处理函数会切换保存在图片的Six属性中的原始彩色版，以及createGSCanvas函数 创建的灰度版。
为了在createGSCanvas函数中把彩色图片转换为灰度图片，我们创建了一个新的canvas元素， 然后在其绘图环境中绘制了彩色图片：
var canvas=document.createElefnent(Mcanvasn);
canvas.width: img.width;	•	^
canvas•height^img•height;
var ctx=canvas^getContext(l!2d,!); ctx^drawlmage(img>0,0);
接下来，再取得原始的图像数据，循环遍历其中的每一个像素，将每个彩色像素的红、绿、 蓝彩色成分求平均值，得到对应彩色值的灰度值。
var c = ctx.getImageData(〇, 0, img.width， img•height); for (i=0; i<c^height; i++) {
干or (]•=〇; j<c,width; j++) { var x = (i*4) * c^width + (j*4); var r = c」ata[x];
var g = c^data[x+l var b = c.data[x+2
c.data[x] = c.data[x+l] = c.data[x+2] = (r+g+b)/3;
剩下的工作就是把灰度数据再放回到画布的绘图环境中，并返回原始的图像数据作为新灰度 图片的源。
ctx•putlmageData(c, 0， 0, 0, 0, c.width, 〇•height); return canvas•toDatal)RL();
这样，即使我们只提供彩色版图片，也可以在该图像的彩色版与灰度版之间切换了。
为什么使用<canvas>而不是多张图片呢？只有在基于用户操作实现交互时，使用<canvas>的优 势才会显现出来。以前，要想在浏览器中实现高级的图片交互功能，只能依靠Flash或Silverlight 这样的插件。今天，有了<canvas>，就可以在浏览器窗口绘制任何对象、任何像素了。当然，还 能通过它来操作图像，或者创建令人眼花缭乱的界面元素。可是，就跟使用Flash—样，也绝对 不能滥ffl<canvas>。换句话说，即使你真的可以在一个<ca_s>元素里创建一个站点，也不表示你 应该那样做。’
此外，你还得考虑到那些使用屏幕阅读器或其他辅助浏览技术的用户。HTML5的这个 <canvas>元素跟Flash—样，都不具备可访问性，会给那些用户带来同样的烦恼。记住，不要被 先进技术的光环左右了你的心智，必要时还要留一手。

11.3.2音频和视频
11.3 几个示例	209
谈到HTML5的新元素，人们议论最多的恐怕就要数〜1(^〇>和它的亲兄弟<311(11〇>了。这两个 元素让HTML具有了原生视频和音频的能力，但也带来了一些不好处理的问题。
在HTML5之前，向网页中嵌入视频需要用到一大堆重复的<〇bject^P<embed>元素，其中一 些在HTML4中甚至都无法通过有效性验证。<object>可以引用各种影片播放器，例如QuickTime、 RealPlayer或Flash，并使用这些插件在浏览器中播放影片。举个例子，以下就是嵌入Flash影片 的代码（想必你一定觉得很眼熟）：
<objectclassid="clsid:d27cdb6e-ae6d，llcf_96b8-
44455354000011 width=ff100!, height=n100,f	.	,,
codebase="http://fpdownload•a3obe.com/pub/shockwave/cabs/flash/swflash•cab#version=9,〇,〇,〇_r> <param name=nmovieM value="moviename，swf">	•
<param name=f,playf, value="true">
<param name=MloopM value=ntruen>
<param nafne="quality’丨 value="high">
〈embed sro"movienanie,swf" widtK="lOOM height="l00" play="true" loop="true" quality="highn pluginspage=__ http: //get • adobe• com/flashplayer,f />
</object>
除了这些代码之外，第三方插件也有各自的问题和局限性。要想让嵌入的代码发挥作用，浏 览器中必须安装相应的插件，而且版本还要合适。插件是在一个封闭的环境中运行的，通过脚本 无法修改或者操作视频内容。如果插件没有提供API,插件运行环境无异于文档中的一个独立王 国。
HTML5的<v1deo>元素为在文档中嵌入影片以及与影片交互定义了一种标准方式，同时也把 嵌入操作简化成了一个标签：
〈video src=,,movie.mp41l>
<!--不支持原生视频时的替代内容-_>
<a href=,lmovie^mp4,r>Download movie^mp4</a>
</video>
'这里我们嵌入了一段mp4视频，并给出了浏览器不支持<v1deo>时的替代下载链接。
类似地，<aud1o>元素的用法也差不多：
<audio src=__sound*ogg">
<! - _不支持音频时的替代内容-->
<a href=,,sound^ogg,,>Download sound^ogg</a>
</audio>
简单、朴素，还很吸引人，是吗？除非它总能如此……
1.也有混乱的时候
让人失望的是，HTML5的<〃1由〇>和<31^1〇>元素也有那么点小问题。这两个标签都很简单， 也都有相应的属性用于显示播放控件或更改播放设置，但是它并未说明支持哪些视频格式。
要搞清楚有关视频格式的问题，必须从什么是视频说起。
像mov1e.rnp4这样的视频，其实是一个包含很多东西的容器。扩展名mp4表示视频是使用基 于苹果QuickTime技术的MPEG4打包而成的。这个容器规定了不同的音频和视频轨道在文件中 的位置，以及其他与回放相关的特性。其他容器还有m4v (另一个MPEG4扩展名)、avi (Audio

210 第 11 章 HTML5
Video Interleave，音频视频交错）、flv (Flash Video)，等等。
在每个影片容器中，音频和视频轨道都使用不同的编解码器来编码。编解码器决定了浏览器 在播放时应该如何解码音频和视频。编解码器的核心就是一个算法，用于压缩和存储视频，以减 少原始文件的大小，同时可能会也可能不会损失品质。视频编解码器也有很多种，其中有代表性 的有三个：H.264、Theom和VP8。同样，音频文件也有相应的编解码器，常见的有mp3 (MPEG-1 Audio Layer 3)、aac (Advanced Audio Coding)矛口 ogg (OggVorbis)。
注意H.264编解码器存在一个非技术问题，即使用许可。使用H.264的解码器和编码器都要付 费，分发经编码许可制作的H.264内容不用付费，但要对其解码则必须得到许可。换句 话说，在你自己的网站上发布H.262影片不用交钱，但需要对其解码的浏览器开发商以 及开发解码软件的软件开发商都要得到许可才行。为了解决视频格式的许可问题>，谷歌 把VP8编解码器（在WebM容器中）的专利权发布到了公共域，并承诺永不收回>。他们 的愿望是让浏览器开发商在实现WebM/VP8/Vorbis时不受许可限制，并向所有人提供一 种公共的格式。
这些不同的容器格式以及编解码器给我们带来了什么问题呢？问题就是没有一款浏览器支 持所有容器和编解码器，因此我们必须提供多种后备格式。Firefox的某些版本、Chrome以及Opera 支持 Theora/Vorbis/Ogg，IE9、Safari、Chrome、Mobile Safari 以及 Android 支持 H.264/ACC/MP4, 而 IE9、Firefox、Chrome 还有 Opera 支持 WebM (VP8 和 Vorbis 的另一种容器格式)。
如此混乱的结果意味着没有哪些格式可以跨浏览器。但愿这个问题在不久的将来能够解决， 否则视频这一块会让整个HTML5黯然失色。眼下看来，为了保证每个人都能看到视频，必须制 作多种格式的视频并在々1(^〇>元素中包含多个来源：
碡
<video id=,finovie,f preload controls〉
<source src=nmovie^nip4M />
〈source src=" movie•webmM type?video/webm; codecs=nvp8, vorbis"1 />
<source src=,tmovie^ogvt, type=*video/ogg; codecs=Mtheora, vorbis111 />
<p>Download movie as	•
<a href="movie.mp4">MP4</a>,
<a href="movie.webmn>WebM</a>, or <a href=,,movie*ogvl,>Ogg</a>x/p>
</video>
为了确保HTML5的最大兼容性，至少要包含下列三个版本：
□基于H.264和AAC的MP4
□ WebM (VP8+Vorbis)
□基于Theora视频和Vorbis音频的Ogg文件
这个例子中没有给出可替代的插件版。为了确保最大程度地兼容那些不支持HTML5的浏览 器，一般还应该准备一个Flash或QuickTime插件版视频。但在这里，为鼓励用户升级到较为先 进的浏览器，我提供了直接下载不同格式文件的链接。

11.3 几个示例 211
■——^门一-■n~-^T-rrrrr^~-~rt-TtTr-rr^^rrt~rr^^-^TnTr^rrT>rniiiiii>ir>iCi：f〇*〇-〇Mt>^in mro'inmw'ij-Miiw l l l•l_l^■•^ltntm-^•靡^_:w■••l|||JmTnnl^〔Tlm••.n“l:^:•”：~~^:	---------……,	:.‘-rT-.rr-rr.ri		-	—									
注意不同的视频格式的排列次序也是一个问题。把MP4放在第一位，是为了让保证iPad、 iPhone及iPod Touch等运行iOS的设备能够顺利读取视频。因为iOS 4之前版本中的 Mobile Safari只能解析一个<^彳(^〇>元素，故而把针对iOS的格式放在了最前面。
总之，这些问题让HTML5视频和音频变得有点乱，一定程度上影响了它的吸引力。想想要 制作同一视频的多个版本，并且要保存三个甚至更多个文件，有人不禁会问：既然最后还是要提 供Flash版本，那为什么不直接就提供一个Flash影片算了？答案是向前兼容，提供较新的<video> 元素，可以在支持HTML5的浏览器中对视频内容进行更多控制。
对HTML5视频，可以（或将来可以）应用CSS属性以修改视频的外观、大小及形状，可以 添加字幕和歌词等信息，还可以组合视频和画布来覆盖内容。甚至可以把视频插入到<〇3_5>对 象中，像前面处理灰度图片一样，通过分析图像来检测视频运动。
下面通过一个例子来说明<v1deo>元素的API,看看怎样定制视频控件，怎样创建简单的播放
按钮。
2.自定义控件
浏览器在显示<v1deo>元素时，会为其添加一些与浏览器样式统一的标准播放控件。要想自定
义这些控件的外观，或者添加新的控件，可以通过一些DOM属性来实现，主要包括：
currentTIme，返回当前播放的位置，以秒表示；
duration,返回媒体的总时长，以秒表示，对于流媒体返回无穷大；
paused，表示媒体是否处于暂停状态。
此外，还有一些与特定媒体相关的事件，可以用来触发你的脚本。主要事件有：
play，在媒体播放开始时发生；
pause,在媒体暂停时发生；
p loadeddata，在媒体可以从当前播放位置开始播放时发生；
ended,在媒体已播放完成而停止时发生。
使用这些及其他属性和事件，可以轻松地创建自定义的视频控件，实现对视频的各种控制。
从暂停和播放按钮到滑动条（进度条），都没有问题。
不管创建什么控件，都别忘了在<v1deo>元素中
添加control属性：
<video src=,,movie^ogvu control〉
这行代码会呈现出一个类似Chrome浏览器中
所示的常见的播放控制界面，如图11-2所示，但其
中的控件可以通过脚本来移走。
下面就运用我们掌握的DOM脚本技能，来创
建一些简单的视频控件。



〇〇；11 4>)
图 11-2

212 第 11 章 HTML5
注意读者如果需要示例文件，可以从

http://www.friendsofed.com/中本书页面下载源代码。
第一步先创建一个简单的HTML页面，命名为mov1e.html。在其中添加一f<v1deo>元素，并 按照前面的介绍指定多种视频格式。此外，页面中还要包含player.css样式表和player.js脚本:
<!D0CTYPE html>
<html lang="en">
<head>
<meta charset=Hutf-8H />
<title>My Video</title>
<link rel=flstylesheet11 hre干="styles/playencss” />
</head>
<body>
<div class=Mvideo-wrapperH>
<video id="movie_’ controls〉	^
<source src="movie』p4’r />	、
〈source sro1’ movie.webm!,
type=fvideo/webm; codecs=nvp8, vorbisf, 1 />
<source src="movie*ogv" type=fvideo/ogg; codecs=Mtheora> vorbis111 />
<p>Download movie as
<a href=nmovie.mp4">MP4</a>,	-
<a href=l?inovie^webmn>WebM</a>> or <a href=Mmovie.ogv,f>Ogg</a>.</p>
</video>
</div>
〈script src=Mscripts/player^jslfx/script>
</body>
</html>
在player.js文件中，我们要修改页面中的所有<\rideo>元素，删除其内置控件并添加自定义 的Play按钮。把下面两个完整的函数添加到player, js文件中：
function createVideoControls() { var vids = document*getElementsByTagName(1video1); for (var i = 0 ; i < vids•length ; i++) { addControls( vids[i]);
function addControls( vid ) {
vidtremoveAttribute('controls1);
vid•height = vid.videoHeight; vid•width = vid^videoWidth;
vid•parentNode•style•height = vid.videoHeight + ’px'; vid.parentNode^style•width = vid♦videoWidth + 'px1;
var controls = document•createElement(!divf); controls•setAttribute(1 class1,1 controls1);
var play = document•createElement(1 button1); play^setAttribute(rtitlef,1Playr); play.innerHTML = f&#x25BA;1;
controls•appendChild(play);

11.3 几个示例 213
vid.parentNode.insertBefore(control$, vid);
play.onclick = function () { if (vid.ended) { vid^currentTime = 0;
}
if (vid.paused) { vid^play();
} else { vid，pause();
>
};
vid*addEventListener(fplayf^ function () { play^innerHTML = r&#x259〇；&#x259〇；!； play•setAttribute(1 paused1, true);
}, false);
vid.addEventListener('pause1, function () { play•removeAttribute(,paused1); play^innerHTML = ,&#x25BA;f;
}, false);
vicLaddEventListener(‘ended、function () { vid^pause();
}, false);
windowtonload = function() {	，
createVideoControls();
}
脚本文件player, js中的这两个函数准备完成很多任务。首先，找到页面中的video元素， 然后对它们分别应用addControls函数：
function createVideoControls() { var videos = document.getElementsByTagName('video1); for (var i • 0 ; i < videos•length ; i++) { addControls( videos[i]);
在addControls函数中，我们删除了 video元素原来的controls属性，从而去掉其内置的控件， 接着又创建了几个DOM对象，用来充当Play/Pause按钮，并把它们都添加为video元素的子元素。
function addControls( vid ) {
vid♦removeAttribute(1 controls1);
vid•height = vid^videoHeight; vid^width = vid.videoWidth;
vid.parentNode•style•height = vid.videoHeight + fpxf; vid.parentNode^style,width = vid•videoWidth + !pxf;
var controls = document.createElement(fdiv1); controls•setAttribute(1 class1,1 controls1);
var play = document♦createElement(1 button1); play.setAttribute('title1,"Play1); play.innerHTML = ’&#x25BA;’；
11

214 第 11 章 HTML5
controls♦appendChild(play);
vid•parentNode.insertBefore(controls, vid);
接下来，给Play按钮添加一个click事件，以便单击它播放影片：
play^onclick = function () { if (vid^ended) { vid^currentTime = 0;
if (vicLpaused) {
vid.play();
} else { vid*pause();
};}
最后，利用play、pause和ended事件来修改Play按钮的状态，并在影片未暂停的情况下显 示Pause按钮。	〃
vid•addEventListener(1 play1, function () { play^innerHTML = f&#x259〇；&#x259〇；1； play^setAttributeC'paused1^ true);
}, false);
vid^addEventListener('pause1, function () { play.removeAttribute('paused1)j play^innerHTML = !8t#x25BA;f;
}, false);
vid•addEventListener(?ended1} function () { vicLpause();
}> false);
注意恐怕有读者注意到了，这里使用的是addEventListener方法为视频添加事件。 addEventLIstene「是为对象添加事件处理函数的规范方法。之前我们使用oncllck之类的 HTML-DOM的on前缀属性，是因为ffi (IE8及以前版本）使用的是一个不同的attachEvent 方法。而到了 IE9,它支持<v1deo>，也是完成本章示例必需的，也开始支持规范的addEvent- Llstener方法了。因此，在本章的例子中使用该方法是没有问题的。
为了给控件添加样式，需要在playe「.css中添加下列CSS样式。可以使用CSS对控件外观 随心所欲地更改：
•video-wrapper { overflow: hidden;
}
•video-wrapper .controls { position: absolute; ieight：3〇px;	、
width：3〇px;	•
margin: auto;
background: rgba(0,0,0,0*5);

11.3 几个示例 215
•video-wrapper button { display: block;
•width: 100%; height: 100%; border: 0; cursor: pointer; font-size: l7px; color: #fff;
background: transparent;
.video-wrapper buttonfpaused] {
干ont-size: l2px;
>
页面加载完成后，window.load事件就会执行createVIdeoContmls函数，结果就会得到一个相 对粗糙的视频控制界面，可以用来播放和暂时视频，如图11_3所示。



图 11-3
这个简单的例子只包含最基本的控件，在此基础上，还可以利用相应的属性和事件添加带位 置指示器的滑动条、时间戳，以及其他特殊的控件。到底添加哪个控件，完全由你说了算。建议 大家抽空学习一下HTML5视频规范中其他与视频相关的属性，地址为

http://www.whatwg.org/ specs/web_apps/ciment-worlJmultipage/video.html#video〇 另夕卜，也可以访问 

http://www.w3.org/2010/ 05/video/mediaevents.html，看看其中给出的一些实例。最后，给大家推荐一本书，女博士 Silvia Pfeiffer 撰写的 TTze	GwzWe to作和〇 (Apress，2011)，看看使用<v1 de〇>元素还能做
哪些事。
11.3.3表单
我们要介绍的最后一个HTML5元素就是表单。表单的身影几乎可以在任何一个网页中的看 到，但在HTML5之前，可用的输入控件类型却少得可怜。文本框、单选按钮、复选框对于简单



216 第 11 章 HTML5
的表单是够用了，但在需要更多交互功能的时候，仍然免不了求诸DOM脚本披挂上阵。如果想 让用户更方便地在表单中输入日期，就得自己构建界面和必要的JavaScript。老天有眼，HTML5 给我们带来了很多新表单元素、新输入控件类型和新的属性，帮我们实现了这些功能。不过，跟 以往一样，你的DOM编程才能还是可以派上用场的。
新的输入控件类型包括：
email，用于输入电子邮件地址；
url，用于输入URL;
date，用于输入日期和时间；
number，用于输入数值；
range，用于生成滑动条；
search,用于搜索框；
口 tel，用于输入电话号码；	_	L
col 0「，用于选择颜色。
这些新类型比单纯的type=”text"好用多了。浏览器知道这些控件都接受什么类型的输入，因 此可以为它们配备不同的输入控件，例如在移动设备上更换不同的软键盘。图11-4中两幅图是 iPhone中Mobile Safari的界面，一幅是针对文本输入框的键盘，一幅是针对电子邮件地址的键盘。



Text： nr
Email: f
Text:「
Email: ff






相应地，新的属性包括如下这些。
11-4

11.3 几个示例	217
autocomplete，用于为文本（text)输入框添加一组建议的输入项；
;□ autofbcus，用于让表单元素自动获得焦点；
'□ form,用于对<fom>标签外部的表单元素分组；
|	□ mln、max和step,用在范围（range)和数值（number)输入框中；
i □ pattern，用于定义一个正则表达式，以便验证输入的值；
|	□ placeholder，用于在文本输入框中显示临时性的提示信息；
required,表示必填。
这些属性把很多原来由DOM脚本负责的任务都转移给了浏览器，例如提供自动完成的建议 项和验证表单输入。但我们要关注的问题，是在浏览器不支持新的类型和属性时怎么办。
；	当然，现在就可以使用这些新增的输入控件，因为它们都向后兼容（某种程度上如此)。对
s于HTML5的电子邮件输入框而言：
<input type=”email11 />
旧浏览器会将该类型默认为text，并呈现出标准的文本输入框。对于email或search类型的 输入框来说，这不会造成什么大问题，但对于range滑动条就不行了。想象一下，原本应该是滑 动条，但现在却是一个输入框，比如Safari和IE显示的range控件，如图11-5所示。



Safari	internet
图 11-5
为了应对不兼容的浏览器，必须使用特性检测来准备另一个方案。
使用本章前面提到的Modemizr库，就可以进行兼容性检查。比如，要检査浏览器是否支持 某个输X类型的控件，可以使用"inputtypes.type属性：
If ( !Modernizr.inputtypes t date
//生成日期选择器的脚本
> {
而要检査某个属性，则可以使用Input.attribute属性:
if ( !Modernizr.input.placeholder ){
}	生成占位符提示信息的脚本
要是没有使用Modemizr，可以使用下面这个InputSupportsType函数来检查浏览器是否支持 某种类型的输入控件：
干unction inputSupportsType(type) { if (!document•createElement) return false; var input 二 document•createElement(finput1); input •setAttributeC type、type); if (input.type == 'text1 && type != 'text1) { return false;
} else {
i

218 第 11 章 HTML5
return true;
>
>
使用InputSupportsType函数的方式与使用Modemizr—样：
If ( linputSupportsTypeC^ate1) ) {
//生成日期选择器的脚本
}
要检査特定的属性，可以使用下面这个elementSupportsAttribute函数:
function elementSupportsAttribute(elementName> attribute) { if (Idocument^createElement) return false; var temp = document•createElement(elementName); return ( attribute in test );
使用elementSupportsAttribute函数的方法还是男酵，只不过需要传入元素名和要检査的属性名:
if ( !elementSupportsAttribute( 1 input1, 'placeholder1 ) ){	、
//生成占位符提示信息的脚本
}
在稳妥的特性检査的基础上，就可以一方面试用新的HTML5表单元素，另一方面提供备用 的DOM脚本，以便浏览器不支持某种类型或属性时“挺身而出”。
举个例子，假设你想在自己的文本输入框中加入占位符信息。在HTML5中，只要像下面这 样使用placeholder就行了：
〈input type="text" id="first-name’’ placeholder=!,Your First Name" />
在Safari或Chrome浏览器中，占位符会在用户尚未输入值 的情况下显示指定的临时文本，如图11-6所示。
| Ymtr Rrst Ha 賺



要在不支持placeholder属性的浏览器中实现相同的效果，
%
就得编写一个简单的DOM脚本来完成同样的功能：
if ( !Modernizr•input•placeholder ) {
var input = document.getElementByl^'first-name')
input•onfocus = function () {
var text = this•placeholder 丨| this•getAttribute(1 placeholder1);
if ( this•value == text ) {
//重置输入框的值，以隐藏临时的占位符文本
this.value = 11;
input^onblur = function () {
if ( this•value == 11 ) {
//把输入框的值设置为占位符文本
this.value = this.placeholder || this^getAttribute(,placeholder1);
//在onblur处理函数运行时中添加占位符文本 input.onblur();
图 11-6
当然，这个替代方案的主要问题是必须依赖于JavaScript实现同样的功能。因此，还必须考 虑到在JavaScript不可用的情况下选择什么输入控件最合适。
要作为后备的高级功能（如自动完成和滑动条）越多，开发工作量就越大，占用时间就越多。

11.5 小结 219
所以还建议大家选择已有的一些帮我们完成了相应功能的库。要了解有关JavaScript库的相关内 容，请参考本书附录。
11.4	HTML5还有其他特性吗
有丨本章前面介绍的这几个标签和属性只是HTML5的冰山一角而已。请读者注意，HTML5 这个规范至今仍然没有尘埃落定，很多地方都有可能发生变化。在浏览器支持不是特别完善的情 况下，全面转入HTML5还为时过早，但这不会影响我们继续探索的兴致。比如，HTML JavaScript API可是我们大家期望已久的了。等不了多长时间，我们就可以享受HTML5的诸多便捷功能了。 口使用localStorage和sessionStorage在客户端存储大型和复杂数据集的更有效方案 (

http://dev.w3 .org/html5/webstorage)；
□使用WebSocket与服务器端脚本进行开放的双向通信（

http://dev.w3.oig/html5/websockets/); □使用 Web Worker 在后台执行 JavaScript (

http://ww.whatwg.org/specs/web-workers/current-woik/); 口标准化的拖放实现（

http://www.whatwg.org/specs/web-apps/current-work/multipage/dnd. html#dnd)；
□在浏览器中实现地理位置服务（

http://www.w3.org/TR7geolocation-API/)。
这些新功能并不都与D0M相关，但它们却是你应该了解和掌握并在不久的将来每天都会使 用的，所以最好提前多花些时间熟悉它们。
要了解更多相关内容和示例，请参考以下资源。
W3C HTML5 Working Draft: 

http://www.w3.org/TR/html5;
WHATWGHTML5 (包含开发中的下一代技术）：

http://www.whatwg.org/specs/web-apps/ current-work；
HTML5 的交互性演示：

http://html5demos.com/;
□&HTML5 相关的 PPT、代码、示例及教程：

http://www.html5rocks.com/;
D/vd欣>//:厂规5，作者 Mark Pilgrim: 

http://diveintohtml5.org/;
11.5小结
本章，我们了解了 HTML5以及使用Modemizr等工具检测特性的重要性。同时也编写了几 个例子，介绍如何使用特性检测来确保为新的HTML5特性提供后备功能。本章介绍的HTML5 的新特性包括：
□可以用来在文档中绘制矢量及位图的<canvas>元素；
□可以免插件而直接在网页中嵌入音频和视频的<audio^P<video>元素；
□可以为你提供更广泛选择的新的表单控件类型以及新的属性。
到目前为止，我们掌握的D0M脚本编程技能都处于各自为战的状态。下一章，我们就把前 面学到的所有概念和技术综合起来，创建一个项目。
到了融会贯通学以致用的时候了。

前面我们看到过很多DOM脚本编程的例子，但那些为了说明问题而设计的例子之间都没有 什么联系。本章我们就来做一个综合的项目，把所有与DOM脚本编程相关的技术学以致用。具 体来说，我们会从头开始做一个网站，然后再用JavaScript来为这个网站增加交互功能。
12_1项目简介
有一件美差落在了你的头上!作为一名Web设计师，你被选中为世界最著名的乐队Jay Skript and the Domsters 设计一个网站。	，
噢，没听说过个乐队？不要紧，我们一起来编个故事。就当你配合我把这章写完吧，假装有 那么一个国际知名乐队，而你恰好有幸被选中，要承担起为这个乐队设计网站的任务。
这个网站必须跟这个乐队一样，得酷。要是你能再给网页加上一些交互特性，那就酷毙了。 但是别忘了，这个网站还必须对残疾用户以及搜索引擎保持友好。
开办这个网站的主要目的就是发布有关乐队的信息。无论怎么构思这个网站，首先都得确保 这些信息能让访客一目了然。下面我们就来看看都要做些什么。
12.1.1原始资料
客户已经提交了构建网站所需的东西：有关乐队的介绍材料、巡演日程，还有一些照片。这 个网站不需要太多的页面，它本质上就是一个宣传手册，而这一点也正是你要把握的核心用户体验。
12.1.2站点结构
,根据客户提供的资料，可以画出一张简单的站点地图。站点的结构的确不算复杂，至少可以 把所有页面都放在一个文件夹里。

12.1 项目简介 221
为了准备站点的制作，创建三个文件夹，一个叫Images，保存要用的图片；一个叫styles， 保存CSS文件；一个叫scripts，保存JavaScript文件。
站点文件夹的目录结构如下所示：
/images
口 /styles	、
/scripts
说到页面，首先得有一个详细介绍乐队背景信息的页面。其次要有一个类似相册的放照片的 页面。巡演日程安排当然也要单独一个页面。为了让歌迷与乐队沟通，还必须有一个联系页面。 最后，当然要有一个主页，放上乐队简介和站点导航信息。以下是要创建的几个页面（如图12-1
所示）：
Home
About
Photos
Live
Contact
Home	About	Photos	Live	Contact
图 12-1
这几个页面对应如下文件：•
index.html
about.html
photos.html
live.html
contact.html
虽然每个页面的内容不一样，但它们都要使用相同的基本结构。下面该考虑为这些页面创建 一个模板了。