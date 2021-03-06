###JavaScript 库


#JavaScript 库
本书从头到尾一直都在介绍DOM的基础知识。我们学习了如何使用标准的DOM方法来完 成常见的操作，如何在脚本中最有效地使用这些方法。也许你已经感觉到了，有时候自己的代码 会显得十分冗长，其中不少还都是重复的。如果只使用诸如document.getElementByld之类的DOM 方法，时间一长不免让人心生厌倦。实际上，很多JavaScript库提供的“魔术”函数（像$)不仅 可以当document.getElementByld来用，还能用来完成这个方法做不到的更多事情。
所谓库，就是可重用的代码包，具有如下一些优点。
□库代码经过了大量用户的测试和验证。
□库能够很容易地与已有的开发框架集成。
□库为大多数日常琐碎的DOM编程工作提供了方便、简洁的方案，每个函数都能节省很多 行代码。
□库很好地解决了跨浏览器的问题，让你更省心。
库可以把你从开发工作中解脱出来，让你专注于最重要的环节，极大地提升工作效率。虽然 使用库的好处很多，但也不是不存在问题。
□库是别人而不是你自己编写的。你可能不了解它的内部工作机制，因此很难调试bug或 解决由它所导致的问题。
□要使用库，就要把它集成到脚本中。这样就会加重页面加载的负担，挤占用户有限的 带宽。
□混合使用多个库可能会造成冲突，同时也会造成功能浪费。
如果你对库只能亦步亦趋而不能超越，那它也会成为你不思进取的慢性毒药。在决定使用库 之前，建议大家先花点时间真正掌握本书介绍的JavaScript和DOM编程技术。从第1章开始， 我们就一直强调理解工作机制的重要性，而不要停留在问题的表面上。唾手可得的库比比皆是， 稍后我们就会接触一些，但是如果你不能理解它们背后的工作机制，对你和你的程序都不能算是 什么好事。如果你对某个库理解不透，而这个库又假设你知道相关细节，那你就很可能被一些琐 碎的问题绊住脚。
在此声明一下，我本人与这些库没有任何关系，因此不会厚此薄彼。我也不认为这些库在任 何情况下都是最佳选择，也不是说只有这几个库可供选择。下面所举的例子，都是为了更好地说

266 附录 JavaScript 库
明如何利用库来更简单地完成本书前面介绍的那些任务。
接下来我们会重温前面涉及的如下主题。
□语法
□选择元素	^


□操作DOM元素	：
□处理事件	—
□动画 □ Ajax
你会看到怎么通过库来完成这些任务一通常要用的代码都会更少一些，以及为什么说使用 库能让你把精力更多地放在业务逻辑而非编写重复性的脚本上面。
注意对任何一个任务来说，每个库都会提供多种实现方渓。我只会从中选择一两种我认为最 佳或最有效的方法，不可能把每个库完成这些任务的所有可能性都列举出来。因此，请 读者通过阅读这些库的文档来了解其他的方法。
在使用库之前，最重要的是先搞清楚哪个库适合自己的需要。下面我们就介绍几条选择库时 需要注意的事项。	.
A. 1选择合适的库
在选择库的时候，你会发现自己将面临上百种选择。要作出正确的选择，建议你考虑如下 问题。
□它具备你需要的所有功能吗？混合使用多个库有可能导致问题。一些常见的方法，如$() 和get()，虽然表面上相同，但功能却完全不一样。此外，如果同时使用多个库，重复的 功能和冗余代码也是不可避免的。
□它的功能是否比你想要的还多？功能太少是一个问题，但功能过多同样不好。如果库中 包含很多你用不到或者不能完全利用的功能，最好还是选择一个功能少一些的版本，至 少能加快下载的速度。开发移动应用时这一点尤其要考虑。
□它是模块化的吗？在解决文件大小问题时，功能丰富的库通常使用模块化的方法，把不 同功能分割保存到不同的文件中。这样，你就可以只加载包含相应功能的个别文件，从 而降低下载量。多数情况下，恐怕都得事先加载所有必需的文件，只有少数库提供了动 态加载机制，让你能够按需动态加载文件。动态加载文件时，还要事先考虑到请求的次 数。经验表明，一次请求一个大文件，要比多次请求多个小文件更好。
□它的支持情况怎么样？如果库的背后没有活跃的开发人员社区维护，就意味着bug没人 修改，功能无法改进。从另一方面说，使用和维护的人多本身也说明它的问题更少，也 更可靠。库背后的社区不仅仅意味着修复和功能，也意味着在你需要帮助时能够及时得 到很多人的支持。

A.1 选择合适的库	267
□它有文档吗？没有文档，会让人无所适从。是这样的，也许你会碰到别人不知道什么时 候写的几个使用示例，但如果没有官方的文档，至少说明它的开发人员不够投入，而库 本身也不会有什么大的发展前途。
□它的许可合适吗？别以为可以在线查看源代码，自己就可以想怎么用就怎么用了。在决 定使用一个库之f，必须查证自己的用途包含在它的许可范围内，如果有特殊需求，就 更要事先确定了：
在选定了一个合适的库并在此基础上有了新的发明创造之后，别忘记回馈社区！这些库都是 开发人员无私奉献的结晶，他们牺牲自己有限的休息时间，就是为了改进你每天在用的工具。如 果你不能帮助改进库的功能或者修改bug，可以提供一些使用示例和教程啊，就算帮着写写文档 也是功德无量的。总之，只要有心，不管做什么都会促进库的良好发展。
A. 1.1有代表性的库
为了撰写这个附录，我根据前面的标准选择了几个有代表性的库，中间也掺杂点个人的喜好。 直说吧，后面的大多数示例都是使用jQuery编写的，少数使用的是具有类似功能的其他库。这 些库各有长短，简述如下。
jQuery (http://jquery.com)官方网站说它是“一个快速简洁的JavaScript库，致力于简化 HTML文档搜索、事件处理、动画以及Ajaz交互，从而实现快速Web开发。jQuery的设 计目的是为了改变你编写JavaScript程序的方式。” jQuery极为强大的选择方法、连缀语 法以及简化的Ajax和事件方法，都会让你的代码变得简洁且容易理解。这个库的背后还 有一个非常大的社区，包括大量插件开发人员，他们开发的插件极大增加了库的功能。
Prototype (http://prototypejs.org)把自己描绘成“一个旨在简化动态Web应用开发的 JavaScript框架。” Prototype提供了很多非常棒的D0M操作功能，还有一个广受好评的 Ajax对象。它是出名最早的一个JavaScript库，也是通过$()实现选择功能的鼻祖。
r
口 The Yahoo! User Interface (YUI) Libraty (h邱://developer.yahooxom/yui)的定位是“一套
碡
用JavaScript编写的实用函数和控件，可用来基于DOM、DHTML以及AJAX构建高交 互性的Web应用。YUI还包含了一些核心的CSS资源。” YUI的开发人员社区是很值得 称道的，它的文档也可圈可点。这个库涵盖的功能非常广泛，从简单的D0M操作到高级 的效果，以及全功能的应用程序部件，只要你能想到的，它都有。由于功能全面，YUI 被按照命名空间切割成很多独立的小文件，也正因为如此，有些使用者有时候会搞不清 自己到底需要哪个文件，到哪里去找到该文件。光API列表就长达20页，这个库的规模 就不难想象了。
DojoToolkit (

http://www.dojotoolkitorg/)说它能“帮你节省时间，性能优异，可以让开 发过程收放自如。它是经验丰富的开发人员为构建伟大的Web体验而提供给你的工具 包。” Dojo确实是一个功能丰富的JavaScript开发工具包，很多国际知识的大公司都在用。 它的开发人员社区也很庞大，文档做得也非常好，市面上有不少关于它的书。

268 附录 JavaScript 库
□ MooTools (

http://mootools.net/)说自己是“一个小巧、模块化、面向对象的JavaScript框 架，适合中高级JavaScript开发人员。利用它精巧、文档完备且前后一致的API，可以编 写出强大、灵活而又能够跨浏览器的代码。” MooTools的文档写得非常好，用户社区也有 相当规模。这个库不仅包含一些非常好用的D0M增强API，它的Moafic效果库更是令 人叫绝，能够实现各式各样的或简单或复杂的网页动画。
注意Prototype和jQuery还有其他库，都使用$()作为函数语法。如果你打算在自已的开发环境 中使用其中一个库，请务必先阅读相应库的文档，看看文档描述与本书介绍有哪些出入， 或者说该库在什么情况下会与其他库发生冲突。
A.1.2内容分发网络
一定要尽可能想办法减少网页文档的大小，并让浏览器缓存文件。除此之外，当然还要让用 户尽可能快地加载到页面。对于库来说，如果有很多站点要使用同一个库，那么最好是把这个库 托管到一个公共服务器上，以便所有站点共享和访问。这样，当用户从一个站点跳到另一个站点 时，他们就不用再重复下载相同的文件了。
内容分发网络（CDN，Content Ddevery Network)可以解决分布共享库的问题。CDN就是 一个由服务器构成的网络，这个网络的用途就是分散存储一些公共的内容。CDN中的每台服务 器都包含库的一份复本，这些服务器分布在世界上不同的国家和地区，以便达到利用带宽和加快 下载的目的。浏览器访问库的时候使用一个公共的URL,而CDN的底层则通过地理位置最近、 速度最快的服务器提供相应的文件，从而解决了整个系统中的瓶颈问题。
Google为以下这些库提供了免费的CDN服务：
广
Dojo
jQuery
MooTools
Prototype
Yahoo! User Interface Library (YUI)
要了解Google CDN托管的这些库的最新版以及其他特殊信息，请访问

http://code.google.com/ apis/libraries/devguide.html〇
使用CDN中托管的库与使用其他JavaScript文件一样。例如，以编写本书时的URL为例， Google CDN 中 jQuery 库的 URL 是 

https://ajax.googleapis.eom/ajax/libs/jquery/l.4.3/jqiiery.miiijs，
因而在文档中就可以添加如T^scri pt>标签：
<script src="

https://ajax.googleapis.com/ajax/libs/jquery/
^ i.4.3/jquery.min.js,!x/script>
如果你觉得仅仅依赖Google或其他CDN不保险，可以再提供一个后备〈script〉标签，以便 在CDN不可用时从本地服务器下载相应文件。方法很简单，无非就是先检测一下相应对象是否

A.2 语法 269
存在，如果不存在就添加加载本地文件的<5(：「1 pt>标签：
〈script src=nhttps://ajax^googleapis.com/ajax/libs/jquery/
l.4.3/jquery^min^ jsflx/script>
<script>!window•jQuery && document•write(unescape(f%BC	1
script src=nscripts/jquery-l•4.3•mirLjs"%3E%3C/script%3E’））</script>
注意这个方法使用document.write在jQuery库没有创建全局window.jQuery对象的情况下洛加 一个<script>标签。本附录中使用的$函数，其实就是对专有的jQuery对象的简写别名。
有了后备代码后，即便CDN的服务器出了问题，也不会连累你的网站了。
A.2语法
在展示具体的示例之前，应该先介绍一些很多库都采用的语法。
注意jQuery、Prototype、MooTools及其他很多库，都把$()函数作为其选择器方法的简写。因 此，在本附录中使用$()会让示例代码更通用一些。不过，也要注意，虽然调用这个函数 的语法形式相似，但不同的库在底层创建的对象则迥然不同。要了解具体的$函数的工作 原理，请查看相应库的文档。
多数库都支持以点将方法连缀起来的语法，也就是通过点操作符把多个方法调用连接成一行 代码；就像我们前面针对getElementByld用过的一样：
document•getElementByld(!example1)♦nodeName;
在jQuery之类的库中，方法连缀是一种特色，这些库特意设计了相应的方法，以便通过连 缀的形式将复杂的脚本连缀成简短的代码。使用这些库时，一行脚本完成多项操作是司空见惯的。 举个例子，使用jQuery先删除文档中所有段落的一个类名，然后再为它们添加另一个类名，可 以这样来写：
$(^§ ).removeClass(,classFoo, ).addClass(,classBar,);
与第9章的那个添加类名的函数相比，这行代码可是清晰多了。稍后我们还会介绍有关$(V) 选择器的更多信息。
另一个语法是迭代。不少库都提供了方便对元素列表进行操作的循环结构，而连缀语法则为 此提供了一种一目了然的方式。
仍以jQuery为例，对于下面这个第3章示例中的循环：
var items = document.getElementsByTagName(,rliff); for (var i=0; i < items•length; i++) { alert(typeof items[i])j
}
使用jQuery的each方法可以写成：

270 附录 JavaScript 库
$(1li1).each(function(i){
alert( typeof this );
});
jQuery的each方法以及其他循环方法，会基于列表中的每个元素来执行一个回调函数。这 个回调函数只接收元素在列表中的索引作为参数，并在当前节点的上下文中执行，因此这个例子 中的this引用的就是每个11元素自身。
了解库的基本语法之后，下面就来看一看选择元素。
A.3选择元素
到目前为止，你已经知道怎么使用内置的D0M方法getElementByld、getElementsByTagName 以及getElementsByClassName，来分别通过ID、标签和类名来选择元素了。
能通过ID选择元素很方便，但如果能使用各种CSS选择器来选择元素不是更好吗？很多库 都和jQuery—样，提供了类似其$函数的髙级选择器方法。使用这些方法，可以基于以下要素进 行选择：
□带#的1〇，如$('#element1d’）
□带•的类名，如 $('.element-class')
口标签名，如$('tag1)
当然，这些选择元素的途径还算不上十分特别，但关键是还可以使用各种CSS选择器 (

http://www.w3 .org/TR/cssS-selectors/Wselectors)来选择特定的元素。
注意在$函数中通过ID选择器#element1d选择元素时，该函数仍然返回对象列表，只不过返回 的列表中只包含一个元素。这样，你可以使用连級语法继续调用each及其他jQuery方法。
A.3.1 CSS选择器
除了使用ID、类名和标签以外，在多数库中都可以使用下列高级的选择器：
)选择所有元素；
$(弋39^选择所有HTML标签中的tag元素；
$('tagA 1:_]选择作为tagA后代的所有tagB元素；
$('tagA,tagB,tagC)选择所有tagA元素、tagB元素和tagC元素；
$r#1d_)和$( 'tag#1cT)选择所有ID为Id的元素或ID为Id且标签为tag的元素；
$(’ .className1)和$('tag.className')选择所有类名为 className的元素或类名为 className 标签为tag的兀素。
也可以使用组合选择器ir：^$runi a.selectMeia空格来分隔选择更具体的后 jQuery还支持下列CSS 2.1属性选择器:

A.3 选择元素	271
$(ftag[attrT)选择所有带有attr属性的tag元素；
$rtag[attr=value；H选择所有attr属性值恰好等于value的tag元素；
$rtag[attr*=value：T)选择所有attr属性值中包含字符串value的tag元素；
$rtag[att卜=value：T)选择所有attr属性值为空格分隔的多个字符串且其中一个字符串等 于value的tag元素；
$( ’tagLattr^value]1)选择所有attr属性值以value开头的tag元素；
$( 'tag[att「$=value]')选择所有attr属性值以value结尾的tag元素；
$(_tag[att「|=valuer)选择所有attr属性值为连字符分隔的字符串且该字符串以value开 头的tag兀素；
$(laghttr^value]')选择所有attr属性值不等于value的tag元素。
此外，还可以使用子选择器或同辈选择器：
$rtagA > tagB’)选择作为tagA元素子元素的所有tagB元素；
$('tagA + tagB'^择紧邻tagA元素且位于其后的tagB元素；
$(’tagA〜择作为tagA同辈元素且位于其后的所有tagB元素。
还可以使用一些伪类和伪元素选择器：
$(1 tag: roor)选择作为文档根元素的tag元素；
口 $( _tag:nth-ch11d(n)')选择作为其父元素正数第n个子元素的所有tag元素；
$rtag:nth-last>cMld(nV)选择作为其父元素倒数第n个子元素的所有tag元素；
$rtag:nth-of-type(nV)选择几个同辈t的元素中的正数第n个；
$rtag:nth-last-of-type(n) _)选择几个同辈tag元素中的倒数第n个；
$rtag:first-cMlcT)选择作为其父元素第一个子元素的tag元素； a $(_ tag: 1 ast-chi 1 d _)选择作为其父元素最后一个子元素的tag元素；
$('tag:fi「st-of-type」选择几个同辈tag元素中的第一个；
$rtag: last-of-type]选择几个同辈tag元素中的最后一个；
$(’t的:only-chi 1 cH选择作为其父元素唯一子元素的tag元素；
$rtag:only-of-type]选择同辈元素中唯一一个标签为tag的元素；
$('tag:empty')选择所有没有子元素的tag元素；
$(’tag:enablecT)选择界面元素中所有已经启用的tag元素；
$rtag:d1sabled_)选择界面元素中所有已经禁用的tag元素；
口 $rtag:checkecn选择界面元素中所有已经被选中的tag元素（如复选框和单选按钮）；
$( _tag:not(s) ’)选择与选择器s不匹配的所有tag元素。
不同的库对上述选择器的支持情况各不相同，请査阅相应库的文档以了解具体的情况。
利用这些选择器，就可以基于它们在文档中的位置而不必通过类名或ID而迅速找到任意一 个特定的元素。而且，你的脚本不仅因此可以不再依赖于特定的ID或类名，还能减少选择元素 所需的代码。比如说，要选择文章中nav元素包含的所有链接，可以使用DOM方法通过下列代
码实现：

272 附录 JavaScript 库
var links =[];
var articles = document•getElementsByTagName(r!articlen); for (var a = 0; a < articles.length; a++ ) { var navs = articles[a].getElementsByTagName(,fnavM); for (var n = 0； n < navs♦length; n++ ) { var links = nav[n]^getElementsByTagName(tfa!,); for (var 1 = 0; 1 < links•length; 1++ ) { links[linkStlengh] = links[l]j
}
//对链接执行相应操作
但利用选择器语法，则可以缩短为很少的字符：
var links = $(!article nav a1);
//对链接执行相应操作
这样，代码不仅清晰了很多，而且也很容易看懂。 ’
A.3.2库所提供的专有选择器
有些库还提供了专有的选择器，例如jQuery支持$('tag:everT^p$rtag:odcn选择器，用于 选择偶数和奇数元素。第12章有一个为表格行添加条纹样式的函数：
function stripeTables() { if (! documentreturn false; var tables = document•getElementsByTagName(11 table11); for (var i=〇; i<tables.length; i++) { var odd = false;
var rows = tables[i].getElementsByTagName(,,trM); for (var ]、0; j<rows.length; j++) { if (odd ~ true) { addClass(rows[ j],noddl!); odd = false;
} else { odd * true;
而用一行jQuery代码，就可以轻松地选择所有奇数表格行并为它们应用CSS属性：
$(,ftr:oddn)^addClass(nodd,f);
怎么样，是不是简单明了？ jQuery还支持其他专有选择器。
$rtag:everT)选择匹配元素集中的偶数个元素——特别适合突出显示表格行！
$rtag:odd’)选择匹配元素集中的奇数个元素；
$('tag:eq(0厂)和$(心9:咖(0)1)选择匹配元素集中的第n个元素，如页面中第一个段落;
$rtag:gt(nV)选择匹配元素集中索引值大于n的所有元素；
$rtag:lt(nV)选择匹配元素集中索引值小于n的所有元素；
$(’tag:f1「st’)等价于:eq(0);

A.3 选择元素	273
$('tag:last_)选择匹配元素集中的最后一个元素；
$('tag:parent')选择匹配元素集中包含子元素（文本节点也算）的所有元素；
$rtag:conta1nsrtest _ V)选择匹配元素集中包含指定文本的所有元素；
$(_tag:visile')选择匹配元素集中所有可见的元素(包括display属性为block和Inline、 vis化111ty属性为visible以及type属性不是hidden的表单元素）；
$(’tag:h1dderT)选择匹配元素集中所有隐藏的元素（包括display属性为none、visibility 属性为hidden以及type属性为hidden的表单元素）。
使用这些选择器可以快速地修改元素，比如要修改页面中第一个段落的字体粗细：
$("p:first").css(，_fon1>weight","bold");
或者用一行代码来显示所有隐藏的<d1 V>元素：
$(l,div:hidden,f) •showO;	.
甚至就连要隐藏所有包含单词“scared”的dlv元素都易如反掌：
$(’丨 div: contains (’scared1 )rr).hide();
最后，jQuery还提供了一些专门为表单设计的表达式，用于快速访问表单元素：
:1nput选择表单中的所有元素（"input、select、textarea、button);
:text选择所有文本字段（type=ntext");
□〔password选择所有密码字段（type="password");
Tadlo选择所有单选按钮（type="rad1o");
:checkbox选择所有复选框（type="checl<box");
:subm1t选择所有提交按钮（type="submit");
:1mage选择所有表单图像（type=n1mage");
:reset选择所有重置按钮（type=nreset");
:button选择所有其他按钮（type=nbuttorT)。
A.3.3使用回调函数筛选
在髙级表达式还不能满足你的需要，或者某个库不支持某个表达式的情况下，还可以使用回 调函数来选择DOM元素，也就是基于每个元素执行相应的筛选代码。在接下来的所有示例中， 回调函数返回true则意味着相应的元素会出现在结果集中，返回false则意味着相应元素不会出 现在结果集中。
如果你想创建一个反向选择器，那么使用回调函数会非常方便。所有CSS选择器选择的都 是表达式最右端的元素，因此就没有办法通过它们选择“只包含一个图像子元素的所有锚标签”。 但使用回调函数则可轻松实现这个选择。假设有以下HTML:
<ul>
<li>
<a name=_rexamplel"><img src=Mexample.gifff alt=rrexamplef7x/a>
</li>
<li>	、

274 附录 JavaScript 库
<a name=lrexample2f,>No Images Here</a>
</li>
<li>
<a name=’’example3">
Two here!
<img sro"example2^gif" alt=ltexafnplel7>
<img src=flexample3.gif11 alt=Mexamplel7>
</a>
</li>
</ul>
使用YUI的YAHOO.utll.Dom.getElementsBy方法，基于本书前面介绍的DOM元素属性，即可 筛选出想要的元素：
var singlelmageAnchors = YAHOO』til』cmugetElementsBy(干unction(e) {
//査找只包含一个图像子元素的<a>节点
return (e.nodeName == ’A1 &S e.getElementsByTagI\lame(limgl).length == l);
})；
此时变量singlelmageAnchors会包含一个列表，列表中只有一个元素，因为示例代码中只有 一个仅包含一个图像子元素的锚，因此该元素引用的就是<a nauie="exampler>。
Prototype和jQuery为此分别提供了 flndAll和filter方法。在连缀调用方法的时候，使用这
两个方法就可以筛选出表达式返回的元素来。
首先来看一下Prototype的代码（使用$$选择器）：
// Prototype库的回调筛选函数
var singlelmageAnchors = SSCa^findAll(干unction(e) { return (e*descendants()^findAll(function(e) { return (e^nodeName == 'IMG1);
}).length == 1);
});
再看一下jQuery的代码：
//jQuery库的回调筛选函数
var singlelmageAnchors = $('a1).filter(function() { return ($(limgl,this).length == i)
})；
Prototype和jQuery的表达式选择器应该足以应付大多数的情况。万一你还需要对元素进行 更深入的分析，那么回调函数还可更复杂一些。
A.4操作DOM元素
每个库都提供了非常多的DOM操作方法，毕竟操作DOM的能力可以体现一个库的水平。 这里我们只简单列举其中几个，剩下的还是请读者自己去查阅相关库的文档。
A.4.1生成内容
用jQuery创建新的DOM元素很简单。把HTML代码作为$函数的参数传入，即可创建新的 节点。下面这行代码就可以给文档的body元素添加一个新的dlv元素。新的dlv元素会有一个值 为example的Id,并且包含“Hello”。

A.4 操作DOM元素 275
$(’<div id="example’f>Hello</div>f).appendTo(document.body);
或者，也可以试一试jQuery 的模板插件（

http://api.jquery.com/category/plugins/templates)。
注意可以使用Microsoft CDN中托管的这个模板插件。在编写本书时的URL为

http://ajax. microsoftcom/ajax/jquery.templates/betal/jquery.tmpLmin.js。
使用jQueiy模板插件可以在HTML字符串中声明一些特殊的变量，如${tenn}，这些变量随
后可以被替换成一组数组或其他模板。，
举个例子，以下是第8章的dlsplayAbbrevlatlons函数：
function displayAbbreviations() {
if (Idocument^getElementsByTagName 丨丨!document.createElement
叫丨! document • createTextNode) return false;
var abbreviations = document♦getElementsByTagName(Mabbrtr); if (abbreviations•length < l) return false; var defs = new Array(); for (var i=0; iobbreviations • length; i++) { var current_abbr = abbreviations[i]; var definition = current_abbr.getAttribute(lftitlefl); var key = current一abbnlastChiicLnodeValue; defs[key] = definition;
}
var dlist = documentscreateElement for (key in defs) { var definition = defs[key]; var dtitle = document•createElement(l,dtM); var dtitle—text = document•createTextNode(key);
.dtitle^appendChild(dtitle_text);
var ddesc = document.createElement(''dd11);
var ddesc_text = document•createTextNode(definition);
ddesc.appendChild(ddesc_text);
dlist•appendChild(dtitle);
dlist•appendChild(ddesc);
}
var header = document.createElement(flh2u);
var headerjtext = document•createTextNode(t,Abbreviations11);
header.appendChild(header_text);
documents body•appendChild^header);
document.body•appendChild(dlist);
}
如果使用jQuery及jQuery模板插件，可以如下重写：
function displayAbbreviations() {
//创建缩写词数组
var data = $(labbr,).map(function(){ return {
desc:$(this)^attr(rtitle1), term:$(this)^text()
}；
}).toArray();
//添加到文档并应用模板
$(,<h2>Abbreviations</h2>f).appendTo(document•body)•after(
$*tmpl( n<dt>${term}</dt><dd>${desc}</dd>ff, data )
•wrapAll("<dl/>，r)
)；

276 附录 JavaScript 库
更进一步，还可以把模板从函数中分离出来，根据每一页的具体情况来定义缩写词模板。模 板插件的文档（

http://api.jquery.com/tmpl)中详细介绍了利用<schpt^素的更高级模板功能，请 读者自行参考。
A.4.2操作内容
如果想对现有文档执行某些操作，或者移动某些元素的位置，可以使用jQuery的appendTo 或InsertAfter等方法。通过这些方法，可以找到一组元素，并把它们全都变成另一个元素的子 元素。
例如，可以把一个列表中的所有元素全部转移到另一个列表中：
$(Tul#listl li1)^appendTo(nul#list2n);
之所以可以实现这种操作，原因在于每个元素在文档中都只有一个引用。你让它成为另一个 元素的子元素，也就意味着它必须与原来的父元素解除“父子关系”。假如你想的是复制这些元 素，那么可以使用jQuery的done方法：
$(ful#listl li1 )^clone()^appendTo(l,ul#list2,t);
DOM操作在任何一个库中都受到了极大的重视，它们分别都提供了一些用于删除、插入、 添加、前置等操作的快捷方法。
A.5处理事件
综观全书，不难发现事件其实是用户交互的根本所在。没有事件，也就没有办法与页面交互。 通过前面的学习，相信你已经掌握了一些基本的事件方法。说到使用库，当然很多也都内置 了相应的事件管理功能。而且，这些库还包含了浏览器没有原生实现或者说W3C事件模块中没 有定义的自定义事件的注册及调用机制。
A.5.1加载事件
前面介绍过一个为页面加载事件注册处理方法的函数，即addLoadEvent:
干unction addloadEvent(func) { var oldonload = window^onload; if (typeof window^onload != 1 function1) { window^onload = func;
} else {
window.onload = function() { oldonload(); func();
利用这个函数可以在页面加载的时候执行其他函数:
function myFucntion() {
//在页面加载后执行一些操作
}
addLoadEvent(mvFunction);

A.5 处理事件	277
以上代码也可以写成：
addLoadEvent(function() {
//在页面加载后执行一些操作 })；
不同的库也都提供了类似的方法，只不过在实现方式上会有所不同。比如说，jQuery就利用 连缀语法基于每种事件类型都提供了相应的事件方法（

http://api.jquery.com/category/events)。
以addLoadEvent为例，jQuery的ready方法以类似的方式实现了相应的机制：
%(documr\t) .ready (handler);
$(handler);
第二个方法假定document对象是ready方法的目标。而ready方法可以接收一个匿名函数， 并将该函数注册为处理文档就绪事件的处理函数：
$(document).ready(function() {
//在页面加载后执行一些操作	•
})；
这样，只要D0M初始化工作一完成，就会调用「eady，相应地就会立即执行传入的回调函 数。
如果想像使用addLoadEvent函数一样使用jQuery的方法，只要把addLoadEvent替换成$就可 以了：
function myFucntion() {
//在页面加载后执行一些操作
}
$(myFunction);
或者干脆这样写：
$(function() {
//在页面i卩—后执行一些操作 });
A.5.2其他事件
除了加载事件，jQuery等库还提供很多特定于元素的事件，例如blur、focus、click、dblcllck、 mouseover、mouseout 和l submit，等等。
使用这些事件方法，可以为DOM元素批量注册事件处理函数，比如为页面中的每个链接注 册相同的click事件处理函数：
$('al).click( function(event) {
//在新窗口中打开当前href中的链接 window.open(this.getAttribute(1 href1));
//阻止链接的默认动作 return false;
});
这些方法还有另一种意外的用法，即在没有用户交互的情况下，你可以通过调用相应的方法 来触发元素上已经注册的事件监听器。
$(fa:first,).click();

278 附录 JavaScript 库
举例来说，下面是第12章的resetFlelds和prepareForms函数：
function resetFields(whichform) { for (var i=0; i<whichform•elements•length; i++) { var element = whichform.elements[i]; if (element•type == n$ubmitn) continue;
var hasPlaceholder = element•placeholder || element•getAttribute('placeholder1); if (!hasPlaceholder) continue; element.onfocus = function() {
var text = element♦placeholder 丨| element.getAttribute(1 placeholder1); if (this^value == text) { this^className = 1f; this•value = n";
element.onblur = function() { if (this^value « ,fn) { this^className = 'placeholder1;
this.value = element.placeholder || element•getAttribute(1 placeholder1);;
} }
element^onblur();
function prepareForms() { for (var i=〇; i<document^forms•length; i++) { var this千orm = document*forms[i]; resetFields(thisform);
addLoadEvent(prepareForms)
使用jQuery选择器和事件方法，以上准备表单的代码可以缩短为:
$(function() {
‘（•form input[placeholder]’）•干ocus(function(){ var input = $(this);
if (input.val() == input.attr('placeholder1)) {
input^val(11)^removeClass(rplaceholder1)•;
}
}).blur(function(){ var input = $(this); if (input.val() == 11) {
input•val(input.attr(lplaceholder1))#addClass(lplaceholder1);
}).blur();
})；
A.6 Ajax
Ajax应用爆发后，JavaScript库也变得越来越流行起来。很多库中的第一个对象就是Ajax, 即便不是，Ajax对象也是这些库迅速流行的一个重要原因。
A.6,1 Prototype 与 Ajax
最早源于RubyonRails项目的Prototype库，就是因Ajax对象而流行的。Prototype提供了几 种独特的Ajax方法：

A.6 Ajax 279
Ajax.Request(u「l, options)执行基本的 XMLHttpRequest 请求；
 Ajax.Updater(element, url, options)包装请求，并且将请求返回的内容自动添加到给定的 DOM节点中；
Ajax.Period1calUpdater(element, url, options)按照一定的时间间隔自动将请求返回的内
容添加到给定的DOM节点中。
以上每个方法中的options参数都包含下列属性。
contentType，即请求的内容类型。默认值为 appllcatlon/x-www-form-urlencoded。
method，即请求的HTTP方法。Prototype对于put和delete等请求的处理方式，以post 请求重写并将原始请求方法放到请求的jnethod参数中。默认值为post。
parameters，即与请求一同发送的参数。这些参数的格式可以是类似get请求中URL编码 的字符串，也可以是类似散列的对象，比如数组或以属性名表示参数名的对象。
postBody，默认值为null，即在post请求体中包含的内容。如果为空，请求体中将包含 parameters选项的内容。
□「equestHeaders,是一个对象或数组，可以通过它在请求中添加额外的头部信息。如果是 对象，属性名和值分别表示请求头部的名和值；如果是数组，则偶数索引项（从〇开始算) 表示头部信息的名称，奇数索引项（从1开始算）表示请求头部信息的值。默认情况下， Prototype会在这个属性中包含几个头部信息（重写就没有了）：
■ X-Requested-W1th，默认情况下为XMLHttpRequest，供服务器端识别Ajax请求用。你可 以根据自己的需要设置。
X-P「ototype-Version，Prototype 当前的版本号。
Accept，默认设置为 text/javasc「1pt、text/html、appllcatlon/xml、text/xml 和*/*。
_ Content-type,根据contentType的值和编码方式构建。
除了这些属性外，还可以在请求的不同阶段根据服务器的响应调用一些回调方法。下列每一 个回调方法都应该接收到两个参数，一个是XMLHttpRequest对象，另一个在响应包含X-JSON头 部的情况下是响应返回的JavaScript对象。如果没有X-JSON头部信息，贝lj第二个参数为null。 唯——个例外是onExceptlon回调方法，它的参数一个是Ajax.Request实例，另一个是异常对象。
下面以它们在请求中被调用的顺序列出了这些回调方法。
onExcept1on(ajax. request,exception)在请求或响应中出现错误时被调用，可能会在下面任
何一个回调方法执行期间同时发生。
onUirin1t1al1zed(XHRrequest ,json)在请求对象创建完成后可能会被调用，但不一定总会被
调用，因此尽量不要使用它。
onLoachng(XHRrequest,json)在对象创建完成且其连接打开时可能会被调用，但同样不一定 总会被调用，因此尽量不要使用它。
onLoadecKXHRrequest,json)在请求对象创建完成、连接打开且准备好发送请求时可能会被
调用，但同样不一定总会被调用，因此尽量不要使用它。
onInteract1ve(XHRrequest ,json)在请求对象接收到部分响应但尚未接收到全部响应时可能

280 附录 JavaScript 库
会被调用。没错，它同样不一定总会被调用，因此尽量不要使用它。
on### (XHR「equest,json)在适当的响应代码被设置时会被调用。###是用来表示响应情况的 HTTP状态代码。这个回调方法会在响应完成但尚未调用onComplete之前被调用。这个方 法也会阻止onSuccess和onFallure回调方法的执行。
onFa11ure(XHRrequest, json)在请求完成且有状态代码但其状态代码不是200到299之间的 数值时被调用。
onSuccess(XHR「equest,json)在请求完成且状态代码没有定义，或者状态代码介于200到 299之间时被调用。
onCoinplete(XHRrequest,json)在请求过程的最后被调用。
Prototype还提供了一个全局Ajax.Responders方法，用于控制和访问进进出出各种 Ajax.Request方法的Ajax请求。要了解有关Ajax.Responders方法的详细情况，请参考Prototype 的在线文档 

http://www.prototypejs.org/api/ajax/responders。
以下是使用Prototype发送Ajax请求的几个例子。
// Prototype Ajax•Request
//创建一个新的一次性请求并在成功时弹出消息 new Ajax.Request(
'some-server-side-script.php1,
{
method:1 get1，
onSuccess: function (transport) {
var response = transport.responseText || "no response text"; alert(fAjax.Request was successful: 1 + response);
h
onFailure: function (){ alert(^jax^Request failed');
}
)；} 、
// Prototype Ajax.Updater
// 创建一"一次性请求，以 responseText 来填充#ajax-updater-target 元素
new Ajax^Updater(
$(,ajax-updaterrtargetl),
^ome-server-side-script^php1,
{
- method: 1 get1>
//将其添加到目标元素的上部 insertion: Insertion•Top
>
)；
// Prototype Ajax.periodicalUpdater
//创建一个周期性的请求，每10秒钟自动填充一次#ajax-per1odic-target元素 new Ajax-PeriodicalUpdater(
$(’ajax轉periodic垂target
'some-server-side-script^php !>
{
method: ’GET、
//添加到现有内容的上方 insertion: Insertion•Top,
//每10秒钟运行一次

frequency: 10
A.6 Ajax 281
}
)；
Ajax.Request对象的另一个简单但却很给力的用法，是隔一段时间保存一次表单信息。这特 别适合在博客应用中解决用户临时保存数据的问题。使用Ajax.RequestO对象，再配合Prototype 的Form序列化方法，可以从表单中取得当前的信息，每隔几分钟就保存到服务器一次，从而保 证用户不会意外丢失已经花时间填写的内容。
//使用Prototype实现自动保存功能 //每30秒钟就保存一次#如1:〇$抑&1:〇〇11表单中的信息 //鲶后Mif^utosave-status元素标明更新状态 set!imeout(function() { new Ajax*Updater(
$('autosave-statusf),
’ some-server-side-autosave-script.php •，
{
method "post、	•
parameters : $(1 autosave-form1)•serialize(true)
}
)；
30000)；
A.6.2 jQuery 与 Ajax
为了比较语法上的异同，接下来看一看jQuery。jQuery也有一个低级的$.ajax方法，可以接
受各种属性。不过，还是先来看看它的那些简单易用的方法吧。
$.post(url, params, callback)通过 POST请求取得数据。
$.get(u「l，pa「ams, callback)通过GET请求取得数据。
$.getJSON(url, params, callback)取得JSON对象。
$.getScript(u「l, callback)取得并执行JavaScript文件。
这些方法实际上都是$.ajax()的包装方法，它们的回调方法总会被作为$.ajax()的成功回调方 法调用。每个回调方法都接受两个参数，分别是请求对象的响应文本（responseText)和状态 (status)：
$，get(’some-server-side-script•php_,
{ key: 'value1 },
function(responseText, status){
//你的代码
}
)；
状态是以下几个值之一：
success
error
notmodified
在使用getJSON和getScrlpt方法时响应会被求值，因此getJSON方法中传给回调的参数是一 个 JavaScript 对象。

282 附录 JavaScript 库
下面再给出几个使用上述方法的例子。
//使用$_get()实现快速的Ajax调用
//创建一个一次性的请求并在成功时弹出消息
$,get(,some-server-side-script.php,>
{ key: 'value1 }, function(responseText,status){
alert(!successful: 1 + responseText);
}
)；
//使用$.getJS0M()加栽JSON对象
//创建一个一次性的请求加载JSON文件并在成功时弹出消息 $.getDSONC1some-server-side-script,php', function(json){ alert(*successful: * + json.type);
});
jQuery还提供了一个load()方法：
□ $(express1on).load(url, params, callback)把URL的结果加载到相应的DOM元素中。 这个方法会以返回的结果自动填充相应的一个或多个元素：
//$(…）.load()用于自动填充元素
"创建一个一次性的请求，用responseText的内容填充#ajax-updater-target元素 $(,f#ajax-updater-target,!).load(
1 some-server-side-script^php1,
{ key: 'value1 }, function(responseText>status) { alert(*successful: 1 + responseText);
}
)；
Prototype的Ajax. update()方法与此也是类似的。
而且，也可以使用$()方法实现周期性的保存功能：
//使用jQuery实现自动保存功能	、
//每30秒钟保存一次#autosave-fomi表单的信息
//然后更新#3此05376*^31115元素标明更新状态 setTimeout(function() {
$('autosave-status1)*load(
1some-server-side-script*phpf,
$.param({
titie:$(_#autosave_form input[@name=title]’)，val(), story ^(^autosave-form textarea[@name=story]1 ).val()
})
)；
30000)；
jQuery 还有一些 Ajax 插件，例如 Mike Alsup 的 Ajax Form 插件（

http://plugins.jquery.com/) 就让处理表单和Ajax事件变得很容易。想要像第12章那样通过Ajax提交评论表单吗？就这么 简单：
$(,#commentForfn,)•ajaxForm(function() { alert(uThank you for your comment!n);
});
这个方法会将表单的内容序列化，然后将结果发送给表单的action属性中指定的脚本。

A.7 动画和效果	283
A.7动画和效果
到现在为止，我们已经知道使用库能完成很多DOM操作和脚本任务了。下面我们来享受一 些视觉上的冲击和交互效果。
有些库（如jQuery)会内置一些效果属性，而另一些库则会依赖插件来提供效果方法。如果 你选择的库没有效果方法，建议考虑一下Moo.fx和Script.aculo.us。
Moof.fx (

http://moofic.mad4miIk.net/)把自身描述为“一个超轻量、超小巧、超精简的 JavaScript效果库，可以配合prototype Js或mootools框架使用。”总的来说，Moo.fx的使 用还是非常方便的，它采用了一种低抽象度的方式，让你指出元素以及想要在给定的时 间间隔内修改哪个CSS属性。这些修改只会应用到特定的元素，不会应用到该元素的子 元素（除非子元素根据层叠规则会继承相应的CSS属性)。利用这些低抽象度的特性，不 用编写太多代码，就可以创造出几乎任何你能够想到的效果。
Script.aculo.us (http://script.aculo.us)呢，它“是一个好用、跨浏览器的 JavaScript用户
界面库，能够让你的网站和Web应用动起来。” Script.aculo.us采用的是一种高抽象度的 方式，提供了一些核心效果以及在此基础上的组合效果。在应用这些髙级效果的情况下， 指定元素的所有子元素可能也会受到影响。例如，在某个段落上调用Effect.Scale时，字 体的大小也会随着段落及其他子元素的宽度和高度的变化而同步缩放。这些高级效果的 组合让应用大型、复杂的效果变得比较简单，值得考虑。
以上这两个效果库都是构建在Prototype基础上的，Moo.fx也有基于MooTools库的版本 (

http://mootools.net/) 0
注意Moo.fx需要通过$()和$$()方法取得元素，因此再重申一次，如果你使用的是这个库，那 么就要在混合多个库时倍加小心。建议查看文档，采取最佳方式避免冲突。
A.7.1基于CSS属性的动画
动画的最基本形式，就是随着时间推移改变一个元素的CSS属性，比如下面这个我们在第 10章看到过的moveElement函数：
function moveElement(elementID,final_x,final_y^interval) { if (!document•getElementByld) return false; if (!document,getElementByld(elementlD)) return false; var elem = document.getElementByld(elementlD); if (elenMnovemerrt) { clearTimeout(elem^movement);
}
if (!elem晄tyle昹eft) { elem# style 昹eft = M〇pxir;
>
if (!elem.style.top) { elem ♦style 晅op =： _?〇px";

284 附录 JavaScript 库
var xpos = parselnt(elem^style.left); var ypos = parselnt(elem^style^top); var dist = 0；
if (xpos == final_x && ypos ==千inal_y) { return true;
} … if (xpos < 千inal_x) {
dist = Math^ceil((final_x - xpos)/l〇);
xpos = xpos + dist;
}
if (xpos > final_x) { dist = Math.ceil((xpos • final_x)/10); xpos = xpos - dist;
}
if (ypos < final一y) { dist = Math.ceil((final_y - ypos)/l〇); ypos = ypos + dist;
}
if (ypos > finally) { dist = Math*ceil((ypos - final_y)/i〇); ypos = ypos - dist;
}
elerru style • left = xpos + "px"; elem^style^top = ypos + ”px";
var repeat = "moveElement("’+elementID+ul,"++inal_x+","+final_y+n,’’+interval+")"; elenu movement = setTimeout(repeat,interval);
}
使用计时器和数学公式的问题在于，代码会在不知不觉中变得非常复杂冗长。好在jQuery 之类的库可以为我们提供很大的帮助。
上面这个moveElement函数是通过链接的鼠标事件触发的：
var links = list^getEleinentsByTagName(rta,1);
//为mouseover事件#加动画行为 links[〇]^onmouseover = function() { moveEiement(npre\/iewM,-100,0,10);
}
links[i].onmouseover = function() { moveEieinent(,f preview",-2〇〇,〇,i〇);
i
碡
links[2].onmouseover = function() { moveElement(f,previewu>-300^0,10)；
}
我们可以把moveElement相关的逻辑集中起来，通过jQuery的animate方法来为preview元素 应用位置动画。这个animate方法以CSS属性及最终值的列表作为参数，能够按照指定的时间间 隔从当前值开始修改相应的属性值。
$(la,)^each(function(i) { var preview = $(^preview1); var final_x = i * -100;
$(this)^mouseover(function(){ preview^animate({left:final_x}, 10);
})； '
});
这就比第10章的代码简单多了。使用jQuery只需几行代码，而且不必担心复杂的数学计算
和计时器问题。	-
当然，还不止于此，你还可以控制动画的变化过程。jQuery的animate方法为此还接受另一

A.7 动画和效果	285
个参数：
i(expression) .dir\imte( properties, duration, easing )
第三个参数easing是一个函数，用于计算动画在特定时间段内的速度。这些函数涉及的数学 计算有时候会非常复杂，但借助它们来改变速度却能创建出精彩的淡入淡出以及弹跳效果。 jQuery库中默认的缓动函数只有默认的swing和速度恒定的linear。
要想得到更多缓动函数，可以在jQuery UI套件（

http://jqueryui.com/)或jQuery缓动插件 (http://gsgd_co.uk/sandbox/jquery/easmg)中去找。
A.7.2组合动画
不少库都提供了一些组合动画，以方便幵发人员使用。例如，在不用插件的情况下，jQuery 提供了下列方法。	•
fadeln f卩 fadeOut。
fadeTo将匹配元素的不透明度调整到指定的值。
slIdeToggle、slIdeDown和slldeUp用“滑移动画”隐藏和显示匹配的元素。
其他库，比如Script.aculo.us，还提供了更多高级动画效果，比如下面这些。
Effect.Appear, Effect.Fade
Effect.Puff
Effect.DropOut
Effect.Shake
Effect.SwItchOff
Effeet • B1 彳 ndDown 和 Effeet • B11 ndUp
Effect. S11 deDown 和 Effeet. S11 dellp
Effect.Pul sate
Effect.Squish	,
Effect.Fold
Effect.Grow
Effect.Shrink
A.7.3注意可访问性
在使用恰当的情况下，微妙的梦果可以起到提示变更的作用。动画和效果也可以把人的注意 力吸引到界面的某个地方，从而引导交互顺利进行，或者只是让访客感到惊喜并给人留下难忘的 印象，为没有什么新意的HTML添加一点生命气息。
、	请注意，应用效果时要时刻提醒自己注意可访问性。看上去美不胜收的各种效果，如果影响
到访客顺利査看信息，恐怕就得不偿失了。

286 附录 JavaScript 库
A.8小结
在本附录中，我们探讨了为什么库能够帮我们简化日常的编程工作。篇幅所限，不可能面面 俱到地谈到所有库或者库的所有功能。为此，请感兴趣的读者自行査阅相关库的文档，从而全面 了解库的特点，作出正确的选择。
选择库的时候，一定要全面考察自己看中的每一个候选库。搞清楚如何处理库之间的冲突， 功能太少还是太多，有没有坚强的社区做后盾，或者说能否得到及时的技术支持。在选定了合适 的库以后，还要尽可能发挥出这个库的最大效用。与此同时，最好能够进一步理解库的工作原理。 依赖于库不要紧，关键是不要只停留在简单的使用这个表面上。

“本书不愧为经典，文笔清新，深入浅出，不知不觉让你掌握优秀的编程原则，明白为什么要遵守标准。”
Slashdot
“我要隆重推荐本书，它前所未有地演示了DOM脚本编程的真正潜力。无论你是JavaScript新手还是专家，本书都绝 对值得你拥有。”
	Garrett Dimon，Digital-Web.com杂志专栏作家
DOM Scripting
Web Design with JavaScript and the Document Object Model
Second Edition
JavaScript DOM编程艺术(第2版)
JavaScript是Web开发中最重要的一门语言，它强大而优美。无论是桌面开发，还是移动应用， JavaScript都是必须掌握的技术。W3C的D0M标准是开发Web应用的基石，已经得到所有现代浏览器的支 持，这使得跨平台Web开发成了一件轻松惬意的事。
本书是超级畅销书的升级版，由倡导Web标准的领军人物执笔，揭示了前端开发的真谛，是学习 JavaScript和D0M开发的必读之作。
本书在简洁明快地讲述JavaScript和D0M的基本知识之后，通过几个实例演示了专业水准的网页开发技 术，透彻阐述了平稳退化等一批至关重要的JavaScript编程原则和最佳实践，并全面探讨了 HTML5以及 jQuery等JavaScript库。读者将看到JavaScript、HTML5和CSS如何协作来创建易用的、与标准兼容的Web 设计，掌握使用JavaScript和DOM通过客户端动态效果和用户控制的动画来加强Web页面的必备技术，同 时，还将对如何利用库提高开发效率有全面深入的理解。