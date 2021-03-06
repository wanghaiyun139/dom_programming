# JavaScript Dom编程艺术

- [第12章 综合示例](chapter12.md)
  - [12.1 项目简介](chapter12.md#121)
    - [12.11 原始资料](chapter12.md#1211)
    - [12.12 站点结构](chapter12.md#1212)
    - [12.13 页面结构](chapter12.md#1213)
  - [12.2 设计](chapter12.md#122)
  - [12.3 CSS](chapter12.md#123)
    - [12.31 颜色](chapter12.md#1231)
    - [12.32 布局](chapter12.md#1232)
    - [12.33 版式](chapter12.md#1233)
  - [12.4 标记](chapter12.md#124)
  - [12.5 JavaScript](chapter12.md#125)
    - [12.51 页面突出显示](chapter12.md#1251)
    - [12.52 JavaScript幻灯片](chapter12.md#1252)
    - [12.53 内部导航](chapter12.md#1253)
    - [12.54 JavaScript图片库](chapter12.md#1254)
    - [12.55 增强表格](chapter12.md#1255)
    - [12.56 增强表单](chapter12.md#1256)
    - [12.57 压缩代码](chapter12.md#1257)
  - [12.6 小结](chapter12.md#126)  


12.1.3页面结构
站点的每个页面都要分成几个区域。
□头部区域包含站点的品牌性信息，也是放Logo的地方。这个区域要使用<header>元素。 □导航区域中包含一组链接，指向各个页面。这个区域使用<隨> 元素。

222 第12章综合示例
□内容区域包含每一页的实质性内容，这个区域使用<3「1：1^>元素。
因为要使用HTML5元素，所以也要在文档的<head>元素中包含Modemizr库（第11章介绍 过)。可以从

http://modemizr.com/下载这个库的最新版本（撰写本章时的最新版本为1.6)，并将 其放到scripts文件夹中。
最后，模板的代码没有多长。
<!DOCTYPE html>
<html lang=rfenM>
<head>
<meta charset=,futf-8n />
<title>3ay Skript and the Domsters</title>
<script src=,lscripts/modernizr-i^6^min.jsf,x/script> </head>
<body>
<header>
<nav>
<ul>
<lixa href=,findex.htmlM>Home</ax/li>
<lixa href=,fabout*htmlM>About</ax/li>
<lixa href=lfphotos^htmlM>Photos</ax/li> <lixa href=nlive^htmlu>Live</a></li>
<lixa href =ncontact.html,f>Contact</ax/li> </ul>
</nav>
</header>
<article>
</article>
</body>
</html>
把这些代码保存在template.html文件中。
在设计好页面结构后，下面就要一页一页地插入内容了。不过，让我们先来设想一下站点完 工后的外观。
12.2设计
既然知道了每个页面中都包含哪_结构化元素，而且手里也已经有了客户提供的资料，那么 接下来的外观设计就不难做了。你可^选择Photoshop、Fireworks或任何其他的图形设计工具， 做出你认为适合的任何风格的设计方案（如图12-2所示)。用一位著名厨师的话说，“以下是我 早就为您准备好的。”
做完了视觉设计之后，可以把平面设计切分成多个图片。把背景图片保存为backgromd.gif。 而品牌图像保存为logo.gif。而带有一点渐变的导航条要命名为navbar.gif。最后把人物剪影保 存为gu1tar1st.gif。把这些图片都到1_es文件夹中。
注意如果你不是设计高手，还是建议你从Friend of ED网站（

http://www.friendsofed.com/)的 本书页面中下载本章用到的图像。

123 CSS 223

{ay Skitpt And the
v^*^r»iWi**wepweWi^WlVN»Hw^MiW
命嗲<蘑馨受聲
fay S&riripf
and the
BOMStmUS
图 12-2
12.3 CSS
现在，你有了基本的HTML模板，也知道自己的站点长什么样了。通过为模板应用CSS， 可以在Web上再现你的设计方案。
如果把所有CSS都放到一个文件中，可能会为后期维护带来一些麻烦。而把所有CSS分别 放在几个文件中则是个好主意。
怎样组件CSS由你决定，但我建议用其中一个保存与整体布局有关的样式，用另一个作为 专门的颜色样式表，而用第三个来保存与版式有关的样式：
口 layout.css
color.css
typography.css
这些样式表都可以导入到一个基本的样式表中：
@import url(layouttcss);
@import url(color.css);
^import url(typography•〇$$);
把包含这三行代码的文件保存为basic.css，并放在styles文件夹中。如果你想添加一个新 样式表或者删除一个样式，只要编辑baslc.css即可。
可以在模板的<head>元素中通过<1被> 元素引入这个基本样式表。然后，再在页面<header> 中添加一个<彳呵>标签，指向logo图片。此时也可以向<3「1：彳(：_^>中添加一些临时性填充文本。
<!D0CTYPE html>
<html lang="en">
<head>
<meta charset=nutf-8n />
<title>Jay Skript and the Domsters</title>
<$cript src=nscripts/modernizr-l.6.min.jsux/script>
clink rel=’’stylesheet" media=’’screen" href=nstyles/basic^css,f />



224 第12章综合示例
</head>
<body>
<header>
<img src=nimages/logo^gifM alt=n3ay Skript and the Domstersn /> <nav>
<ul>
<lixa href=t!index^htmln>Home</ax/li>
<lixa href=l,about^htmln>About</ax/li>
<lixa href=nphotos^htmlH>Photos</ax/li>
<lixa href=Hlive.htmlll>Live</ax/li>
<lixa hrefcontact•htmlM>Contact</ax/li>
</ul>
</nav>
</header>
<article>
<hl>Lorem Ipsum Dolor</hl>
<p>Lorem ipsum dolor sit amet, consectetuer adipiscing eli七 Nullam iaculis vestibulum turpis^ Pellentesque mattis rutrum nibh^ Ouisque orci, euismod sit amet, sollicitudin et, ullamcorper at, lorenu	^
Pellentesque habitant morbi tristique senectus et netus et malesuadd fames ac turpis egestas.
Ut lectus. Mauris eu sapien non enim dapibus imperdiet.
Sed eu mauris sed pede mollis commodo*
Fusee eget est^ Sed ullamcorper enim nec est^
Cras dui 千elis, porta vitae, faucibus laoreet^ sollicitudin eget, enirru Nulla auctor^ Fusee interdum diam ac eros^
Mauris egestas. Fusee in elit et sem aliquet pretium.
Donee nunc erat, sodales ac, facilisis a, molestie eu, massa.
Aenean nec justo eu neque malesuada aliquetx/p>
</article>
</body>
</html>
这样，基本的模板就算完工了，如图12-3所示。

♦ ✓ ^ y a Mr *
■■■■
.and the
momsTmms
_	卞	V«v_

.€^* ©之
•.您’乂…

I^orera Ipsum
Qut^tiean

玠lplici 玪it milis	'Mkmsiq&i i
le orw fflBwncd «ma45rMlprtr<?in et	TrtvW
♦ ♦ ♦	鲁	一	^ * (^	w ^	^	s
.jdiAtiHmyfdpl



狐 Ui	册邱 h 廳磁	Sell 如脚也 iidJ
m紱你政你}你齡肩败抬扣胡erutm铎麻iwtiitm f mn仗糊紀
mlHi mm^K	e»t Sad tik
VttilA moot.	Oitm 2c enn.
ac, », KUf Acmn mu m
图 12-3

12.3 CSS 225
12.3.1颜色
样式表color.css是最直观的。记住，不管为哪个元素应用什么颜色，都要同时给它一个背 景色。否则，就有可能导致意外，看不到某些文本。
body {
color: #fb5； background-color: #334；
}
a:link { color: #445； background-color: #eb6;
>
a:visited { color: #345； background-color: #eb6;
}
a:hover { color: #667； background-color: #fb5;
}
a:active { color: #778; background-color: #ec8;
}
header { color: #ec8; background-color: #334； border-color: #667；
>
header nav { color: #455； background-color: #789； border-color: #667；
}
article { color: #223； background-color: #edc; border-color: #667；
header nav ul { border-color: #99a;
>
header nav a:link,header nav a:visited { color: #eef;
background-color: transparent; border-color: #99a;
>
header nav a:hover { color: #445； background-color: #eb6;
>
header nav a:active { color: #667； background-color: #ec8;
}
article img { border-color: #ba9; outline-color: #dcb:
#imagegallery a {

226 第12章综合示例
background-color: transparent;
此时的模板已经有了色彩了，如图12-4所示。
夏兹分Skripf
and file
mmMSTmms



12.3.2布局
基本的布局还是相当简单的，所有内容都在一栏中。
为了让导航中的链接水平排列，需要应用一些浮动效果。除此之外，layont.css也没有什么 不好理解的了。
首先是为HTML5块元素定义默认的样式。主要针对那些不支持它们的浏览器，好让这些元 素都能够具有适当的块布局。
其次，使用通配选择器把所有元素的内外边距设置为零。这样就把不同浏览器为元素设置的 不同内外边距全都删除了。重设这些值之后，所有样式就可以一视同仁了。
section, header, article, nav { display: block;
padding: 0; margin: 〇;
>
body {
margin: lem 10%;
background-image: url("/images/backgrounchgi干)； background-attachment: fixed; background-position: top left;

background-repeat: repeat-x; max-width: 8〇em;
>
header {
background-image: url(*♦/images/guitarist^gif);
background-repeat: no-repeat;
background-position: bottom right;
border-width: •lem;
border-style: solid;
border-bottom-width: o；
>
header nav {
background-image: url("/images/header navbar^gif);
background-position: bottom left;
background-repeat: repeat-x;
border-width: •lem;
border-style: solid;
border-bottom-width: 〇;
border-top-width: 0;
padding-left: 10%;
}
header nav ul { width: 100%; overflow: hidden; border-left-width: .lem; border-left-style: solid;
>
header nav li { display: inline;
}
header nav li a { display: block; float: left;
)adding: •Sem 2em;
5〇rder-right: .lem solid;
}
article {
border-width: •lem; border-style: solid;
.border-top-width: 0;	^
f padding: 2em 10%; line-height: l^8em;
>
article img { border-width: •lem; border-style: solid; outline-width: .lem; outline-style: solid;
这样，我们就通过CSS定义了颜色和布局，如图12-5所示。

228	第12章综合示例



图 12-5
12_3.3版式
有时候，的确很难分清某些样式声明放到哪个文件里更合适。字体和大小很显然应该放在 typography.css里，但外边距和内边距呢？很难说它们到底应该与布局有关，还是与版式有关。 在我们这个例子中，把内边距信息都放在了 layout.css中定义（上一节已经定义了），而外边距 信息则会放在typography.css中。
body {
font-size: 76%;
font-family: ”Helvetica","Arial",sans-serif;
}
body * {	r
千oni>size: lem:
aN
font-weight: bold; text-decoration: none;
>
header nav
font-famiiy: "Lucida Grande"厂Helvetica",Mrial",sans-serif
}
header nav a { text-decoration: none; font-weight: bold;
}
article {
line-height: l^8em;
}
article p {

12.4 标记 229
margin: lem 0；
}
hi {
font-family: "Georgian,"Times New Roman11,sans-serif; font: 2^4em normal;
}
h2 {
font-family: "Georgia'"Times New Roman’、sans-serif; font: l.8em normal; margin-top: lem;
}
h3 {
font-family: ’’Georgia",Times New Roman11,sans-serif; font: l*4em normal; margin-top: lem;
}
#imagegallery li { list-style-type: none;
}
textarea {
font-family: "Helvetica'’’Arial”,sans-serifj
>
现在，模板不仅有了颜色、布局，还具有了版式，如图12-6所示。



图 12-6
以上三个 CSS 文件（color.css、layout.css 和 typography.css)都和 basic.css 样式表一块， 放在styles文件夹中。
124标记
模板做完了，样式也都写得差不多了。接下来该考虑站点中的每个页面了。

230 第12章综合示例
首先从主页1ndex.html开始，这个页面包含一段介绍性文字，放在<article>元素中:
<p id="intro">
Welcome to the official website of Day Skript and the Domsters^
Here, you can <a href^^about^html11 title=_’Aboutu>learn more about the band</a>,
view <a href=nphotos.htmln title=lfPhotosM>photos of the band</a>,
find out about <a href=f,live.html11 title=HTour Date,f>tour dates</a>
and <a href=,fcontact•html11 titles11 Contact11 >get in touch with the band</a>.
</p>
这样，主页就完成了，如图12-7所示。



图 12-7
这段文字有一个id，叫"intro"。我们要利用这个Id为这段介绍添加特殊的样式。此外，还 可以利用这个Id来添加一些DOM脚本。
12.5 JavaScript
在编写DOM脚本之前，必须先确定怎么组织JavaScript文件。如果站点需要很多长长的脚 本，那最好把它分割成几个小文件，正如本书前面展示的那样。可是，眼下这个网站非常简单， 所需的JavaScript代码也不长。为了减少请求的数量，我们就把所有脚本都放在一个叫global, js
的文件里。这样也有助于最后缩减其代码。
先在scripts文件夹中创建global .js。然后在其中添加几个整个站点都会用到的函数。
肯定要用到addLoadEvent函数（参见第6章），因为在文档完全加载后如果想运行某个函数， 就要用到它。
_
function addLoadEvent(func) { var oldonload = window^onload;

12.5 JavaScript 231
if (typeof window^onload != _function1) { window^onload = func;
} else {
window.onload = function() { oldonload(); func();
另外，InsertAfter函数（参见第7章）也很有用，它与1nse「tBefo「e方法正好对应。
function insertA千ter(newElement，targetElement) { var parent = targetElement^parentNode; if (parentJastChild == targetElement) { parent•appendChild(newElement);
} else {
parent•insertBefore(newElement>targetElement.nextSibling);
最后还需要一个addClass函数（参见第9章)。
function addClass(element,value) { if (lelement^className) { element•className = value;
} else {
newClassName = element•className; newClassName+= ’丨"； newClassName+= value; element.className = newClassName;
>
}
要调用这个脚本，应该在模板页面1ndex.html结束的</b〇dy>fe签之前，添加一个<script〉fe 签：_
</article>
<script src=,fscripts/global^jsnx/script>
</body>
</html>
这样，站点中的每个页面都将包含global.js文件，而其中的函数也可以在这些页面里共 享了。
实际上，还需要向global.js文件中添加一个函数，就是下一节我们要写的hlghllghtPage。
12.5_1页面突出显示
每当我们基于模板页面创建一个新页面时，都要向<3「1：1(：16>元素中插入标记。对你要设计的 站点而言，这一部分正是每个页面之间不同的地方。
理想情况下，还应该更新每个页面<nav>元素中的链接。比如，如果当前页面是1ndex.html， 那么导航里面就没有必要添加指向当前index.html页面的链接了。
但在实际的网站开发中，不太可能一页一页地编辑导航链接。更常见的做法是通过服务器端包 含技术，把包含导航标记的片段插入到每个页面中。这里我们就假设服务器端会包含下列代码块:

232	第12章综合示例
<header>
<img src=,fimages/logo.gif,f alt=,f3ay Skript and the Domsters■’ />
<nav>
<ul>
<lixa href=nindex.htmrr>Home</ax/li>
<lixa href=Mabout.htmllf>About</ax/li>
<lixa href=nphotos.htmrf>Photos</ax/li>
<lixa href=,,live*html,,>Live</ax/li>
<lixa href=Mcontact.html,f>Contact</a></li>
</ul>
</nav>
</header>
服务器端包含可以使用Apache Server Side Includes (SSIs)、PHP、ASP,或者其他服务器端
语言。
服务器端包含的优点是可以把重用标记块集中保存。这样，等到以后要更新页面头部或者导 航链接时，只要修改一个文件就可以了。但集中保存的缺点，就是不能在每个页面中自定义这 个块。
无论如何，至少当前页面的导航链接还是应该突出显示的。通过突出显示，访客就能知道自 己“现在在这里”。
修改col 〇「_ css文件，添加为here类定义的样式：
header nav a♦here:link, header nav a^hereivisited, header nav a,here:hover, header nav a.here:active { color: #eef; background-color: #799；
为了应用刚刚定义的颜色样式，为指向当前页面的导航链接添加here类，如下所示：
<a href=nindex•html" class=l,here1,>Home</ax/li>
如果使用服务器端包含的话，要做到这一点可就不容易了。一般来说，服务器端技术应该为 每个页面创建正确的标记。但实际情况却并非始终如此。
JavaScript这个时候就能派上用场了。
在这个例子中，JavaScript是最后一招了。如果能在标记中直接添加here类，当然最好了。 但是，如果控制不了标记，就只好求诸JavaScript 了。
首先，删除已经添加到导航链接中的所有class属性。然后，编写一个hlghtllghtPage函数，
完成下列操作：
取得导航列表中所有链接；
循环遍历这些链接；
如果发现了与当前URL匹配的链接，为它添加here类。
同往常一样，先在函数中添加检査要使用的DOM方法的代码。此外，还要检査各种元素是 否存在。
function highlightPage() { if (!document♦getElementsByTagName) return false; if <!document•getElementByld) return false;

12.5 JavaScript 233
var headers = document^getElementsByTagName('header1); if (headers.length == 0) return false; var navs = headers[〇]•getElementsByTagName(lnav,); if (navs.length == 〇) return false;
取得导航链接，然后循环遍历它们：
var links = navs[〇].getElementsByTagName(flat!); var linkurl;
for (var i=〇; i<links.length; i++) {	A
接下来，要比较当前链接的URL与当前页面的URL。要取得链接的URL,可以使用 getAttribute("h「ef")，而要取得当前页面的 URL，则可以使用 window.location.href。
linkurl = links[i]*getAttribute(MhrefH);
JavaScript为比较字符串提供了很多方法。其中，IndexOf方法用于在字符串中寻找子字符串 的位置：
string .ir\dexOi(substring)
这个方法返回子字符串第一次出现的位置。我们在这里只想知道某个字符串是否被包含在另 一个字符串里面，是否是当前URL里的链接URL。
currenturl^indexOf(linkurl)
如果没有匹配到，IndexOf方法将返回-1。如果返回其他值，则表示有匹配。如果IndexOf方 法不返回-1，那么就可以前进到函数的最后一步了：
if (winddlocation.hre干•indexOf(linkurl) != -l) {
此时的链接一定是指向当前页面的链接，因此就给它添加here类：
links[i]^className = "here";
剩下的代码就是关闭If语句、关闭for循环和关闭function定义的花括号了。最后，使用 addLoadEvent 函数调用 hlghllghtPage。
function highlightPage() { if (!document•getElementsByTagName) return false; if 〇document•getElementByld) return false; var headers • documenttgetElementsByTagName('header1); if (headers.length ~ 〇) return false; var navs = headers[〇]^getElementsByTagName(lnav,); if (navs♦length == 〇) return false; var links = navs[〇]^getElementsByTagName(ffa,T);
for (var i=0; i<links^length; i++) { var linkurl;
for (var i=〇; i<links*length; i++) { linkurl = links[i^getAttribute(nhreffl)^ if (window^location*href^indexOf(linkurl) != -l) { links[i]*className = "here";
}
}
}
addLoadEvent(highlightPage);
保存包含这个函数的global .js文件。刷新Index.litml之后，你就会看到Home链接突出显
示了，如图12-8所示。

234	第12章综合示例

___v AV^W^W. > W • ♦ » 		»♦_•

Imf Skript
^ and the
:■脚
kniiiftrfi^A



■
義您J 气、讓f::
,，.^||麵一:…繼:
图 12-8
♦
\
利用hlghllghtPage函数，还可以达到一箭双雕的目的。
通过给每个页面的body元素添加Id属性，可以为每个页面应用不同的样式。为了给每个页 面添加独特的Id属性，可以取得并使用当前链接（即添加here类的链接）中的文本。但需要使 用JavaScript的toLowerCase方法把该文本转换成小写形式：
var linktext = linksfi].lastChild^nodeValue^toLowerCase();
这样就取得了当前链接最后一个子元素的值，也就是链接的文本，然后把它转换成小写形式。 如果链接中的文本是“Home”，那么linktext变量中保存的值就是"home"。通过下面的语句就可 以把这个变量的值设置为body元素的Id属性了 ：
document•body•setAttribute(nidM,linktext);
这条语句就相当于在<b〇dy>标签中添加了 IcKhome"。
现在的hlghllghtPage函数如下所示：
千unction highlightPage( href ) { if (!document•getElementsByTagName) return false; if (! document	return false;
var headers = documentgetElementsByTagName^header1);
if (headers•length == 0) return false;
var navs = headers[〇].getEle(nentsByTagName(,nav,);
if (navs•length == 〇) return false;
var links = navs[〇].getElementsByTagNaine(naH);
for (var i=0; i<links•length; i++) {
var linkurl;
for (var i=〇; i<links^length; i++) { linkurl = linksfij^getAttributeC^href11); if (window^location•href*indexOf(linkurl) != -l) { links[i].className = "here";
var linktext = links[i]^lastChild^nodeValue»toLowerCase(); document.body.setAttribute(,fidM, linktext);
addLoadEvent(highlightPage);

12.5 JavaScript 235
于是，1ndex.html文件的body元素就会有一个值为"home"的Id，about.html文件中的Id就是 "about", photos.html 文件中的 Id将是’’photos”，依次类推。
新加入的这些标识符都可以成为CSS中的挂钩。例如，可以利用这些Id为不同页面的头部 应用不同的背景图像。
接下来为每个页面制作一幅图像，大小为250x250px。也可以使用我已经做好的:11neup.g1f、 basshead.gif、bass1st.gif 和 daraier.g'if，把它们者P放到 Images 文件夹中。
然后就可以更新layout.css文件，添加background-image声明：
#about header { background-image:
>
#photos header { background-image:
>
#live header { background-image:
>
#contact header { background-image:
url(^♦/images/lineup.gif);
url(-•/images/basshead^gif);
url(.•/images/bassist^gif);
url(. •/images/drurmner^gif);
如此一来，每个页面的头部就会应用不同的背景图像了。
JavaScript 幻灯片
主页还需要美化一下。毕竟，大多数访客都要先访问主页，在其中添加一些炫酷功能是非常 有必要的。第10章讨论的JavaScript幻灯片用在这里正合适。
在"intm"那一段文字中，有指向站点其他页面的所有链接。如果在访客把鼠标放到相应链接 上的时候，能够让他们得到有关页面的一点信息应该不错。在这里，可以显示相应页面头部图像 的缩小版。
把每一幅图像缩小为150xl50px，然后合并为750px长的一张图，命名为sl1deshow.gif。 把这张图放在Images文件夹中。
组合后的图像如图12-9所示。



图 12-9
为了实现幻灯片功能，需要更新global.js文件。先把第10章中定义的moveElement函数复 制过来：
function moveElement(elementID^final_x,final_y^interval) { if (!document•getElementByld) return false; if (!document•getElementByld(elementID)) return false;
12

236 第12章综合示例
var elem = document•getElementByld(elementlD) if (elem.movement) { clearTimeout(elem^movement);
>
if (!elem.style.left) { eiem • style • left = !,〇px,r;
}
if (lelem*style.top) { elem^style^top = n0px";
}
var xpos = parselnt(elenustyle•left); var ypos = parselnt(elem.style*top); if (xpos == final_x && ypos == final_y) { return true;
}
if (xpos < final_x) {
var dist = Math.ceil((final_x • xpos)/i〇); xpos = xpos + dist;
if (xpos > final一x) {
var dist = MatH.ceil((xpos - final_x)/lO); xpos = xpos - dist;
}
if (ypos < finally) {
var dist = Math.ceil((finally - ypos)/l〇); ypos = ypos + dist;
}
if (ypos > final一y) {
var dist = Math.ceil((ypos - final_y)/l〇); ypos = ypos - dist;
>
eleiTh style • left = xpos + upxf,; elem^style.top = ypos + Irpxn;
var repeat = ,,moveElement(,l<+elementID+,fl/,+final_x+n,,t+final_y+H/t+interval+n) elem.movement = setTimeout(repeat,interval);
现在应该创建幻灯片元素并准备相应链接了。在此，我们把幻灯片直接放在文档中的"int「cy 段落后面。
function prepareSlideshow() {
if (!document•getElementsByTagName) return false; if (!document•getElementByld) return false; if (!document•getElementById(l,introrf)) return false; var intro = document^getElementById(Hintro,1); var slideshow = documentscreateElement(Hdivt,); slideshow.setAttribute("id","slideshow");
var preview = document •oreateElefnent("img");	•
preview^setAttribute(,fsrcll>,,images/slide$how^giflf);	•
preview^setAttribute(l!altM/fa glimpse of what awaits you’’）；
preview •setAttribute(’’id’V,preview’1);
slideshow^appendChild(preview);
insertAfter(slideshow,intro);
接着循环遍历"intm"段落中的所有链接，并根据当前鼠标所在的链接来移动preview元素。 比如说，如果链接的href值中包含字符串"about.html"，就把preview元素移动到-150px的位置 上；如果链接的href值中包含字符串"photos.htmV1，就把preview元素移动到-300px的位置上， 依次类推。

12.5 JavaScript 237
为了让动画效果看起来很帅，给moveElement函数传入仅为5毫秒的Interval值：
var links = intro.getElementsByTagName(Mal!); var destination;
for (var i=0; i<links.length; i++) { links[i]•onmouseover = function() { destination = this.getAttribute(,,hrefn); if (destination•indexOf(,tindex.html,r) != -l) { moveElement(,'preview11,0,0,5)；
}
i千（destination.indexOf("about.frtml") != -1) { moveElement("preview",-i5〇,〇,5);
}
if (destination.indexOf(l,photo$^htmrt) != -l) { moveElement("previewn,-3〇〇,〇,5);
}
if (destination^indexOf(lflive*htmri) != -l) { moveElement(llpreviewll>-45〇>〇, 5)；
}
if (destinatioruindexOf("contact.html”） ！= -l) { moveElement(npreviewn,-600^0,5);
}
}
}
}
还要通过addLoadEvent调用这个函数：
addLoadEvent(prepareSlideshow);
保存global, js文件。
当然，还得更新样式，在layout.css中添加如下声明：
#slideshow { width: 15〇px; height: 15〇px;
;position: relative;
overflow: hidden;
#preview {	•
position: absolute;
)order-width: 0;
outline-width: 0;
>
在浏览器中刷新1ndex.html，试一试幻灯片的效果。
看起来还不错。要是把动画效果放到一个小窗口里，就更完美了。
创建一幅150xi50px的图像，它的绝大部分都透明，只有四个圆角是与内容dlv颜色相同 的。把它命名为frame.gif并保存在Images文件夹中。
把下列代码添加到global .js中的prepareSlIdeshow函数中，放到创建slideshow元素的代码
后面：
var frame = document.createElement(n imgM); frame•setAttribute("src"/1 images/frame^丄;"）； frame •set Attribute(,laltn,,MI); frame^setAttribute(Mid,,/,frarnen); slideshow^appendChild(frame);

238	第12章综合示例
为保证这个小窗口出现在动画之上，还要在layout.css中加入如下代码：
#frame {
position: absolute; top: 0; left: 0; z-index: 99；
>
刷新Index.html，再试试幻灯片效果，现在图像应该舍出现在小窗口里面了。
目前，访客的鼠标放到"intro"段落中的链接上时会触k幻灯片动画。如果想让导航dlv中的 链接也能触发幻灯片，可以把下面这行代码：
var links = intro•getElementsByTagName(Man);
改为：
var links = documerrLgetElementsByTagName("a");
完成后的prepareSl 1 deshow函数如下所示：
function prepareSlideshow() { if (丨document•getElementsByTagName) return false; 、 if (Idocument.getElementByld) return false; if (!document.getElementById(,fintron)) return false; var intro = document-getElementById(Hintrorr); var slideshow = document.createElement(ltdivH);
slideshow. setAttribute(uid"/slideshow__);	)
var frame = document ♦createElement(11 imgn)j
frame.setAttribute(l,srcl,,lfimages/frame^gif,l)j
frame^setAttribute(f!alt%ll,f);
frame. setAttribute^id’Vframe");
slideshow^dppendChild(frame);
var preview = document.createElement(,limgt,);
preview^setAttribute(,lsrcn/1 images/slideshow.gifH);
previev^setAttribute<"alt","a glimpse of what awaits you’’）；
preview»setAttribute(,lid,,>,f preview11);
slideshow^appendChild(preview);
insertAfter(slideshow,intro);
var links = document^getElementsByTagName(,,a,t);
var destination;
for (var i=0; i<links.length; i++) { links[i].onmouseover = function() { destination = this^getAttribute(frhrefn); if (destination^indexOf(Hindex.htmrf) != -l) { moveElement("preview%0,0,5);
}
if (destination.indexOf(nabout,html") != -l) { moveElement(’’preview" ,-150,0,5);
}
if (destination•indexOf(1,photos.htmln) != -l) { moveElement (,f preview11^-3〇〇>〇>5)；
}
if (destination.indexOf(’’live.html") != -1) { nfioveElement(,lpreview,,,-45〇,〇,5)；
}
if (destinatiorKindexOf("contact.html") != -l) {
moveElement(upreviewfl,-600,0,5)；

12^5 JavaScript 239
addLoadEvent(prepareSlideshow);
这样，把鼠标放在导航链接上，也将会触发幻灯片，如图12-10所示。

二“，:I - r nrrr「「rr

图 12-10
12.5.3内部导航
站点中的下一页是About页面。在about.html的<3怍1(^>元素中添加如下标记:
<hl>About the band</hl>
<nav>	•
<ul>
<lixa href=’’#jay">]ay Skript</ax/li>
<lixa href=,f#domsterstf>The Domsters</ax/li>
</ul>
</nav>
〈section id=,ljaylt>
<h2>3ay Skript</h2>
<p>3ay Skript is going to rock your world!</p>
<p>Together with his compatriots the Domsters>
Day is set for world domination^ Dust you wait and see.</p>
<p>3ay Skript has been on the scene since the mid 1990s.
His talent hasnft always been recognized or fully appreciated•
In the early days, he was often unfavorably compared to bigger, similarly named artists• That's all in the past now.</p>
</section>
〈section id=”domsters">
<h2>The Domsters</h2>
<p>The Domsters have been around, in one 千orm or another,
千or almost as long. It's only in the past 干ew years that tfie Domsters have settled down to their current, stable lineup*
Now they're a rock-solid bunch: methodical and dependablex/p>
</section>

240 第12章综合示例
然后，About页面如图12-11所示。
♦ - rV 0 U	~~~'—~'~一窃



图 12-11
似乎还可以，但就是页面有点长了。知道为什么<nav>元素中包含内部链接吗？就是为了解 决这个问题。单击<nav>中的每个链接，都会跳到带有相应"id属性的<sect1on>。
而使用JavaScript和DOM,还可以选择性地每次只显示其中一个部分（section)。把下面这 个函数添加到global.js中，它能够根据指定的Id显示相应的<sect1on>，同时隐藏其他部分：
function showSection(id) {
var sections = document•getElementsByTagName("section'1); for (var i=〇; i<sections^length; i++ ) { if (sections[i].getAttribute(t,idH) != id) { sections[i] •style^display = ’’none";
} else {
sections[i]•style.display = ”block”；
这个showSectlon函数的用途是修改每个部分的display样式属性。除了与作为参数传入的Id 对应的部分，其他部分的dl spl ay属性都将被设置为"none"，而与传入1 d对应的那个部分的dl spl ay 属性则被设置为％1〇(±"。
然后，还需要在<art1cle>中的<nav>所包含的链接被单击时调用showSectlon函数。
创建一个名为preparelnternalnav的函数，先从循环遍历<8代1(：'^>中的<nav>所包含的链接
开始：

12^5 JavaScript 241
function preparelnternalnav() { if (!document•getElementsByTagName) return false; if (Idocument.getElementByld) return false; var articles * ciocument^getEiementsByTagNamerarticle"); if (articles•length == 〇) return false; var navs = articles[〇]^getEleir!entsByTagName(,lnav,t); if (navs.length == 0) return false; var nav = navs[〇];
var links = na^getElementsByTagName(”an); for (var i=0; i<links.length; i++ ) {
每个链接的href属性中都包含对应部分的1d，开头的“#”表示内部链接。要提取每一部分 的Id值，可以使用split方法。这是根据分隔符把一个字符串分成两或多部分的一种便捷方式:
array ^ string.split(character)
这里，我们想要的是“#”后面的字符串，因此可以以“#”为分隔符，得到的数组中包含两 个元素：第一个元素是“#”前面的所有字符（在此是空字符串），第二个元素则是后面的所有字 符。还得吧，数组中第一个元素的索引是〇,而我们想要的是数组中的第二个元素，它的索引 是1。
var sectionld = linksfi].getAttribute(,,href").split(,,#,,)[i];
这样就可以把“#”后面的字符串提取出来并保存到sectlonld变量中。
再添加一个简单的测试，确保真的存在带有相应Id的元素。如果不存在，则继续下一次 循环。
if (!document.getElementByld(sectionld)) continue;
在页面加载后，需要默认隐藏所有部分。下面这行代码可以解决问题：
document.getElementByld(sectionld).style,display = "none";
接下来可以给链接添加onclick事件处理函数，以便链接被单击后，把sectionld传给 showSectlon函数。但这里存在作用域问题。因为变量sectionld是一个局部变量，它只有在 preparelnternalnav函数执行期间存在，等到了事件处理函数执行的时候它就不存在了。
要解决这个问题，可以为每个链接创建一个自定义的属性。比如把这个属性命名为 destination，然后把sectionld的值赋给它：
links[i].destination = sectionld;
这个属性的作用域是持久存在的。回头，我们可以在事件处理函数中再查询这个属性：
links[i]•onclick = function() { showSection(this.destination); return false;
>
为preparelnternalnav函数加上几个花括号，结束它的定义。再通过addLoadEvent函数调 用它：
addLoadEvent(preparelnternalnav);
以下是 global _js 中的 preparelnternalnav 函数:

242 第12章综合示例
千unction preparelnternalnav() {
if (!document•getElementsByTagName) return 千alse;
if <! document	return false;
var articles = documents get ElementsByTagName(!t article11);
if (articles.length == 0) return false;
var navs = articies[〇hgetElemerrtsByTagName(irnav”）；
if (navs^length == 〇) return false;
var nav = navs[〇];
var links = nav.getElementsByTagName(Ha,f);
干or (var i=0; i<links.length; i++ ) { var sectionld = links[i]•getAttribute(,,href,l)^split(n#n)[l]; if (!document.getElementByld(sectionld)) continue; document •getElementById(sectionId).style^display = 11 none11;
links[i]
links[r
•destination = sectionld; .onclick = function() {
showSection(this•destination); return false;



addLoadEvent(preparelnternalnav);
在浏览器中打开about.html，测试一下刚才实现的功能。单击一个内部链接，应该只会显示 相关的部分。图12-12只是显示了一个部分的About页面。
4-% ^4 §	ViTTS
[t&v
图 12-12
页面越长，这个功能的效果就越明显。例如，要是有一个常见问题页面，那么每个问题都可 以作为内部链接来处理。而单击一个问题，就会显示出与该问题对应的答案，与此同时其他问题 的答案并不显示。
JavaScript 图片库
接下来我们来制作photos.html，这个页面是使用JavaScript构建图片库的理想之所。

12.5 JavaScript 243
客户提供了 JaySkript和Domsters演出的四张照片，大小为400x300px:
concert.jpg	—
bassist.jpg
guitarist.jpg
crowd.jpg
在Images文件夹里创建一个名为photos的文件夹，把这四张照片放到里面。再为每张照片 分别创建100 x lOOpx的缩略图：
thumbnail—concert.jpg
thumbnail_bassist.jpg
thumbnail_guitarist.jpg
thumbnail_crowd.jpg
把这些照片也放在photos文件夹中。
创建一组链接，指向全尺寸照片。为这个列表指定1dSn1magegaleryn。在每个链接中添力口一 个<1mg>标签，各个标签的six属性分别指向不同的缩略图。
<hi>Photos of the band</hl>
<ul id="imagegallery”>
<li>
<a href=,!images/photos/concert.jpgn title="The crowd goes wild">
<img src=l,images/photos/thumbnail-concert^jpg?l alt=Mthe band in concert" />
</a>	一
</li>
<li>
<a href=,!iiiiage$/photos/bassist^jpg!, title=nAn atmospheric moment11 >
<img src=nimages/photos/thumbnail_bas$ist.jpgtr alt=’’the bassist" />
</a>	~
</li>
<li>
<a href=,!images/photos/guitarist.jpg,! title=lfRocking outH>
<img src=,timages/photos/thumbnail_guitarist.jpglf alt=!,the guitarist11 />
</a>	一
</li>
<li>
<a href=Mimages/photos/crowd^jpgH title=nEncore! Encore!”>
<img src=,fimages/photos/thumbnail_crowd.jpg11 alt=Mthe audience1' />
</a>	一
</li>
</ul>
把这组链接放到photos.html的<3怍1 cl6>元素中。
更新layout.css文件，让缩略图片从垂直排列变成水平排列（如图12-13所示)。
#imagegallery li { display: inline;
>
为了让图片库的脚本正常运行，还需要再制作一个占位符图片。把这个图片命名为 placeholder .gif 并放到 Images 文件夹中。
接下来就可以把第6章和第7章编写的图片库脚本放到scripts文件夹的global .js文件中。

244 第12章综合示例
V^I* ♦ V、，，^_矿MM__I%_I___?輙VSVr*l^fV#MV ^ V<?s^	? ‘一' ?♦ w ?"> ■"•丨吻_1 私鈐K、i••“ ♦ ?	A*A^^A __ I 丨“ _ -   			 I ■ ?      
伞•♦鑀•企 W					—一^0 (



图 12^3
function showPic(whichpic) {
if (!document•getElementById(,fplaceholder11)) return true; var source = whichpic.getAttribute(nhref,!); var placeholder = document•getElementByld("placeholder"); placeholder •setAttribute(,rsrc?l, source); if (! documents get ElementById(!ldescription11)) return false; if (whichpic^getAttribute(Mtitle,f)) { var text = whichpic.getAttribute(irtitleM);
} else { var text = IM,;
}
var description = document• getElementById(udescription,f); if (descriptiomfirstChilchnodeType == 3) { description•firstChild.nodeValue = text;
}
return false;
function preparePlaceholder() { if (!document•createElement) return false; if (!document•createTextNode) return 干alse; if (!document.getElementByld) return false; if (!document.getElementByldCr,imagegallery11)) return false; var placeholder = document♦createElement(uimgn); placeholder •setAttribute(l,idH/'placeholder11); placeholder.setAttiibuteCsxcu,nimages/placeholder.gifu); placeholder•setAttribute(l,altM/fmy image gallery11); var description = documentscreateElement(MpM)j description•setAttribute("id","description"); var desctext = document♦createTextNode(t,Choose an image"); description♦appendChild(desctext);	-
var gallery = document\getElemen1:ById("iniagegallery’_); insertAfter(description,gallery); insertAfter(placeholder,description);

12,5 JavaScript 245
function prepareGallery() { if (!document•getElementsByTagName) return false; if (!document•getElementByld) return 干alse; if (!document.getElementById(,fimagegalleryH)) return false; var gallery = document.getElementById(,,imagegallery!,); vai \流s : g沿ery.gettle讯咐卿飞啡抓 for ( var i=0; i < links•length; i++) { links[i]•onclick = function() { return showPic(this);
}
}
}
addLoadEvent(preparePlaceholder);
addLoadEvent(prepareCallery);
只有一处微小的变化：description中的文本被放到了 placeholder图像的上方。 在浏览器中打开photos.html，试验一下效果（如图12-14所示)。



I纖!
卽 w	 芒
• «***«••«••••	• 9 t4 p% 7少歲分•严，y	| » I	$ • % f* 9* 99	tf t〇t» P *4 *• * « i « « « i • » « 4^4 4 ^ ••	«VM *♦一
♦，畴-# _ f ¥	’ 亡	;	刁焱旮<
P6Mg^^gB6CKS
•^SBtiuSKiil v1fc JJM
i™
隱屮
:■通
IbBWI
ggaaSEgg^KaFgf^
»KTgrg>?raMjJ44j4k
mBB^Sk
龄4德孩
fhinm oi the hm\d	,t..
®IWI»L lill™ a 二3^|£^
.m.«.	.. -x：	* ：:
 :* 、‘5 	—外托”、
• •:難鱗錄
.., ■// 5 A A
r ?w :<?> ^ ></^ -f ■.*•：.^fvr^：
:,〇/.公V•少
>-A
• • •、.，"；v/?夂”•;透乂"
.::參‘尜，
m	%-^ ^ -:
t^y^L l x A；^y^36fldlkiA ：	♦♦冊％ a >♦♦匕	八，w“ Z :i：心vZ
IBIMSBSIBBIBBBH
图 12-14
'y*n
12.5.5增强表格
客户给我们提供了 JaySkript和Domsters的巡演日程。每场演出，都有一个日期（data)、一 个城市（city)和一个地点（venue)。显然，这是表列数据。因此，Live页面应该包含一个巡演 表格D

246 第12章综合示例
<hl>Tour dates</hl>
ctable summary=uwhen and where you can see the band,f>
<thead>
<tr>
<th>Date</th>
<th>City</th>
<th>Venue</th>
</tr>
</thead>
<tbody>
<tr>
<td>Dune 9th</td>
<td>Portland> <abbr title=tfOregonM>OR</abbrx/td> <td>Crystal Ballroom</td>
</tr>
<tr>
<td>3une I0th</td>
<td>Seattle, <abbr title="Washington">WA</abbr></td> <td>Crocodile Cafe</td>
</tr>	#
<tr>
<td>]une l2th</td>
<td>Sacramento, <abbr title=nCalifornia,,>CA</abbrx/td> <td>Torch Club</td>
</tr>
<tr>
<td>]une I7th</td>
<td>Austin, <abbr title="Texasu>TX</abbr></td> <td>Speakea$y</td>
</tr>
</tbody>
</table>
把这个<table>放到"Mve.html中的<article>S素内。
接着再在layout.css中为表格中的单元格应用一些样式:
td {
padding: •Sem Bern;
>
♦
更新col or\ css，为表头和表格选定指定颜色：
th {
color: #edc; background-color: #455；
}
tr td { color: #223; background-color: #eb6;
在浏览器中打开11ve.html后，可以看到一个普普通通、丝毫没有应用什么脚本的表格（如 图12-15所示)。
此时，正好可以把第9章定义的表格样式化的函数strl peTabl es及hi ghl 1 ghtRows拿过来使用。 还可以把第8章的dlsplayAbbrevlatlons函数借用过来。







12.5 JavaScript 247

^ am	Jrty
:鐵◎免冢
•!祭0
♦	♦	z	• ^	v ^	•	*	/ ,声	•	•	*	•	，•
?i, ,:、，w*;

tmw Skripf
--and the *^：
■
'/^<A-
y^ys<^ym
，释 1
» ♦ ♦ r#
Tourclatcsl •
©齡•:銳*说分少:1
图 12-15
把这几个函数全都添加到global. js文件中，并通过addLoadEvent调用它们:
干unction stripeTables() { if (!document•getElementsByTagName) return false; var tables = document,getElementsByTagName(ntable"); for (var i=〇; i<tables.length; i++) { var odd = false;
var rows = tables[i].getElement$ByTagName(tltrM); for (var j=0; j<rows.length; j++) { if (odd ~ true) { addClass(rows[j],floddf,); odd = false;
} else {	•
odd = true;
function highlightRows() { if(!document.getElementsByTagName) return false; var rows = document •get ElementsByTagName(11 tr11); for (var i=0; i<rows.length; i++) { rows[i]«oldClassName = rows[i]^className rows[i]^onmouseover = function() { addClass(this,,fhighlightn);
}
rows[i]*onmouseout = function() { this#className = this^oldClassName
function displayAbbreviations() { if (!document•getElementsByTagName || !document♦createElement • 11 !document•createTextNode) return false;

248 第12章综合示例
var abbreviations = document.getElementsByTagName(nabbrM); if (abbreviations^length < l) return false; var defs = new Array();
for (var i=〇; iobbreviations^length; i++) { var current一abbr = abbreviations[i]; if (current~abbr.childNodes*length < l) continue; var definition = current一abbr.getAttribute("title”)； var key = current_abbr^lastChild.nodeValue; defs[key] = definition;
}
var dlist = document•createElement(,ldlM)j for (key in defs) { var definition = defs[key]; var dtitle = document•createElement(Mdtfr); var dtitlejtext = document•createTextNode(key); dtitle^appendChild(dtitle_text); var ddesc = document^createElement(t,dd,1); var ddesc_text = document•createTextNode(de干inition); ddesc•appendChild(ddesc_text); dlist♦appendChild(dtitle); dlist•appendChild(ddesc);
}
if (dlist.childNodes•length < 1) return false;
var header = document♦createElement(,th3fl);
var header一text = document•createTextNode(,!Abbreviations11);
header.appendChild(header_text);
var articles = document•getElementsByTagName(,larticlett);
if (articles•length == 〇) return false;
var container = articles[〇];
container.appendChild(header);
container•appendChild(dlist);
addLoadEvent(stripeTables); addLoadEvent(highlightRows); addLoadEvent(displayAbbreviations)j
在此，hlghllghtRows 和 dlsplayAbbrevlatlons 函数都稍有改动。
□ hlghlightRows:没有像以前那样直接应用样式属性，而是使用addClass函数添加了 highlight 类。这个类会在用户鼠标悬停在表格行上的时候应用。在应用新类名之前，先把原来的 className保存到名为oldClassName的自定义属性中。当用户的鼠标离开表格行之后，再 把classMame属性重置回原来的oldClassName值。
口 dlsplayAbbrevlations:修改了最后几行代码，因为这里要找的是article元素，而不是第 8章Id为content的dlv元素。
这两处修改也提醒我们，以前定义的函数仍然需要进一步抽象。比如说，可以为 dlsplayAbbrevlatlons函数再增加一个参数，以便指明把新创建的歹丨j表添加到明卩个元素中。
还要更新layout.css，再添加一些样式：
di {
over干low: hidden;
>
dt {
float: left;
}
dd {
float: left:

12.5 JavaScript 249
再更新 typography .css:
dt {
margin-right: lem;
}
dd {
margin-right: 3em;
}
最后，在col or. css中为odd和hi ghl 1 ght类添加颜色样式：
tr.odd td { color: #223； background-color: #ec8;
}
tr•highlight td { color: #223; background-color: #cba;
}
在浏览器中打开11ve.html，看一看增强之后的<table^E5。此时，偶数行都会有一个odd类 (如图12-16所示）。




图 12-16
12.5.6增强表单
还得为这个站点制作一个很重要的页面，这个页面能够让乐队的粉丝们跟乐手沟通。

250 第12章综合示例
想一想，差不多任何网站都会公布一些联系信息，哪怕只是一个电子邮件地址。对眼下这个 网站来说，你打算构建一个联系表单。
联系表单，和其他任何类型的表单一样，都需要某种服务器端技术来进一步验证并把数据保 存到后台数据库或系统中。Perl、PHP、ASP.以及其他服务器端编程语言都是可选的技术。但我 们这个例子不会涉及服务器端脚本，而是会创建一个极为普通的HTML页面，向访客显示感谢 信息。访客填充的信息也不会发送到哪去（别忘了，乐队是我们虚构的)。假如真有这么一个网 站，就必须得有服务器端脚本来处理用户提交的数据，把它们保存到数据库中，或者通过邮件转 发给适当的人，然后才显示感谢信息。
创建一个文件，命名为contact.html，当然这个文件要基于template.html来创建，只不过 〈art^i cl e> 中要包含一个 <form>:
<hl>Contact the band</hl>
<form method=Hpost,! action=,lsubmit^html,l>
<fieldset>
<p>
〈label for=lfname">Name:</label>
<input type=Mtextlf id=nnamen name=,lnameM
placeholder=MYour name" required=Mrequiredn />
</p>	、
<P>
<label 干or=nemailn>Email:</label> cinput type=’remail” id=lfemail11 name=’’email"
placeholder=,,Your email address" required=l!requiredft />
</p>
<P>
〈label for=umessageH>Message:</label>
〈textarea cols="45” rows="7" id="message"
name=Mmessage,t required=Mrequiredtf
^ placeholder=nWrite your message here^ nx/textarea>
</p>
<input type=l,submit,1 value=_rSend" />
</fieldset>
</form>
更新layout.css文件:
label {
display: block;
}
fieldset { border: o；
这样，就有一个基本的联系表单，如图12-17所示。
接下来，再基于template.html创建一个新文件，命名为subm1t.html。这一次，〈article：^ 包含了感谢信息。
<hl>Thanks!</hl>
<p>Thanks for contacting us^ Wef 11 get back to you as soon as we canx/p>
这个subnrit.html页面中只包含感谢信息，不处理表单提交的信息，你懂的（如图12-18 所示)。

12.5 JavaScript 251
Z9 fJ	iiii <	rmiAi j^bral
m	..	<SgS^ Jbi tainwwmi.yii^^wtwi^rr^^r^w^^wKacin^umiaBwtwwgawwurwwwfWXMWaiWBffftM^iWMiiiii^^flr^Ti ^KWA^KBt.	^ 一
令•	#澄丨衫	r,



图 12-17



图 12-18
1.字段标签
表单中有三个字段：name、email和message。每个字段都有一个对应的〈label〉标签。

252 第12章综合示例
作为增进可访问性的元素，label非常有用。它通过for属性把一小段文本关联到表单的一 个字段。对于屏幕阅读器来说，标签中的这一小段文本几乎是不可或缺的。
即使是那些视力没有任何问题的人，label元素同样也具有不可低估的价值。很多浏览器都 会为label元素添加默认行为：如果label中的文本被单击，关联的表单字段就会获得焦点。这 对于增进表单的可用性是很有帮助的。然而，并不是所有浏览器都实现了该行为。
可能上述行为在默认情况下是不存在的，但我们为何不自己添这种行为呢？所需的只不过 数行JavaScript代码而已。
⑴取得文档中的label元素。
如果label有for属性，添加一个事件处理函数。
在label被单击时，提取for属性的值。这个值就是相应表单字段的Id值。
确保存在相应的表单字段。
 让相应的表单字段获得焦点。	’
在global • js中添加函数focusLabels，并通过addLoadEvent函数在页面加载时执行该函数。
function focusLabels() {
if (!document.getEiementsByTagName) return false; var labels = document.getElementsByTagName(f,labeln); for (var i=〇; i<labels^length; i++) { if (!labels[i].getAttribute(f,forn)) continue; labels[i].onclick = function() { var id = this .getAttributed^for11); if (!document.getElementByld(id)) return false; var element = docuiTient.getElementByld(id); element focus ();
addLoadEvent(focusLabels);
在浏览器中加载contact.html页面，单击一个标签就会把焦点转移到关联的表单字段中。也 许访客使用的浏览器不支持这个行为。但现在不一样了，现在所有浏览器都会支持这个行为。
2.占位符值
我们注意到，联系表单中的每个字段都通过HTML5的placeholder属性添了占位符文本， name字段中有"your name"，email 字段中有"your email"，等等。
注意从增进可访问性的角度说，占位符值也很有价值。Web Accessibility Iniative指南的10.4 节指出，“在用户代理能够正确处理空的控件之前，应该在可编辑文本框和文本区中添加 默认的、占位字符^ [优先级3]。”要了解有关Web Accessibilitylnitiative的更多信息，请 访问 http://www_w3.org/WAI/。
过去，有些浏览器不能正确识别空的表单字段，从而为键盘导航制造了麻烦。访客无法通过 按Tab键进入空字段。
与<label>fe签类似，增强可访问性对任何人来说都是一件好事。即使是那些不使用键盘导航

12.5 JavaScript 253
人，看到表单字段中显示着提示文本，也会觉得非常友好。
通过HTML5的placeholder属性设置占位符值有一个缺点，那就是使用旧版本浏览器的用户
看不到字段中的占位符文本（字段仍然是空的)。
使用JavaScript可以保证字段中始终可以显示提示信息。不过，这一次我们不再使用DOM 核心的方法和属性，而是要使用HTMLDOM中最常用的一个对象：form对象。
j	form对象 <	頌茜::驅_|麵獲.
>,• V, " .V,w,		 : :	” 〜.々厶✓	/..A i V.V，.	<		 .	: : :	v	^	> . v V - V • .	V.	'	^	： . ； •	* V < ,<, %%, .	• A i.f. ,	.； i
有读者可能知道，HTML文档中的每个元素都是一个对象。每个元素都有110(]_31胎 nocfeType之类的DOIV[属性
而有些的元素具有的属性比DOM核心中定义的还要多。文挡中的每个表单元素都是一 个form对象，每个form对象都有一个e]ements.length属性。这个属性返回表单中的包含的 表单元素的个数：
form.elements.length
这个返回值与childNodes.length不一样，后者返回的是元素中包含的所有节点的个数。 而form对象的elements.length属性只关注那些属于表单元素的元素^如Input、textarea,等
菩
v .〇
相应地，表单中的所有字段都保存在form对象的elements属性中。也就是说，下面是，
个包含所有表单元素的数组： form, elements
. . . ♦ .
同样，这个属性与chtldNodes属性也不一样，后者也是一个数组彳chiIdNodes教飯返回的 是所有节点，而elements数组则只返回input、select、textarea以友其他表单字段。
elements数组中的每个表单元素都有自己的一组属性。比如，valt^属性中保存的就是表 .单元素的当前值: element,value
这行代码等价于： element • get Attribute( "value ’f)
包含在contact.html中的每个表单字段都有一个初始的placeholde「属性。你可以取得这些 占位符的值并临时将它们作为相应表单字段的value。而在该字段获得焦点时，再删除字段的 value值。类似地，如果用户并没有在字段中输入文本且离开了当前字段，那么再重新应用占位 符值即可。这个例子与第11章中的占位符的例子是类似的。
为此，你需要写一个函数，命名为resetFlelds,它只接受一个form对象作为参数。这个函 数执行如下操作。
⑴检查浏览器是否支持placeholder属性。如果支持，继续。
循环遍历表单中的每个元素。
如果当前元素是提交按钮，跳过。

254 第12章综合示例
为元素获得焦点的事件添加一个处理函数。如果字段的值等于占位符文本，则将字段的 值设置为空。
再为元素失去焦点的事件添加一个处理函数。如果字段的值为空，则为其添加占位符值。
为了应用样式，在字段显示占位符值的时候添加placeholder类。
这个函数的定义如下：
function resetFields(whichform) { if (Modernizr•input•placeholder) return; for (var i=0; i<which干orm,elements•leng士hj i++) { var element = whichform,elements[i]; if (element.type == "submit") continue;
var check = element.placeholder 11 element.getAttribute(1 placeholderf);
if (Icheck) continue;
element•onfocus = function() {
var text = this.placeholder || this*getAttribute('placeholder1); if (this^value == text) {
this.className * 1f;	^
this •value = t,M;
>
>
element•onblur = function() { if (this^value == ,,n) { this.className = ’placeholder、
this•value = this•placeholder || this•getAttribute(fplaceholderT);
} }
element ♦onblurO;
函数中用到了两个事件处理函数。其中，onfocus事件会在用户通过按Tab键或单击表单字 段时被触发，而onblur事件会在用户把焦点移出表单字段时触发。另外，在onblur事件定义之 后，立即调用了它，以便在必要时应用占位符值。
	   			 								 										 •!	t 1 r^^rr — — —rrmTrrmrrrfTinmtnmn Anmi mTTmnr mifiiinririiiiiDi imucw JL〇raca)t.uxa>cnaiCLia<iiuumi:；：T^-^iTiTTrT irnunninnuunuuumnu
注意鉴于不同的浏览器对未知属性的实现方式有所不同，这里同时使用了 HTML DOM的 placeholde「属性和 DOM 的 getAttributerplaceholder’）方法。
把resetFlelds函数添加到global. js文件中。但我们需要为它传入form对象来调用它。再编 辑一个函数prepareFoms，循环遍历文档中的所有fonri对象，并将每个form对象传给resetFlelds 函数。
function prepareForms() {
干or (var i=0; i<document•forms•length; i++) { var thisform = document•formsfi]; resetFields(thisform);
使用 addLoadEvent 函数来调用 prepareForms。
addLoadEvent(prepareForms);

12.5 JavaScript 255
为了让占位符更突出一点，在color_css文件中通过placeholder类修改字段的颜色：
input.placeholder { color: grey;
}
在不支持HTML5的浏览器中刷新contact.html，看看「esetPields函数的效果如何。你会看 到resetHelds函数起到了在支持HTML5的浏览器中使用placeholder属性一样的效果。
随便单击几个字段，或者单击相应的标签试一试。默认值应该消失。如果在没有输入文本的 情况下移动到另一个字段，默认值应该再次出现。如果输入了文本，那么默认值就不应该再出 现了。	-
表单验证
围绕联系表单的下一个任务涉及JavaScript最古老的用途。
自从JavaScript诞生之日起，客户端表单验证就拉开了序幕。想法很简单，就是在用户提交 表单时，对提交的值进行一番测试。如果必填字段留空，用户就会看到一个警告框，告诉他哪个 字段必须要填写内容。
支持HTML5的浏览器终于针对一省字段实现了原生的表单验证。例如，OpemlO可以自动 验证电子邮件字段，如图12-19所示。	'
当你提交包含电子邮件输入字段的表单时，Opera会基于RFC定义的电子邮件格式来验证用 户的输入，而且启不启用JavaScript都没有关系。HTML5还定义了其他类型的字段验证，例如 URL输入字段。对于这些字段而言，我们不必在表单中添加任何额外的标记；浏览器根据输入 字段的类型就可以完成验证。
HTML5也提供了 required属性，用于表示某个字段的值是必须填写不能留空的，如图12-20 所示。Opera 10同样支持不依赖任何脚本的这一原生特性。



图 12-19	图 12-20
对于支持HTML5的浏览器而言，这是个好消息。但对于客户委托给你制作的这个乐队网站 来说，还必须再灵活一点，还得再添加使用JavaScript验证表单的功能。
使用JavaScript进行表单验证听起来没有什么，而且通常也确实如此。但如果JavaScript验 证脚本写得不好，也会带来负面的结果。假如代码中包含错误，最终可能会导致用户根本无法提 交表单。
在使用JavaScript编写验证表单的脚本时，要记住三件事。

256 第12章综合示例
□验证脚本写得不好，反而不如没有验证。
□千万不要完全依赖JavaScript。客户端验证并不能取代服务器端的验证。即使有了 JavaScript验证，服务器端照样还应该对接收到的数据再次验证。
□客户端验证的目的在于帮助用户填好表单，避免他们提交未完成的表单，从而节省他们 的时间。服务器端验证的目的在于保护数据库和后台系统的安全。
一定要尽量保证验证过程尽可能简单。开始的时候，可以只检査用户是否输入了什么内容。 下面这个函数，IsPilled，以一个表单元素作为参数：
function isFilled(field) {
if (千ield.value.replace。 f/_).length == 0) return 千alse;
var placeholder = field•placeholder || field•getAttribute^1 placeholder1);
return (干ielckvalue != placeholder);
}
通过检查去掉空格之后的value属性的length属性，就可以知道value中是否没有任何字符 (不都是空格)。如果确实不包含任何字符，函数返回false。否则，继续下面的比较。
通过比较value属性与placeholder属性，就可以知道用户是否对占位符文本一字未动。如果 两个相同，函数返回false。如果上面两个测试都通过，说明用户已经在字段中填写了内容， IsFIlled函数就会返回true。
接下来一个类似的函数是IsEmall。这个函数会进行非常简略的检査，看表单字段中的内容 是不是一个电子邮件地址。
function isEmail(干ield) {
return (field^value^indexOf(,!@,f) != -l && field^value^indexOf!• -l);
>
这个函数使用IndexOf方法执行了两方面测试。这个方法用于在一个字符串中査找另一个字 符串第一次出现的位置。如果要搜索的字符串存在，则返回该字符串第一个字符所在的位置。如 果没有找到要捜索的字符串，则返回-1。函数中的第一个测试在表单字段的value属性中搜索@ 符号。这是电子邮件中绝不能少的一个符号。如果没有找到@，IsEinall函数就返回false。第二 个测试的原理相同，只不过搜索的是句点（•）符号。如果在表单字段的value属性中没有找到这 个字符，那么函数仍然会返回false。如果两个测试都通过了，IsEmall函数就返回true。
这个IsEmall函数并不十分可靠。如果用户输入了一个伪造的电子邮件地址，甚至根本就不 是电子邮件地址的字符串，验证也有可能通过。但是，验证写得太过复杂并不是件好事。验证越 复杂，误报的可能性就会越大。比如，很多验证电子邮件的脚本都错误地假设电子邮件的域名只 能是三个字母。这样的错误假设会导致域名为.info、.name之类的邮件就不能通过验证。
现在，你已经有了两个验证函数：IsFIlled和IsEmall。但你并不想对每个表单字段都运行它 们。因此，还需要某种方式来指定哪个字段是必填的，哪个字段必须输入电子邮件地址。
在HTML标记中，可以使用HTML5的requl red属性：	，
<input type=utextn id=nname" name=Mnamen value=MYour name” required=nrequiredn />
• •»
cinput type="email" id="email" name=Hemailn value=ftYour email address"
?required=拻required?/>

12.5 JavaScript 257
注意这里的代码使用了 required = "required"，而不是仅指定一个没有值的required属性。在 HTML5中，这两种写法都是有效的，因为HTML5兼容这两种语法。尽管如此，我还是 建议读者使用较为严格的XHTML语法，也就是说所有属性都要赋值，而且单独的标签 要添加斜杠（/)。
在CSS文件中也可以使用这些属性。例如，可以为必填字段添加粗一些的边框，或者应用 一种不同的背景颜色。
同样，在JavaScript中也可以使用这些属性。下面我们编写一个名为valldateForm的函数。 这个函数以一个form对象为参数，并执行下列操作。
循环遍历表单的elements数組。
如果发现了 required属性，把相应的元素传递给IsPilled函数。
 如果IsFIlled函数返回false，显示警告消息，并且valldateForm函数也返回false。
如果找到了 email类型的字段，把相应的元素传递给IsEmall函数。
 如果IsEmall函数返回false，显示警告消息，并且valldateForm函数也返回false。
否则，valldateForm 函数返回 true。
下面就是完成后的valldateFom函数： .
干unction validateForm(whichform) {
千or (var i=〇j i<whichform•elements.length; i++) { var element =： whichform.elements[i]; if (element•required ~ 1 required1) { if (!isFilled(element)) {
alert(lfPlease fill in the M+element^name+11 field/1); return false;
}
}
if (element•type == remail') {
if (!isEmail(element)) {
aiert("The "+element.name+" field must be a valid email address."); return false;
return true;
这样，只要在表单被提交时基于表单执行valldateFonn函数就可以了。为此，可以在 prepareForms函数中通过onsubmlt事件处理函数来添加验证行为：
function prepareForms() { for (var i=0; i<document•forms•length; i++) { var thisform = document•forms[i]; resetFields(thisform); thisform• onsubmit = function。{ return validateForm(this);
无论什么时候提交表单，都会触发submit事件，而事件会被onsutwit事件处理函数拦截。

258	第12章综合示例
执行事件处理函数时，会将表单传递给valldateForm函数。如果valldateForm函数返回true，就 意味着可以把表单数据提交给服务器。而如果valldateForm函数返回false,提交操作就会被取消。 把上面几个表单验证函数都保存到global .js中。
在浏览器中刷新contact.html。试一试，在留空表单或保持字段中默认值的情况下提交表单。 你应该会看到一个有礼貌的警告框弹出来，告诉你必须解决哪些问题才能提交表单，如图12-21 所示。



图 12-21
提交表单
针对联系表单的最后一项改进，就是给页面添加一点Ajax。还记得前面创建的submit.html 页面吗？如果你正确地提交了表单，表单就会打开submit.html显示感谢信息。如果表单能够发 送一个Ajax请求，而感谢信息能以嵌入方式添加到表单所在的页面，那种体验想必会更好。说 白了，就是表单提交成功之后，不打幵新页面了，而是拦截提交请求，自己显示结果。（关于拦 截的介绍请参考第7章。）
先在global. js文件中添加第7章的getHTTPObject函数：
function getHTTPObject() { if (typeof XMLHttpRequest == "undefined")
XMLHttpRequest = function () { try { return new ActiveX0b]ect(f,Msxml2.XMLHTTP.6^0,!); } catch (e) {}
try { return new ActiveX0bject(tfMsxml2^XMLHTTP^3-〇f,)； } catch (e) {}
try { return new ActiveX0bject(uMsxinl2.XMLHTTP,1); } catch (e) {} return false;
return new XMLHttpRequest();

12.5 JavaScript 259
然后，创建一个加载图像，在Ajax请求刚启动时把它添加到文档中。如果你手上没有动画 加载GIF，可以到http://ajaxload.info去创建一个。把这个加载图像命名为load1ng.gif，并将它放 在Images文件夹中。
把下面的dlsplayAjaxLoadlng函数添加到global • js文件中。这个函数接受一个D0M元素作 为参数，然后把它的所有子元素都删除掉。删除之后，再把load1ng.gif图像添加到该元素中。
function displavAjaxLoading(elew\er\t) { while (element.hasChildNodes〇) { element•removeChild(element♦lastChild);
}
var content - document •createElement(img11); content •setAttribute(,,src,,/,images/loading •giff,); content.setAttribute("art",,HLoa3ing. • element.appendChild(content);
}
好玩的地方到了。接下来该编写submltFomWIthAjax函数了。这个函数的第一个参数是一个
f〇「m对象，第二个参数是一个目标对象，并执行如下操作。
调用dlsplayAjaxLoachng函数，删除目标元素的子元素，并添加load化g.gif图像。
把表单的值组织成URL编码的字符串，以便通过Ajax请求发送。
⑶创建方法为POST的Ajax请求，把表单的值发送给subnrit.html。
如果请求成功，解析响应并在目标元素中显示结果。
如果请求失败，显示错误消息。
subrnltFonnWIthAjax函数在修改DOM和显示加载图像之前，首先要检查是否存在有效的 XMLHttpRequest 对象。
function submitFormWithAjax( whichform, thetarget ) { var request = getHTTPObject(); if (!request) { return false; } displayAjaxLoading(thetarget);
然后，创建一个URL编码的表单数据字符串，以便通过POST请求发送到服务器。这个URL 字符串的格式与URL参数相同：
name^value&natne2=value2&nanie3=value3
表单中每个字段的值都会被编码为这种数据字符串。比如说，如果表单中包含消息“Why does 2+2=4?”，字符串就类似如下所示：
message=Why does 2+2=4?&name=me&email=me@examplK：om
但是，这里面的加号（+)、等于号（==)和问号（?）都会带来问题。
□等于号的意思是不是说表单里有一个字段名叫2,而它的值是4呢？
□加号是一个编码后的空格，还是一个普通的加号？
□问号表示它后面是参数列表吗？
为了避免这些歧义，可以使用JavaScript的encodeURIComponent函数把这些值编码成URL安 全的字符串。这个函数会把有歧义的字符转换成对应的ASCII编码：
fnessage=Why%20does%202%2B2%3D4%3F%26&nanfie=Me&email=me%4〇example.com

260 第12章综合示例
接下来，就像前面验证表单一样，循环遍历表单的每个字段，但这次不是验证，而是收集它 们的名字和编码后的值，把结果保存在一个数组中：
var dataParts =[];
var element;
for (var i=〇; i<whichform.elements•length; i++) { element = whichform.elements[i];
dataParts[i] = element•name + !=f + encodeURIComponent(element•value);	.
}
收集到所有数据后，把数组中的项用和号（&)联结起来：
var data = dataParts.join('&');
然后，向原始表单的action属性指定的处理函数发送POST请求：
request• open(1 POST1, whichform.getAttribute(,'action11), true);
并在请求中添加 applKatlon/x-www-fonn-urlencoded 头部：
request•setRequestHeader(ftContent-type,1^ ’’application/x-www-form-urlencoded’1);
这个头部信息对于POST请求是必需的，它表示请求中包含URL编码的表单。
现在，请求已经准备好了。在发送请求之前，还需要创建处理响应的onreadystatechange事 件处理程序。
服务器返回的响应就是subnrit.html页面。这个页面与站点中其他页面一样，也包含头部区 域、导航和内容。因为我们是想把结果加载到已有的页面中，所以就不需要头部区域和导航了。 只要从页面中取得<art1cle>元素就足够了。而完整的页面放在那里，就是预备着在Ajax无效的 情况下，就直接返回subm1t.html页面。
如果你在使用自己常用的服务器端脚本语言编写响应，那么可以只为Ajax请求输出必要的 标记。但目前来讲，只能假设没有服务器端脚本，因此只能使用Ajax来增加一点用户体验。
为了从响应中提取出<art1cle>元素，你得考虑使用一种叫做正则表达式的技术。简单地说， 正则表达式就是一种模式，它以用来匹配字符串中的不同部分。
下面就是将会用于提取<3「1：1(：16>中内容的正则表达式：
/<article>([\s\S]+)<\/article>/
在JavaScript中，正则表达式的每个模式都以一个斜杠（/)开头和结尾。如果模式本身包含 斜杠，必须使用反斜杠对其转义，就像上面模式中对结束的</art1cle>标签中的斜杠转义那样。
要査找与正则表达式模式匹配的字符，只要输入想査找的字符即可。因为要提取的内容以 <a「t1cle>开始以</art1cle>结尾，因此就直接写出来就好。
注意正则表达式语法中会用到一些特殊字符，例如方括号和竖线。如果想直接匹配这些字符， 同样需要对它们进行转义，就像对斜扛转义一样。比如说，如果想在模式中匹配星号（*)， 就需要写成\*，因为*在正则表达式中用于表示重复。要了解其他特珠字符，请参考 http://en;wikipedia.org/wiki/Regular expression。

12.5 JavaScript 261
在<3怍化le^n</art1cle>之间，是一个捕获组，用于捕获位于开始和结束标签之间的文本。 捕获组中的方括号包含了要匹配的字符。而圆括号定义的捕获组是为了便于后面提取其中匹配的 内容。
如果你想猜出两个标签之间可能包含的所有字符，即使你的模式写得再长，最终可能还是无 济于事。为此，我们就在方括号中使用了特殊字符来表示要查找的内容。在这个正则表达式中， \s匹配任意空白字符，而\S匹配任意非空白字符，包括回车符和换行符。当然，除此之外，正则 表达式中还有很多其他字符类，用于匹配数值、单词、非单词之类的情况。
最后，在方括号后面，使用一个加号（+)表示前面的模式重复一次或多次。星号（*)表示 前面的模式重复零或多次。
简单地说，正则表达式模式/<art"icle>([\s\S]+)<\/article>/可以理解为如下：
□査找一个字符串，这个字符串以<a「t1cle>开头，后跟一或多个空格或非空格字符，最后 还有一个	cl e>;
口把这个字符串中的空格及非空格字符包含在一个捕获组中，以便后面提取。
有了正则表达式之后，就可以编写onreadystatechange函数了 ：
request•onreadystatechange = function () { if (request•readyState == 4) {
if (request.status == 200 || request.status == 0) { var matches = requesttresponseText.match(/<article>([\s\S]+)<\/article>/); if (matches•length > 0) { thetarget^innerHTML = matches[l];
} else {
thetarget•innerHTML = ,<p>0ops, there was an error. Sorry#</p>r;
}
} else {
thetarget•innerHTML = f<p>_ + request.statusText + ,</p>,;
}
>
>；
与第7章中的Ajax示例类似，这个函数一开始也是检测值为4的「eadyState属性，然后再 验证状态值是不是200。
在得到成功的响应后，就可以通过JavaScript的match方法对responseText应用正则表达式了。 match方法以正则表达式为参数，返回包含各种匹配结果的数组。
数组matches的第一个元素（索引为0)是responseText中与整个模式匹配的部分，即包括 〈article〉和〈/article〉在内的部分。因为模式中包含了一个捕获组（一对圆括号），因此matches 的第二个元素（索引为1)是responseText中与捕获组中的模式匹配的部分。在这个例子中，只 有一个捕获组，因此matches中也只包含两个元素。
在取得了捕获的内容之后，函数把matches[l]中保存的内容赋值给了目标元素的InnerHTML
属性，响应处理到此结束。
这样，submltFormWIthAjax函数中剩下的代码就是发送请求，并返回true，表示函数已经成 功发送请求。
request.send(data); return true;
}；

262 第12章综合示例
完成后的submltFormWIthAjax函数如下所示：
千unction submitFormWithAjax( whichform, thetarget ) { var request = getHTTPObject(); if (!request) { return false; } displayAjaxLoading(thetarget); var dataParts =[]; var element;
for (var i=0; i<whichform•elements.length; i++) { element = whichform^elementsfi];
dataParts[i] = element.name +	+ encodeURIComponent(element•value);
}
var data = dataParts•join(l&_);
request.open(1 POSTry whichform.getAttribute(tractionn), true); request•setRequestHeader(l1Content-typeH> tIapplication/x-www-form-urlencoded,1); request.onreadystatechange = function () { if (request•readyState == 4) {
if (request.status = 200 丨丨 request.status ~ 0) { var matches = request•responseText^match(/<article>([\$\S]+)<\/article>/); if (matches.length > 〇) { thetarget.innerHTML = matchesfl];
} else {
thetarget • innerHTML = f<p>0ops, there was an error• Sorryx/p>f;
}
} else {
thetarget.innerHTML = r<p>r + request.statusText + f</p>f;
}
}
}；
request.send(data); return true;
>；
现在，可以利用s—ltFomWIthAjax函数来执行拦截表单提交的任务了。为此，需要修改 prepareForms函数，调用submltForaWIthAjax，并给它传递当前的form对象和页面中的artKle元 素作为参数。修改后的函数应该完成如下操作。
口如果表单没有通过验证，返回false;因为验证失败，所以不能提交表单。
□如果submltFormWIthAjax函数成功发送了 Ajax请求并返回true,则让submit事件处理函 数返回false，以便阻止浏览器重复提交表单。
□否则，说明subnritFormWIthAjax没有成功发送Ajax请求，因而让submit事件处理函数返 回tme，让表单像什么都没有发生一样继续通过页面提交。
以下就是完成上述三项操作的prepareForms函数：
♦
function prepareForms() { for (var i=0; i<document.forms•length; i++) { var thisform = document•forms[i]; resetFields(thisform); thisform^onsubmit = function() { if (!validateForm(this)) return false; var article = document^getElementsByTagName(,article1)[〇];
if (submitFormWithAjax(this, article)) return false; return true:

12.5 JavaScript 263
好了，现在提交一下表单试试，你应该看到感谢信息出现在了同一个页面上，页面没有刷新。 不信，就看一看浏览器的地址栏。在提交了表单之后，你看到的还是contact.html，而不是 submit.html 0
联系页面制作完毕，当然整个网站也随之大功告成了。
12.5.7压缩代码
虽说你的网站已经可以上线了，但别忘了还有一件重要的事情要做：改进性能！此时此刻， global.js文件的大小是13 KB，不算大，而通过压缩，它还能再“痩身”。我们在第5章曾经讨 论过，用来压缩JavaScript代码的工具不少。在此，我们要使用的是谷歌的Closure Compiler。通 过它的在线表单，只要粘贴JavaScript进去，就可以得到压缩后的结果^
在浏览器中打开

http://closure-compiler.appspot.com/home，把global Js中的代码复制粘贴到 左侧文本区//ADD YOUR CODE HERE的下面，如图12-22所示。



图 12-22
单击Compile按钮，然后就可以得到编译后的代码，还有相关的统计信息。以我编写的 global.js文件为例，得到的结果如下：
口原始大小12.43 KB (gzip压缩后3_12 KB)
□编译后大小8.62 KB (gzip压缩后2.36 KB)
□比原始大小减少了 30.64% (gzip压缩版减少了 24_22%)
注意，根据所添加的注释及其他代码的多少，结果会有所差异。

264 第12章综合示例
在scripts文件夹中新建一个global .min. js文件，把压缩之后的代码复制粘贴到该文件中。 然后，把所有页面的巧^彳pt>#签中引用的脚本改为这个压缩版。
12.6小结
好了，JaySkripandtheDomsters乐队的网站终于可以上线了。不客气地说，你为他们设计 的这个站点在网络上绝对可以风靡一时。更重要的是，你把内容都放到了有效的、语义化的 HTML5标签里面，并用夕卜部样式表实现了整个外观设计。最后，又利用JavaScript和DOM为它 添加了诸多交互功能及可用性方面的增强。
而且，即便你把这些增强的功能去掉一部分，甚至全都拿走，整个站点照样可以完美地运行。 DOM脚本在这里并不是必需的，但有了它，光临站点的访客们会有更好的体验。想想看，这个 乐队居然是虚构的，就连我都有点为你愤愤不平啊！
那接下来还要学习什么？从某种意义上说，你的学习可以告一段落了。通过本书，你不仅掌 握了 DOM背后的理论知识，还把它实际运用到了构建完整的站点上面。利用从本书中学到的各 种方法和属性，你还能创造出更具实用性也更加强大的功能。
但从另外一个角度说，你的前端开发之路才刚刚开始。本书只向你展示了通过少数DOM方 法所能实现的少数功能。不仅这些方法还有更加广泛的用途，而且从未提及的很多其他方法都有 待你去探索呢。
基于DOM的脚本编程是一项值得深入掌握的技术。希望本书能让你对JavaScript和DOM产 生初恋一般的美好感觉。更希望你能肩负起一位技术人应有的责任，坚守DOM可用性的阵地， 并且能够乐在其中。在光怪陆离的现实世界中，你稍不留神就会误入歧途，掉进一味标新立异的 泥淖里。有时候，只要静下心来，回头看一看，把视角放得更开阔一些，问题就会变得很清楚。 从TimBemersLee发明万维网（WoirldWideWeb)至今，它的宏伟愿景就没有改变过：
Web的无所不在是它的魅力。保证任何人都能无障碍地使用它，是一个最基本的 原则。
Web中无处不在的超文本文档具有天然的可访问性。之所以变得让人处处受限，仅仅是由于 我们没有作出正确的选择。通过综合Web标准和最佳实践，让我们一起来保障Web的开放、无 障碍。
□使用有意义的标记来构建页面的结构；
□把表现性的信息者卩分离到CSS样式表中；
口负责任地使用不唐突的JavaScript来应用行为增强，同时确保平稳退化。
现在，我们正处于Web发展的十字路口。随着Ajax技术的普及和HTML5的出现，桌面软 件与Web应用之间的界限已经越来越不分明了。在努力推动Web向前发展的同时，还要坚守它 作为一个无处不在的媒体的初衷，势必要面临诸多挑战，战胜各种困难。
接下来的路在何方，这个问题只能你自己来回答。我只能告诉你，这是一个令Web设计师 激动不已的时代。
