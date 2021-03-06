

## 31


<h1>第3章 DOM</h1>
<h2>3.1 文档：DOM中的“D”</h2>
<h2>3.2 对象：DOM中的“O”</h2>
<h2>3.3 模型：DOM中的“M”</h2>
<h2>3.4 节点</h2>
<h3>3.41 元素节点</h3>
<h3>3.42 文本节点</h3>
<h3>3.43 属性节点</h3>
<h3>3.44 CSS</h3>
<h3>3.45 获取元素</h3>
<h3>3.46 盘点知识点</h3>
<h2>3.5 获取和设置属性</h2>
<h3>3.51 getAttribute</h3>
<h3>3.52 setAttribute</h3>
<h2>3.6 小结</h2>



终于要与DOM面对面了。本章将介绍DOM,带领大家透过DOM去看世界。
<h3>3.1文档：DOM中的“D”</h3>
如果没有document (文档），DOM也就无从谈起。当创建了一个网页并把它加载到Web浏览 器中时，DOM就在幕后悄然而生。它把你编写的网页文档转换为一个文档对象。
在人类语言中，“对象”这个词的含义往往不那么明确，它几乎可以用来称呼任何一种东西。 但在程序设计语言中，“对象”这个词的含义非常明确。
<h3>3.2对象：DOM中的“0”</h3>
在上一章的末尾，我们向大家展示了几个JavaScript对象的例子。你应该还记得，“对象”是 一种自足的数据集合。与某个特定对象相关联的变量被称为这个对象的属性；只能通过某个特定 对象去调用的函数被称为这个对象的方法。
JavaScript语言里的对象可以分为三种类型。
口用户定义对象（user-definedobject):由程序员自行创建的对象。本书不讨论这种对象。 □内建对象（nativeobject):内建在JavaScript语言里的对象，如Array、Math和Date等。 口宿主对象（hostobject):由浏览器提供的对象。
即使是在JavaScript的最初版本里，对编写脚本来说非常重要的一些宿主对象就已经可用了， 它们当中最基础的对象是wl ndow对象。
window对象对应着浏览器窗口本身，这个对象的属性和方法通常统称为BOM (浏览器对象模 型），但我觉得称为Window Object Model (窗口对象模型）更为贴切。BOM提供了 wlndow.open 和wlndow.blur等方法，这些方法某种程度上要为到处被滥用的各种弹出窗口和下拉菜单负责。

<h3>3.3模型：DOM中的揗</h3>
难怪JavaScript会有一个不好的名声！
值得庆幸的是，我们不需要与BOM打太多的交道，而是把注意力集中在浏览器窗口内的网 頁内容上。document对象的主要功能就是处理网页内容。在本书的后续内容里，我们几乎只讨论 document对象的属性和方法。
现在，我们已经对DOM中的字母“D”（document，文档）和字母“0”（object,对象）做 了解释，那么字母“M”又代表着什么呢？
<h3>3.3模型：D〇M中的“M”</h3>
D0M中的“M”代表着“Model”（模型），但说它代表着“Map”（地图）也未尝不可。模 室也好，地图也罢，它们的含义都是某种事物的表现形式。就像一个模型火车代表着一列真正的 火车、一张城市街道图代表着一个实际存在的城市那样，DOM代表着加载到浏览器窗口的当前 网页。浏览器提供了网页的地图（或者说模型），而我们可以通过JavaScript去读取这张地图。
既然是地图，就必须有诸如方向、等高线和比例尺之类的图例。要想看懂和使用地图，就必 須知道这些图例的含义和用途，这个道理同样适用于D0M。要想从D0M获得信息，必须先把
各种表示和描述文档的“图例”弄明白。
D0M把一份文档表示为一棵树（这里所说的“树”是数学意义上的概念），这是我们理解和 运用这一模型的关键。更具体地说，D0M把文档表示为一棵家谱树。
家谱树本身又是一种模型。家谱树的典型用法是表示一个人类家族的谱系，并使用Parent (父)、child (子)、sibling (兄弟）等记号来表明家族成员之间的关系。家谱树可以把一些相当 复杂的关系简明地表示出来:一位特定的家族成员既是某些成员的父辈，又是另一位成员的子辈， 同时还是另一位成员的兄弟。
家谱树模型非常适合用来表示一份用(X)HTML语言编写出来的文档。 请看图3-1中这份非常基本的网页，它的内容是一份购物清单。
0〇@
Shopping list







.叫© c
What to buy
Don't forgei m buy this
(1)A tin of beam
(2)Milk
Done
图3-1

<!D0CTYPE html>
<html lang=lfenfl>
<head>
<meta charset=nutf-8n />
<title>Shopping list</title>
</head>
<body>
<hl>What to buy</hl>
<p title=!,a gentle reminder,l>Don,t forget to buy this stuffx/p> <ul id=_’purcfiases”>
<li>A tin o干 beans</li>
<li class=lfsalen>Cheese</li>
<li class=flsale important11 >Milk</li>
</ul>
</body>
</html>
这份文档可以用图3-2中的模型来表示。



图 3-2
现在我们来分析一下这个网页的结构，了解它的构成，看看它为什么那么适合用前面提到的 模型表示。DOCTYPE之后，一个打开了的<html>标签标识整个文档的开始，这个网页里的所有 其他元素都包含在这个元素里，这表示它至少是一个父亲（parent)。又因为所有其他的元素都 包含在其内部，所以这个<_1>标签既没有父亲，也没有兄弟。如果这是一棵真正的树，这个<html> 如签就是树根。
根元素是html。不管从哪个角度看，html都代表整个文档。
接下来深入一层，我们发现有<1^3(1>和4〇办>两个分支。它们位于同一层次且互不包含，所 以它们是兄弟关系。它们有着共同的父元素但又各有各的子元素，所以它们本身又是其 他一些兀素的父兀素。
<head>元素有两个子元素：<meta^p<t1tle> (这两个元素是兄弟关系）。<body>元素有三个子 元素：<hl>、<卩>和<1!1> (这三个元素是兄弟关系）。继续深入下去，我们发现<ul>也是一个父元

素，它有二个子兀素，它们都是<11>兀素，有一些class属性。
3.4 节点 35
利用这种简单的家谱关系记号，我们可以把各元素之间的关系简明清晰地表达出来。例如， <W>和<ul>之间是什么关系？答案是它们是兄弟关系。那么<1)〇(^>和<1|1>之间又是什么关系？ <^办>是<111>的父元素，<ul>是<1)0(^>的一个子元素。
如果你能把一个文档的各种元素想象成一棵家谱树，我们就可以用同样的术语描述DOM。 不过，与使用“家谱树”这个术语相比，把文档称为“节点树”更准确。
<h3>3.4节点</h3>
节点（node)这个词是个网络术语，它表示网络中的一个连接点。一个网络就是由一些节点 均成的集合。
在现实世界里，一切事物都由原子构成。原子是现实世界的节点。但原子本身还可以进一步 分解为更细小的亚原子微粒。这些亚原子微粒同样也被当成是节点。
DOM也是同样的情况。文档是由节点构成的集合，只不过此时的节点是文档树上的树枝和 树叶而已。
在DOM里有许多不同类型的节点。就像原子包含着亚原子微粒那样，也有很多类型的DQM 节点包含着其他类型的节点。接下来我们先看看其中的三种：元素节点、文本节点和属性节
O	r.
□元素节点
DOM的原子是元素节点（elementnode)。
在描述刚才那份“购物清单”文档时，我们使用了诸如<body>、<卩>和<1(1>之类的元素。如果 茫Web上的文档比做一座大厦，元素就是建造这座大厦的砖块，这些元素在文档中的布局形成 了文档的结构。
标签的名字就是元素的名字。文本段落元素的名字是“P”，无序清单元素的名字是“ul”， 列表项元素的名字是“11”。
元素可以包含其他的元素。在我们的“购物清单”文档里，所有的列表项元素都包含在一个 无序清单元素的内部。事实上，没有被包含在其他元素里的唯一元素是<html>元素，它是我们的 f点树的根元素D
3.4.2文本节点
元素节点只是节点类型的一种。如果一份文档完全由一些空白元素构成，它将有一个结构， 但这份文档本身将不会包含什么内容。在内容为王的互联网上，绝大多数内容都是由文本提供的。
在“购物清单”例子里，<P>元素包含着文本“Don’t forget to buy this stuff•”。它是一个文本 爷点(text node) 〇
在XHTML文档里，文本节点总是被包含在元素节点的内部。但并非所有的元素节点都包含

36 第3章DOM
有文本节点。在“购物清单”文档里，<ul>元素没有直接包含任何文本节点，它包含着其他的元〕
素节点（一些<li>元素），后者包含着文本节点。
3.4.3属性节点
属性结点用来对元素做出更具体的描述。例如，几乎所有的元素都有一个title属性，而我 1
们可以利用这个属性对包含在元素里的东西做出准确的描述：

在 DOM 中，title^a gentle renrinder"是一个属性节
点（attribute node)，如图3_3所示。因为属性总是被放在
起始标签里，所以属性节点总是被包含在元素节点中。并
非所有的元素都包含着属性，但所有的属性都被元素包含。
在前面的“购物清单”示例文档里，可以清楚地看到那
个无序清单元素（<ul>)有个Id属性。有些清单元素（<11>)
有class属性。如果曾经用过CSS，你对Id和class之类卜
的属性应该不会感到陌生。不过，为了照顾那些对CSS还
不太熟悉的读者，我们下面将简要地重温几个最基本的CSS
概念。
3.4.4 CSS
DOM并不是与网页结构打交道的唯一技术。我们还可以通过CSS (层叠样式表）告诉浏览
器应该如何显示一份文档的内容。
类似JavaScript脚本，对样式的声明既可以嵌在文档的<head>部分（<style>#签之间），也可
以放在另外一个样式表文件里（参见第4章)。CSS声明元素样式的语法与JavaScript函数的定义
语法很相似：
selector {
property: value;
}
在样式声明里，我们可以定义浏览器在显示元素时使用的颜色、字体和字号，如下所为
p {
color: yellow;
font-family: "narial", sans-serif;
font-size: l^2em;
>
继承（inheritance)是CSS技术中的一项强大功能。类似于DOM，CSS也把文档的内容视
为一棵节点树。节点树上的各个元素将继承其父元素的样式属性。
例如，如果我们为body元素定义了一些颜色或字体，包含在body元素里的所有元素都将自
属性节点
动获得那些样式:

3.4 节点 37
body {
color: white; background-color:, black;
这些颜色将不仅作用于那些直接包含在<body>标签里的内容，还将作用于嵌套在body元素内 部的所有元素。
图3-4是把刚才定义的样式应用在“购物清单”示例文档上后得到的网页显示效果。
图 3-4	，
在某些场合，当把样式应用于一份文档时，我们其实只想让那些样式作用于某个特定的元素。 例如，我们只想让某一段文本变成某种特殊的颜色和字体，但不想让其他段落受到影响。为了获 得如此精细的控制，需要在文档里插入一些能够把这段文本与其他段落区别开来的特殊标志。 为了把某一个或某几个元素与其他元素区别开来，需要使用class属性或Id属性。
1_ cl ass属性
你可以在所有的元素上任意应用class属性：
<p class=Hspecial">This paragraph has the special class</p>
<h2 class="special">So does this headline</h2>
在样式表里，可以像下面这样为class属性值相同的所有元素定义同一种样式：
•special { font-style: italic;
>
还可以像下面这样利用class属性为一种特定类型的元素定义一种特定的样式：
h2.special {
text-transform: uppercase;
}
□id属性
id属性的用途是给网页里的某个元素加上一个独一无二的标识符，如下所示：
#
<ul id=_’purchases’’>
在样式表里，可以像下面这样为有特定Id属性值的元素定义一种独享的样式：
#purchases {
border: lpx solid white;

background-color: #333； color: #ccc; padding: lem;
尽管Id本身只能使用一次，样式表还是可以利用Id属性为包含在该特定元素里的其他元素定 义样式。
#purchases li { font-weight: bold;
图3-5是把刚才利用Id属性定义的样式应用在“购物清单”示例文档上而得到的网页显示效果。
0 〇 〇	SHcppiil0 hsi
\ t
What to buy
Don't forget to buy this stuff.
• A ifti «)f fmma ^ Milk
图3-5
Id属性就像是一个挂钩，它一头连着文档里的某个元素，另一头连着CSS样式表里的某个 样式。DOM也可以使用这种挂钩。
315获取元素
秦
有3种DOM方法可获取元素节点，分别是通过元素ID、通过标签名字和通过类名字来获取。 1. getElementByld
DOM提供了一个名为getElementByld的方法，这个方法将返回一个与那个有着给定"id属性 值的元素节点对应的对象。请注意，JavaScript语言区分字母大小写，所以在写出“getElementByld” 时千万不要把大小写弄错了。如果把它错写成“GetElementByld”或“getElementbyid”，你都得 不到正确的结果。
它是document对象特有的函数。在脚本代码里，函数名的后面必须跟有一对圆括号，这对圆 括号包含着函数的参数。getElementByld方法只有一个参数：你想获得的那个元素的Id属性的值, 这个Id值必须放在单引号或双引号里。
document.getElementByld(id)
下面是一个例子：
doamierrLgetElementByIcl( "purchases”）



3.4 节点 39
这个调用将返回一个对象，这个对象对应着document对象里的一个独一无二的元素，那个元 素的HTML Id属性值是purchases。你可以用typeof操作符来验证这一点。typeof操作符可以告
诉我们它的操作数是一个字符串、数值、函数、布尔值还是对象。
下面是把一些JavaScript语句插入到前面给出的“购物清单”文档之后得到的一份代码清单, 新增的代码(黑体字部分)出现在</body>结束标签之前。顺便说一句，我本人并不赞成把JavaScript 代码直接嵌入文档，但这确实是一种简便快捷的测试手段：
<!D0CTYPE html>
<html lang=nenn>
<head>
<meta charset=lfutf-8f, />
<title>Shopping list</title>
</head>
<body>
<hl>What to buy</hl>
<p title=Ha gentle reminder11 >Donft forget to buy this stuf干•<々>
<ul id=npurchasesH>
<li>A tin of beans</li>
<li class=f,salefr>Cheese</li>
<li class=ffsale importantn>Milk</li>
</ul>
<script>
alert(typeof document.getElementById(MpurchasesM));	•
</script>
</body>
</html>
把上面这些代码保存为一个XHTML文件。当在Web浏览器里加载这个XHTML文件，会 募出一个如图3-6所示的alert对话框，它向你们报告document.getElementByld rpurchases")的
类型——它是一个对象。
00 Q



图3-6
事实上，文档中的每一个元素都是一个对象。利用DOM提供的方法能得到任何一个对象。 一般来说，用不着为文档里的每一个元素都定义一个独一无二的Id值，那也太小题大做了。DOM 是供了另一个方法来获取那些没有Id属性的对象。
2. get Element sByTagName
getElementsByTag_e方法返回一个对象数组，每个对象分别对应着文档里有着给定标签的一

个元素。类似于getElementByld，这个方法也是只有一个参数的函数，它的参数是标签的名字：
elefnent - get Element s ByTagName (tag)
它与getElementByld方法有许多相似之处，但它返回的是一个数组，你在编写脚本时千万注
意不要把这两个方法弄混了。
下面是一个例子：
document •getElementsByTagName(ffliH)
这个调用将返回一个对象数组，每个对象分别对应着document对象中的一个列表项元素。与 任何其他的数组一样，我们可以利用length属性査出这个数组里的元素个数。
首先，在上一小节给出的XHTML示例文档里把<script>#签中的alert语句替换为下面这
条语句：
alert (document •getElemerrtsByTagNamef’li"^ length);
你会看到这份示例文档里的列表项元素的个数：3。这个数组里的每个元素都是一个对象。 可以通过利用一个循环语句和typeof操作符去遍历这个数组来验证这一点。例如，你可以试试下 面这个f〇「循环：
for (var i=〇; i < document.getElementsByTagName(,fli!l).length; i++) { alert(typeo千 doamien1^getElemervtsByTagName(’’li’’）[i]);
}
请注意，即使在整个文档里这个标签只有一个元素，getElementsByTagName也返回一个数组。 此时，那个数组的长度是1。
你或许已经开始觉得用键盘反复敲入(docurnent.getElementsByTagNameni)是件很麻烦的事
情，而这些长长的字符串会让代码变得越来越难以阅读。有个简单的办法可以减少不必要的打字 量并改善代码的可读性：只要把document.getElementsByTagName("11n")赋值给一个变量即可。
请把<sc「1卩1>标签中的al ert语句替换为下面这些语句：
```
var items = documents get ElementsByTagName(l,li,f); 
for (var i=0; i < items.length; i) 
{ alert(typeof itemsfi]);
} 
```
现在，你将看到三个alert对话框，显示的消息都是“object”。
getElementsByTagName允许把一个通配符作为它的参数，而这意味着文档里的每个元素都将在 这个函数所返回的数组里占有一席之地。通配符（星号字符“*”）必须放在引号里，这是为了让 通配符与乘法操作符有所区别。如果你想知道某份文档里总共有多少个元素节点，像下面这样使 用通配符即可：
alert (document •getElementsByTagName(ll*n) .length);
还可以把getElementByld和getElementsByTagMame结合起来运用。例如，刚才给出的几个例子 都是通过document对象调用getElementsByTagName的，如果只想知道Id属性值是purchase的元素 包含着多少个列表项，必须通过一个更具体的对象去调用这个方法，如下所示：

3.4 节点 41
var shopping = document•getElementById(!,purchasesn); var items = shopping.getElementsByTagName(H*,f);
在这两条语句执行完毕后，Items数组将只包含Id属性值是purchase的无序清单里的元素。 具体到这个例子，Items数组的长度刚好与这份文档里的列表项元素的总数相等：
alert (items•length);
如果还需要更多的证据，下面这些语句将证明Items数组里的每个值确实是一个对象：
for (var i=〇; i < items•length; i++) { alert(typeof itemsfi]);



□getEl ementsByCl assName
HTML5 DOM (h郎://

www.whatwg.org/specs/web-apps/current-work/)中新增了一个令人期待 已久的方法：getElementsByClassName。这个方法让我们能够通过class属性中的类名来访问元素。 不过，由于这个方法还比较新，某些D0M实现里可能还没有，因此在使用的时候要当心。下面 我们先来看一看这个方法能帮我们做什么，然后再讨论怎么可靠地使用该方法。
与getEl ementsByTagName方法类似，getEl ementsByCl assName也只接受一个参数，就是类名：
getElementsByClassName(c2ass)
0
这个方法的返回值也与getElementsByTagName类似，都是一个具有相同类名的元素的数组。 下面这行代码返回的就是一个数组，其中包含类名为"sale"的所有元素：
document •getElementsByClassName(llsalefr)
使用这个方法还可以査找那些带有多个类名的元素。要指定多个类名，只要在字符串参数中 用空格分隔类名即可。例如，在<script>标签中添加下面这行alert代码：
alert(document^getElementsByClassName(11 important sale11).length);
你会看到警告框中显示1，表示只有一个元素匹配，因为只有一个元素同时带有"important" 和"sale”类名。注意，即使在元素的class属性中，类名的顺序是"sale import"而非参数中指定的 •import sale"，也照样会匹配该元素。不仅类名的实际顺序不重要，就算元素还带有更多类名也 没有关系。
与使用 getElementsByTagName—样，也可以组合使用 getElementsByClassName 和 getElementBy Id。
如果你想知道在Id为"purchases"的元素中有多少类名包含”sale"列表项，可以先找到那个特定的 对象，然后再调用 getElementsByClassName:
var shopping = document^getElementById(npurchasest!); var sales = shopping.getElementsByClassName(l,sale11);
这样，sales数组中包含的就只是位于"purchases"列表中的带有"sale"类的元素。运行下面这 行代码，就会看到sales数组中包含两项：
alert (sales•length);
这个getElementsByClassName方法非常有用，但只有较新的浏览器才支持它。为了弥补这一 不足，D0M脚本程序员需要使用已有的D0M方法来实现自己的getElementsByClassName，有点像

是成人礼似的。而多数情况下，他们的实现过程都与下面这个getElementsByClassName大致相似， 这个函数能适用于新老浏览器：
function getElementsByClassName(node, classname) {
if (node^getElementsByClassName) {
//使用现有方法
return node^getElementsByClassName(classname);
} else {
var results = new Array();
var elems = node^getElementsByTagName(n*l!);
for (var i=〇; i<elems^length; i++) {
if (elems
results
；i].className*indexOf(classname) ；results.length] = elems[i];
-1) {
return results
这个getElementsByClassName函数接受两个参数。第一个node表示DOM树中的搜索起点， 第二个classname就是要捜索的类名了。如果传入节点上已经存在了适当的getElementsByClassName 函数，那么这个新函数就直接返回相应的节点列表。如果getElementsByClassName函数不存在， 这个新函数就会循环遍历所有标签，査找带有相应类名的元素。（这个例子不适用于多个类名。） 如果使用这个函数来模拟前面取得购物列表的操作，就可以这样写：
var shopping = document^getElementById(,,purchasesT!); var sales = getElementsByClassName(shopping, nsalef?);
当然，捜索匹配的DOM元素的方法有很多，但真正高效的却不多，有兴趣的读者可以参考 Robert Nyman 的文章	所ate g故五/e所办

http://robertnyman.com/2008/05/27/the-
ultimate-getelementsbyclassname-anno-2008) 0
第5章将继续讨论类似的支持性问题，以及如何解决这些问题。第7章将更详细地探讨DOM 操作方法。
3.4.6盘点知识点
你一定已经厌倦了看那么多遍显示着单词“object”的alert对话框。你一定已经明白：文档 中的每个元素节点都是一个对象。不仅如此，这些对象中的每一个还天生具有一系列非常有用的 方法，这要归功于DOM。利用这些预先定义好的方法，我们不仅可以检索出文档里任何一个对 象的信息，甚至还可以改变元素的属性。
下面是对本章此前学习内容的一个简要总结。
□一份文档就是一棵节点树。
口节点分为不同的类型：元素节点、属性节点和文本节点等。
(2)getElementByld将返回一个对象，该对象对应着文档里的一个特定的元素节点。
(3)getElementsByTagName和getElementByclassName将返回一个对象数组，它们分别对应着文
档里的一组特定的元素节点。
□每个节点都是一个对象。
接下来介绍节点对象的属性和方法。
<h3>3.5获取和设置属性</h3>
至此，我们已经介绍了 3种获取特定元素的方法:分别是getEl ementBy Id，getEl ementsByTagName 茜getElementBy
<h3>3.6小结</h3>
ClassName。得到需要的元素以后，我们就可以设法获取它的各个属性。getAttn'bute 方法就是用来做这件事的。相应地，setAttrlbute方法则可以更改属性节点的值。
3.5.1 getAttribute
getAttri bute是一个函数。它只有一个参数	你打算査询的属性的名字：
object .getl\ttxibute(attribute)
与此前我们介绍过的那些方法不同，getAttribute方法不属于document对象，所以不能通过 Jocinent对象调用。它只能通过元素节点对象调用。例如，可以与getElementsByTagName方法合用， 获取每个<p>元素的title属性，如下所示：
var paras = document.getElefnentsByTagName(np");	，
for (var i=〇; i < paras•length; i++ ) { alert(paras[i]^getAttribute(,ftitle,f));
}
把上面这段代码放到前面给出的“购物清单”文件的末尾，然后在Web浏览器里重新加载 这个页面，屏幕上将弹出一个显示着文本消息“a gentle reminder”的alert对话框。
在“购物清单”文件里只有一个<P>元素，并且它有title属性。假如这份文档有更多个<p> 元素，并且它们没有title属性，贝ljgetAttribute("t1tle")方法会返回null值。在JavaScript里，
mil的含义是“没有值”。把下面代码添加到“购物清单”文件中的现有<P>标签之后：
<p>This is just a test</p>
重新加载这个页面。这一次，你将看到两个alert对话框，而第二个对话框将是一片空白或 者是只显示着单词“mill”，这取决于你使用是哪种Web浏览器。
我们可以修改脚本，让它只在title属性有值时才弹出消息。我们将增加一条If语句来检查 getAttribute的返回值是不是null。趁着这个机会，我们顺便增加几个变量以提髙脚本的可读性。
var paras = document• getElementsByTagName(,rp,f); for (var i=〇; i< paras•length; i++) { var title一text = paras[i] ♦getAttribute(,ftitletf); if (title_text != null) { aiert(title一text);
} ~
}
现在重新加载这个页面，你会看到一个显示着“a gentle reminder”消息的alert对话框，如 图3-7所示。

44 第3章DOM
o o o .：

Wha
\ >



9«n^e reminder
Don*t fo?
This is just a test







我们甚至可以把这段代码缩得更短一些。当检查某项数据是否是null值时，我们其实是在 检查它是否存在。这种检査可以简化为直接把被检查的数据用作If语句的条件。If (something) 与If (something != null)完全等价，但前者显然更为简明。此时，如果something存在，则If语 句的条件将为真；如果something不存在，则If语句的条件将为假。
具体到这个例子，只要我们把If (tniejext != null)替换为彳f (tniejext)，我们就可以 得到更简明的代码。此外，为了进一步增加代码的可读性，我们还可以趁此机会把alert语句与 If语句写在同一行上，这可以让它们更接近于我们日常生活中的英语句子：
var paras = document.getElementsByTagName(Hpn); for (var i=〇; i< paras•length; i++) { var title_text = paras[i]^getAttribute(ntitleM); if (title_text) alert(titlejtext);
3.setAttribute
此前介绍的所有方法都是用来获取信息。setAttributeO有点不同：它允许我们对属性节点的 值做出修改。与getAttribute—样，setAttribute也只能用于元素节点：
object .setMtxibute(attribute, value)
在下面的例子里，第一条语句得到Id是purchase的元素，第二条语句把这个元素的title 属性值设置为a list of goods:
var shopping = docufnent^getElementById(npurchasesM); shopping.setAttribute(,,title,,/,a list of goods'1);
我们可以利用getAttribute来证明这个元素的title属性值确实发生了变化：
var shopping = document•getElementById(npurchases!,);
alert(shopping,getAttribute("title"));
shoppingssetAttribute(,'title''/'a list of goods11);
alert (shopping, getAttribute( "title”)；	、
加载页面后将弹出两个alert对话框：第一个alert对话框出现在setAttribute被调用之前， 它将是一片空白或显示单词“null”；第二个出现在设置title属性值之后，它将显示“a list of