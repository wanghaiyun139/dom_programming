# JavaScript Dom编程艺术


<h1>第9章 CSS-DOM</h1>
## 91
<h2>9.1 三位一体的网页</h2>
## 911
<h3>9.11 结构层</h3>
## 912
<h3>9.12 表示层</h3>
## 913
<h3>9.13 行为层</h3>
## 914
<h3>9.14 分离</h3>
## 92
<h2>9.2 style属性</h2>
## 921
<h3>9.21 获取样式</h3>
## 922
<h3>9.22 设置样式</h3>
## 93
<h2>9.3 何时该用DOM脚本设置样式</h2>
## 931
<h3>9.31 根据元素在节点树里的位置来设置样式</h3>
## 932
<h3>9.32 根据某种条件反复设置某种样式</h3>
## 933
<h3>9.33 响应事件</h3>
## 94
<h2>9.4 className属性</h2>
## 95
<h2>9.5 小结</h2>


9.1三位一体的网页
我们在浏览器里看到的时页其实是由以下三层信息构成的一个共同体：
□结构层 a表示层 □行为层
9.1.1结构层
网页的结构层（structural layer)由HTML 或XHTML之类的标记语言负责创建。标签 (tag)，也就是那些出现在尖括号里的单词，对 网页内容的语义含义做出了描述，例如，<p>标 签表达了这样一种语义：“这是一个文本段。” (如图9-1所示。）但这些标签并不包含任何关于 内容如何显示的信息。
<p>An example of a paragraph</p>
9_1 _2表不层

：*»	**r	-v«v ^w v»

m

An exampte of a pmgi^ph
_ ▼!0
r-ryr ^岭—冷说vyw.



图 9-1
表示层（presentation layer)由CSS负责完成。CSS描述页面内容应该如何呈现。你可以



9.1 三位一体的网页 149
…样一个CSS来声明:
图9-2所示。
“文本段应该使用灰色的Arial字体和另外几种scan-serif字体来显示。
P {
color: grey;
font-family: "Arial"， sans-serif;



9.1.3行为层
行为层（behavior layer)负责内容应该如何响应事件这一问题。这是JavaScript语言和DOM 主宰的领域。例如，我们可以利用DOM实现这样一种行为：“当用户点击一个文本段时，显示 卜个alert对话框。”如图9-3所示。
var paras = document•getElementsByTagName(l,pt,); for (var i=0; i<paras•length; i++) { paras[i].onclick = function() { alert(,!You clicked on a paragraph/1);



图 9-3

150 第 9 章 CSS-DOM
网页的表示层和行为层总是存在的，即使未明确地给出任何具体的指令也是如此。此时 Web浏览器将应用它的默认样式和默认事件处理函数。例如，浏览器会在呈现“文本段”元素| 留出页边距；当用户把鼠标指针悬停在某个元素的上方时，有些浏览器会弹出一个显示着该元： 的title属性值的提示框，等等。
9-1.4分离
在所有的产品设计活动中，选择最适用的工具去解决问题是最基本的原则。具体到网页设 工作，这意味着：
□使用(X)HTML去搭建文档的结构；
□使用CCS去设置文档的呈现效果；
口使用DOM脚本去实现文档的行为。
不过，在这三种技术之间存在着一些潜在的重叠区域，你也已见过这样的例子。用DOM 以改变网页的结构，诸如createElement和appendChlld之类的DOM方法允许你动态地创建和]
加标记。	分
在CSS上也有这种技术相互重叠的例子。诸如:hover和:focus之类的伪类允许你根据用户鲅j 发事件改变元素的呈现效果。改变元素的呈现效果当然是表示层的“势力范围”，但响应用户餘I 发的事件却是行为层的领地。表示层和行为层的这种重叠形成了一个灰色地带。
没错，CSS正在利用伪类走进DOM的领地，但DOM也有反击之道。你可以利用DOM 式给元素设定样式。
style 属性
文档中的每个元素都是一个对象，每个对象又有着各种各样的属性。有一些属性告诉我们： 素在节点树上的位置信息。比如说，parentNode、netxtS^ibllng、prevlousSibllng、chlldNodes、
flrstChlld和lastChlld这些属性，就告诉了我们文档中各节点之间关系信息。
其他一些属性（比如nodeType和nodeName属性）包含元素本身的信息。比如说，对某个元素丨 的nodeName属性进行的査询将返回一个诸如“p”之类的字符串。
除此之外，文档的每个元素节点还都有一个属性style。style属性包含着元素的样式，査^ 这个属性将返回一个对象而不是一个简单的字符串。样式都存放在这个style对象的属性里：
element•style•property
下面是一个内嵌样式的元素的例子：
<p id=nexafnple" style=ucolor: grey; font-family: •Arial1,sans-serif;11 >
An example of a paragraph
</p>
利用style属性，你可以得到这个<p>标签的样式。
首先，需要从文档里把这个元素找出来。我已经给这个<P>标签设置了一个独一无二的Id值丨 example。只需把这个Id值传递给getElementByld方法，再把这个方法的返回值赋值给变量pa「a,

9.2 style 属性 151
就可以通过para变量引用这个p元素了 ：
var para = document.getElementByld("example");
在拿到这个元素的样式之前，我想先向大家证明一下style属性确实是一个对象。这可以利 用关键字typeof来验证。下面，我们来对比一下style属性与nodeName属性的typeof结果。
把下面这些XHTML代码写入文件example.html，然后把这个文件加载到浏览器里：
<!D0CTYPE html>
<html>
<head>
<meta charset="utf-8" />
<title>Example</title>
<script>
window^onload = function() { var para = document*getElementById(nexaniple,f);
alert(typeof para^nodeName);	_
alert(typeof para♦style);
}
</script>
</head>
<body>
<p id=nexampleu style="color: grey; font-family: fArialf,sans-serif;11 >
An example of a paragraph
</p>
</body>
</html>
第一条alert语句将返回字符串“string”，因为nodeName属性是一个字符串（如图9-4所示)。 第二条alert语句将返回字符串“object”，因为style属性是一个对象（如图9-5所示)。



图 9-4	图 9-5
也就是说，不仅文档里的每个元素都是一个对象，每个元素都有一个style属性，它们也是 一个对象。
9.2.1获取样式
你能够得到para变量所代表的<p>标签的样式。为了查出某个元素在浏览器里的显示颜色，



152 第 9 章 CSS-DOM
我们需要使用style对象的color属性：
element♦style•color
下面这条alert语句告诉我们style对象（这个对象是para元素的属性）的colo「属性:
alert(._The color is " + para • style •color);
这个元素的style属性的colo「属性是“grey”（如图9-6所示)。




图 9-6
刚才的代码中还设置了<p>元素的另一个CSS属性font-fanrily。这个属性的获取方式与color 属性略有不同。你不能简单地査询style对象的font-family，因为“font”和“family”之间的连 字符与JavaScript语言中的减法操作符相同，JavaScript会把它解释为减号。如果像下面这样去访 问名为font-family的属性，就会收到一条出错信息：
element.style•font-family
JavaScript将把减号前面的内容解释为“元素的style属性的font属性”，把减号后面的内容 解释为一个名为family的变量，把整个表达式解释为一个减法运算。这完全违背了我的本意！
减号和加号之类的操作符是保留字符，不允许用在函数或变量的名字里。这同时意味着它们 也不能用在方法或属性的名字里（别忘了，方法和属性其实是关联在某个对象上的函数和变量)。
当你需要引用一个中间带减号的CSS属性时，DOM要求你用驼峰命名法。CSS属性 font-famlly 变为 DOM属性 fontFanrily:
element.style•fontFamily
为了査看para元素的style属性的fontFamlly属性， 语句：
在 example
html
文件里增加一条
alert
<!D0CTYPE html>
<html lang=flenM>
<head>
<meta charset=nutf-8n />

9.2 style 属性 153
<title>Example</title>
<script>
window*onload « function() { var para = document.getElementById(11 example11); alert(flThe font family is n + para^style^fontFamily);
}
</script>
</head>
<body>
<p id=,,exampletl style=Mcolor: grey; font-family: 1 Arial1,sans-serif; lf>
An example of a paragraph
</p>
</body>
</html>
在浏览器里重新加载example.html文件将能看到如图9-7所示的结果。



图 9-7
DOM属性fontFamlly的值与CSS属性font-family的值是一样的。具体到这个例子，它是:
'Arial1,sans-serif
不管CSS样式属性的名字里有多少个连字符，DOM—律采用驼峰命名法来表示它们。CSS 属性 background-colo「对应着 DOM属性 backgroundColor，CSS 属性 font-weight 对应着 DOM属 性 fontWelght，DOM 属性 marglnTopWldth 对应着 CSS 属性 margin-top-width。
DOM在表示样式属性时采用的单位并不总是与它们在CSS样式表里的设置相同。
在示例的<P>元素里，CSS属性color的设置值是单词“grey”，用JavaScript代码检索出来的 DOM col or属性的值也是“grey”。现在，把这个col or属性修改为十六进制值#999999:
<p id=nexamplef, style^?lcolor: #999999； font-family: fArialf,sans-serifH>
再在JavaScript代码里加上一条alert语句输出DOM里的colo「属性：
alert("The color is ’’ + para^style^color);
在某些浏览器里，colo「属性以RGB (红，绿，蓝）格式的颜色值(153,153,153)返回，如图
9-8所示。

154 第 9 章 CSS-DOM



图 9-8
还好，这类例外情况并不多。绝大部分样式属性的返回值与它们的设置值都采用同样的计量 单位。如果我们在设置CSS font-size属性时以em为单位，相应的DOM fontSIze属性也将以em 为单位：
<!D0CTYPE html>
<html lang=nen">
<head>
<meta charset>"utf-8” />
<title>Example</title>
<script>
window.onload = function() {	^
var para = docufnent.getElementById(!,exampleH); alert(,fThe font size is M + para^style^fontSize);
</script>
</head>
<body>
<p id="example" style=”color: grey; font-family: ’Arial’,sans-serif; ^ font-size: lem;11 >
An example of a paragraph
</p>
</body>
</html>
如图9-9所示，DOM fontSIze属性的确也是以em为单位的。



；： ；rr： -
图9-9
如果CSS font-size属性的值是lem，DOM fontSIze属性的返回值就将是lem。如果CSS

9,2 style 属性 155
it-slze属性的值是12px，DOMfontSIze属性的返回值就将是12px。
使用CSS速记属性，你可以把多个样式组合在一起写成一行。比如说，如果声明了 font: 12px •AriaV, sans-serif，CSS font-size属性将被设置为 12px，CSS font-family 属性将被设置为• AriaV, ns-serif：	.
<p id=nexample" style="color: grey; font: I2px rArial!,sans-serif;M>
DOM能够解析像font这样的速度属性。如果査询fontSIze属性，将得到一个12px的值：
alert(,fThe font size is " + para• style,fontSize);
如图9-10所示，DOM fontSIze属性的确也是以px为单位的。



内嵌样式
通过styl e属性获取样式有很大的局限性。
style属性只能返回内嵌样式。换句话说，只有把CSS style属性插入到标记里，才可以用 DOM styl e属性去査询那些信息：
<p id=’丨example" style=flcolor: grey; font: I2px _Arial、sans-serif;">
这可不是使用样式的好办法一表现信息与结构混杂在一起了。更好的办法是用一个外部样 式表去设置样式：
p#example { color: grey;
font: l2px ^rial1^ sans-serif;
}
把上面这段CSS代码存入文件styles.css。然后，从example.html文件里把内嵌在HTML代 码里的样式删掉，只保留以下内容：
<p id="example">
An example of a paragraph
</p>
在example.html文件的开头部分加上一个link元素并让它指向styles.css文件：
<link rel=frstylesheetN media=Mscreenlf href="styles/styles.css•’ />

156 第 9 章 CSS-DOM	
样式还像以前那样作用到了 HTML内容上，但与使用style属性不同，来自外部文件 styles.css的样式已经不能再用DOM style属性检索出来了。
alert(lfThe font size is tf + para.style.fontSize);
DOM style属性不能用来检索在外部CSS文件里声明的样式，如图'll所示。



图 9-11
如果把样式添加在example.html文件<head>部分的<st/le>标签里，你将看到相同的结果：
<style> p#example { color: grey;
font: I2px ^Arial、sans-serif;
</style>
DOM style属性提取不到如此设置的样式。
在外部样式表里声明的样式不会进入style对象，在文档的<head>部分里声明的样式也是如 此。
style对象只包含在HTML代码里用style属性声明的样式。但这几乎没有实用价值，因为 样式应该与标记分离开来。
现在，你或许会认为用DOM去处理CSS样式毫无意义，但这里还有另一种情况可以让DO style对象能够正确地反射出我们设置的样式。你用DOM设置的样式，就可以用DOM再把它们 检索出来。
9.2.2设置样式
许多DOM属性是只读的——我们只能用它们来获取信息，但不能用它们来设置或更新信息 类似 prevlousSibllng、netxtSIbllng、pa「entNode、firstChlld和 lastGrild之类的属^性，它们在
收集一个元素在节点树上的位置信息时可以帮上大忙，但它们不能用来更新信息。
凡事无绝对，style对象的各个属性就都是可读写的。我们不仅可以通过某个元素的style 属性去获取样式，还可以通过它去更新样式。你可以用赋值操作来更新样式：
element•style♦property = value

9.2 style 属性 157
style对象的属性值永远是一个字符串。在example.html文件里写一些JavaScript代码覆盖那 些内嵌在标记里的CSS代码。比如说，把para元素对象的color属性设置为"black":
<!D0CTYPE html>
<html lang:’fen__>
<head>
<meta charset=nutf-8n />
<title>Example</title>
<script>
window.onload = function() { var para = document•getElementByld("example"); para•style•color = "black";
}
</script>
</head>
<body>
<p id=’_example11 style=ffcolor: grey; font-family: •Axial1,sans-serif;•’>
An example of a paragraph
</p>
</body>
</html>
color属性已经被变成了"black"，如图9-12所示。
style对象的属性的值必须放在引号里，单引号或双引号均可：
para•style*color = 'black1;
如果忘了使用引号，JavaScript会把等号右边的值解释为一个变量：
para•style♦color = black;	.
如果前面并未定义过变量black,则上面这行代码将无法工作。
用赋值操作符你可以设置任何一种样式属性，诸如font之类的速记属性也不例外：
para•style•font = "2em 'Times1,serifu;
上面这条语句将把fontSize属性设置为2em，把fontFamlly属性设置为'Times' serif，如 图9-13所示。
图 9-12	图 9-13
通过JavaScript代码设置样式并不难，我也给出了一些具体例子。不过或许应该先问问自己:

158 第 9 章 CSS-DOM
为什么要这么做？
9.3何时该用DOM脚本设置样式
你已经看到，用DOM设置样式是多么容易，但你能做什么事并不意味着你应该做什么事。 在绝大多数场合，还是应该使用CSS去声明样式。就像你不应该利用DOM去创建重要的内容那 样，你也不应该利用DOM为文档设置重要的样式。
不过，在使用CSS不方便的场合，还是可以利用DOM对文档的样式做一些小的增强。
9.3.1根据元素在节点树里的位置来设置样式
通过CSS声明样式的具体做法主要有三种。第一种是为标签元素（比如p元素）统一地声明 样式，如下所示：
P {
font-size: lem;
第二种是为有特定class属性的所有元素统一声明样式，如下所示：
•fineprint { font-size: Jem;
第三种是为有独一无二的Id属性的元素单独声明样式，如下所示：
#intro {
font-size: l^2em;
也可以为有类似属性的多个元素声明样式，如下所示：
input[type*="textn] {
font-size:l^2em;
在现代浏览器中，甚至可以根据元素的位置声明样式：	-
p:first-of-type {
font-size:2em;
font-weight:bold;
CSS2引入了很多与位置相关的选择器，例如:f1rst-child和:last-ch11d，而CSS3则定义 诸如:nth-chlldO和:nth-of-type()之类的位置选择器。尽管如此，在文档的节点树中，为特定 置的某个元素应用样式仍旧不是件容易的事。例如，在CSS3中，你可以使用hi〜*选择器为 有hi元素的下一个同辈元素声明样式。问题是，有那么多的浏览器根本不支持CSS3的这些可 的位置选择器。
现在，CSS还无法根据元素之间的相对位置关系找出某个特定的元素，但这对DOM来说 不是什么难题。我们可以利用DOM轻而易举地找出文档中的所有hi元素，然后再同样轻而易 地找出紧跟在每个hi元素后面的那个元素，并把样式添加给它。

9.3何时该用DOM脚本设置样式	159
首先，用getElementByTagName方法把所有的hi元素找出来：
var headers = document♦getElementsByTagNan)e(tlhiff);
然后，遍历这个节点集合里所有元素：
for (var i=〇; i<headers^length; i++) {
文档中的下一个节点可以用nextSIbllng属性査找出来：
headers[i]•nextSibling
请注意，这里真正需要的不是“下一个节点”，而是“下一个元素节点”。下面这个getNext- Element函数可以让我们轻松完成这一任务：
function getNextElement(node) { if(node.nodeType == i) { return node;
>
if (node^nextSibling) { return getNextElement(node.nextSibling);
}
return null;
}
把当前hi元素（即headers[1])的nextSibling节点作为参数传递给getNextElement函数，并 把这个函数调用的返回值赋值给elem变量：
var elem = getNextElement(headers[i]•nextSibling);
现在，就可以按照我们的想法去设置这个元素的样式了：
elem • style •fontWeight = f,bold!,; elem • style • font Size = "：U2em";
最后，把以上代码封装到函数styleHeaderSIbllngs中，别忘了安排一些测试去检査浏览器能 否理解我们在这个函数里用到的DOM方法：
function styleHeaderSiblings() { if (IdocumervLgetElementsByTagName) return false; var headers = docuinent.getElementsByTagName(,lhlt,); var elem;
for (var i=〇; i<headers.length; i++) { elem = getNextElement(headers[i]•nextSibling);
elem.style* fontWeight = "bold"; elem^style.fontSize = "Uem";
function getNextElement(node) { if(node.nodeType == l) { return node;
>
if (node.nextSibling) { return getNextElement(node.nextSibling);
return null;
你可以用window.onload事件调用这个函数:

160 第 9 章 CSS-DOM
window^onload = styleHeaderSiblings;
但更好的做法是用addLoadEvent函数，这样你就能很方便地把更多的函数绑定到这个事件:
addLoadEvent(styleHeaderSiblings);
下面是addLoadEvent函数的代码清单，你可以把它保存到一个外部文件：
function addLoadEvent(func) { var oldonload = window.onload; if (typeof window.onload != 'function') { window^onload = func;
} else {
window,onload = function() { oldonload(); func();
为了看到styleHeaderS'iblings函数的使用效果，写一个HTML文档，并在里面添加一些一 级标题（即hi元素）：
<!D0CTYPE html>
<html lang="en">
<head>
<meta charset=flutf-8M />
<title>Man bites dog</title>
</head>
<body>
<hl>Hold the front page</hi>
<p>This first paragraph leads you iru</p>
<p>Now you get the nitty-gritty of the storyx/p〉
<p>The most important information is delivered first*</p>
<hl>Extra! Extra!</hi>
<p>Further developments are unfolding.</p>
<p>You can read all about it here.</p>
</body>
</html>
把这个文档保存为story.html文件。图9-14是它目前在浏览器里的样子。
接下来，创建文件夹scripts来存放JavaScript脚本文件。把addL6adEvent函数存为一个名为 addLoadEvent.js的文件，并把它放到这个文件夹，把styleHeaderSIbllngs函数存为一个名为 styleHeaderSIbllngs. js的文件，也把它放到此文件夹。
为了调用这个两个JavaScript脚本文件，还需要在story.html文件的</boc(y>标签之前插入一 些〈script〉标签：
〈script src^nscripts/addLoadEventtjsnx/script>
〈script src=Mscripts/styleHeaderSiblings.jsMx/script>
现在，把story.html文件加载到Web浏览器中，你就可以看到DOM脚本生成的样式效果了。 动态设置的样式将作用于紧跟在各个hi元素后面的那个元素（如图9-15所示)。
从理论上讲，这类样式还是应该用CSS来设置；但在实践中，用CSS来设置这类样式的难 度往往会很大。具体到这个例子，其实只需给紧跟在hi元素后面的每个元素添加一个class属性，




9.3何时该用DOM脚本设置样式 161
就可以用CSS来获得同样的效果。但如果文档的内容需要定期编辑和刷新，添加class属性的工 作很快就会变成一种负担。不仅如此，如果文档的内容需要通过一个CMS (内容管理系统）来 处理，给文档内容的个别部分添加class属性或其他样式的做法甚至是不允许的。
♦參凝 @ H	5m© C
Hold the front page
This first paragraph k^is you in*
Now you get the nitQr-grto of die story,
Tlie roost impottant in 负 mialioii is ^JeKveredfiistK
Extra! Extra!
Rufher devdopments are unfading. You can read alt about h here.



图 9-14
Hold the front page
Thi$ first paragraph leads you in?
Now you gel tfee niny-gritt>r of the stoiy.
The roost iitq>onaR! infoimation b detiveied first.
Extra! Extra!
Furth^ devdopmeots are unfotdlngt
You can read all about i( here.



图 9-15
912根据某种条件反复设置某种样式
不妨假设我有一份由一些日期和地名构成的清单，比如一份乐队演出日程表或一份旅行日程 表。我们不必关心它到底是什么，只要其中的日期和地点有直接对应的关系就行了。对，就是表 格型数据，把表格型数据转换为HTML内容的理想标签当然S<table>。
注意在用CSS安排你的内容时，千万不要人云亦云地认为表格都是不好的。虽然利用表格来
做页面布局不是好主意，但利用表格来显示表格数据却是理所应当的。
下面是为这个表格编写的标记:
<!D0CTYPE html>
<html lang="enn>
<head>
<meta charset=”utf-8" /> <title>Cities</title>
</head>
<body>
<table>
<caption>Itinerary</caption>
<thead>
<tr>
<th>When</th>
<th>Where</th>
</tr>
</thead>
<tbody>
<tr>















162 第 9 章 CSS，DOM
<td>Dune 9th</td>
<td>Portland, <abbr title="OregorT>OR</abbr></td>
</tr>
<tr>
<td>〕une lOth</td>
<td>Seattle> <abbr title=,lWashington,,>WA</abbrx/td>
</tr>
<tr>
<td>Dune I2th</td>
<td>Sacramento, <abbr title=llCalifornial,>CA</abbrx/td>
</tr>
</tbody>
</table>
</body>
</html>
把这些代码保存为1t1nerary.html文件。如果现在就把这个文件加载到一个Web浏览器里， 你将看到一个包含全部的信息但呆滞模糊的表格，如图9-16所示。
&B0
QTm





Itinerary
When Where
June 9th Porfland.OR June lOtti Seattle, WA June 12tfi Sacramento^ CA
t • *	4 i •	•	* •	* •	•	41	^	* t*% 99*	•• •

图 9-16
编写一个CSS样式表，让其中的数据可读性更好:
body {
font-family: 11 Helvetica11 >,lArial,f> sans-serif; background-color: #ff千^ color: #000；
}
table { margin: auto; border: lpx solid #699；
}
caption { margin: auto; padding: .2em; font-size: l.2em; font-weight: bold;
>
th {
font-weight: normal; font-style: italic; text-align: left; border: lpx dotted #699； background-color: #9cc;



color: #〇〇〇;
9.3何时该用DOM脚本设置样式	163
th,td { width: 10em; padding: .5em;
>
把这个CSS样式表保存为format.css文件并将其放入文件夹styles里。在1tinerary.html 文档的<head>部分增加一个<11冰>标签来引用这个CSS文件：
〈link rel="stylesheet" media="screen" href="styles/format.css” />
在Web浏览器里刷新1t1ne「a「y.html文件就可以看到这个CSS的效果，如图9-17所示。


^爹鏺©
I
itinerary
June 9th
June 10th June 12th
Poland, OR Seatte, WA Sacramento, CA

Doiiii
^	图 9-17
让表格里的行更可读的常用技巧是交替改变它们的背景色，从而形成斑马线效果，使相邻 的两行泾渭分明。通过分别设置奇数行和偶数行样式的办法可实现这种效果。如果浏览器支持 CSS 3,那就很简单，只需要如下两行样式：
tr:nth-child(odd) { background-color:# f干cj trrnth-child(even) { background-color
如果:nth-ch11d()不可用，要获取同样的效果就只好采用另外的技术。具体到1t1nerary.html 文档这个例子，只需为表格中的每个奇数行（或每个偶数行）设置一个class属性即可。不过， 这个方法不够方便，尤其是对大表格来说更是如此：如果你以后要在这个表格的中间插入或删
除一行，就不得不痛苦地手动更新大量的class属性。
JavaScript特别擅长处理重复性任务。用一个whl 1 e或fo「循环就可以轻松地遍历一个很长的
列表。
可以编写一个函数来为表格添加斑马线效果，只要隔行设置样式就行了。 ⑴把文档里的所有table元素找出来。
对每个table元素，创建odd变量并把它初始化为false。
遍历这个表格里的所有数据行。
如果变量odd的值是t「ue，设置样式并把odd变量修改为false。







164 第 9 章 CSS-DOM
如果变量odd的值是false，不设置样式，但把odd变量修改为true。	，
我为这个函数命名为stripeTables。这个函数不需要参数，所以函数名后面的圆括■f'是空的 别忘了在这个函数的开头部分安排一些测试，检查浏览器是否支持函数中用到的那些DOM方法
function stripeTables() { if (!document•getElementsByTagName) return false; var tables = document•getElementsByTagName(tltablefl); var odd, rows;
for (var i=〇; i<tables^length; i++) {
-	odd = false;
rows = tables[i]^getElementsByTagName(!<trff); for (var ]•=0; jcrows-length; j++) { if (odd « true) {
rows[j].style^backgroundColor Ir#ffc!,; odd - false;
} else { odd = true:
这个函数应该在页面加载时执行。用addLoadEvent函数来做这件事再合适不过：
addLoadEvent(stripeTables);
把以上JavaScript代码保存为文件strlpeTables.js，再将其和addLoadEvent.js文件都放到文 件夹scripts里去。
在1t1nerary.html文档的</body>；^签之前，增加两个<script>标签来调用这两个JavaScrii^ 脚本文件：
<script src=Mscripts/addLoadEvent^jsnx/script>
〈script src="scripts/stripeTables.js"></script>
把1t1ne「a「y.html文件加载到一个Web浏览器里，就可以看到表格里的偶数行都有了一个新 的背景颜色，如图9-18所示。

■ @ © !1
© Q t
Itinerary



June 10th
Seattle, WA

图 9-18

9.3何时该用DOM脚本设置样式	165
很凑巧，上一章的dlsplayAbbrevlatlons函数也适用于这个文档。把dlsplayAbbrevlatlons.js 文件也放到scripts文件夹里，并在Itlnerary.html文档再增加一个<sc「1pt>标签引用它。在Web 浏览器里刷新这个页面可以看到动态生成的“缩略语列表”，如图9-19所示。
0 ?0




♦癰 © fSH
▼
]© Q €

itinerary





June 10th
>
i
i 寒發爾
SeatUe, WA
Abbreviations
OR
CA
Oregon
Washington
California

,•
■ .. ,
图 9-19
9.3_3响应事件
只要有可能，最好选用css为文档设置样式。话虽这样说，你刚才也看到一些CSS不能处 理或是难以部署的情况。在这类CSS力不从心的场合，DOM可以帮上大忙。
何时应该使用CSS来设置样式，何时应该使用D0M来设置样式并不总是那么容易决定。如 果问题涉及需要根据某个事件来改变样式，就更难做出决定了。
CSS提供的:hover等伪cl ass属性允许我们根据HTML元素的状态来改变样式。D0M也可 以通过onmouseover等事件对HTML元素的状态变化做出响应。很难判断何时应该使用:hover属 性、何时应该使用onmouseover事件。
最简单的答案是选择最容易实现的办法。比如说，如果只是想让链接在鼠标指针悬停在其上 时改变颜色，就应该选用CSS:
a:hover { color: #c6〇;
>
伪类:hover已经得到了绝大多数浏览器的支持——至少在它被用来改变链接的样式时是如 此。但如果还想利用这个伪类在鼠标指针悬停在其他元素上时改变样式，支持这种用法的浏览器 就没有那么多了。

166 第 9 章 CSS-DOM
仍以1t1nerar7.html文档中的表格为例。如果想让某行在鼠标指针悬停其上时其文本变为粗 体，可以使用CSS:
tr:hover { font-weight: bold;
>
从理论上讲，鼠标指针悬停在表格的哪一行，哪一行的文本就应该加黑加粗；但在实践中， 这种效果只能在一部分浏览器里看到。
在这样的场合，DOM却能够得到公平对待。绝大多数的现代浏览器，虽然对CSS伪类的支 持很不完整，但对DOM却都有着良好的支持。在浏览器们对CSS的支持进一步完善之前，在事 件发生时用DOM改变HTML元素的样式更切合实际。
下面这个hlghllghtRows函数将在鼠标指针悬停在某个表格行的上方时，把该行文本加黑加 粗：	.
干unction highlightRows() {
if(!document•getElementsByTagName) return false; var rows = document•getElementsByTagName(,ftrn); for (var i=〇; i<rows.length; i++) { rows[i]•onmouseover = function() { this^style.fontWeight = ''bold11;
}
rows[i]•onmouseout = function() { this•style.fontWeight = "normal";









€
Itinerary











Abbreviations
addLoadEvent(highlightRows);
把这个函数存入文件hlghllghtRows.js并把它
放入scripts文件夹，然后在1t1nerary.html文档的
</body>标签之后增加一个如下所示的<$(：「1卩1:>标签：
<script src=uscripts/highlightRows.jsnx/$cript>
在Web浏览器里刷新it1nerary.html文档。现
在，当你把鼠标指针悬停在某个表格行的上方时，
这个表格行里的文本将加黑加粗，如图9-20所示。
在这一类场合，需要决定是采用纯粹的CSS来
解决，还是利用DOM来设置样式。你需要考虑以
下因素：
□这个问题最简单的解决方案是什么；
□哪种解决方案会得到更多浏览器的支持。
要做出明智的抉择，就必须对CSS和DOM技
术都有足够深入的了解。如果你手里只有榔头，那
么你看到的任何东西都像钉子。如果你只喜欢使用CSS，你十有八九会选择一个CSS解决方案，
而不考虑JavaScript解决方案的效果会不会更好。反之，如果你只懂得写D0M脚本，你往往会
WA
CA
Omgon
Washington
Caiifomia


图 9-20

9.4 className 属性 167
立刻动手编写JavaScript函数，而不去考虑用CSS来解决问题会不会更简明快捷。
如果想改变某个元素的呈现效果，使用CSS;如果想改变某个元素的行为，使用DOM;如 果你想根据某个元素的行为去改变它的呈现效果，请运用你的智慧，在这个问题上没有放之四海 而皆准的答案。
9.4 className 属性
在本章前面的例子里，我们一直在使用DOM直接设置或修改样式。这种做法让“行为层” 干“表示层”的活，并不是理想的工作方式。如果你改变了主意，想换换那些由DOM脚本设 置的样式，就不得不埋头于JavaScript函数中去寻找和修改与设置样式有关的语句。如果可以在 样式表里进行那些修改，那就好多了。
这里有一种简明的解决方案：与其使用DOM直接改变某个元素的样式，不如通过JavaScript 代码去更新这个元素的class属性。
大家看看styleHeaderSIbllngs函数是如何添加样式的：
function styleHeaderSiblings() { if (!document.getElementsByTagName) return false; var headers = document*getElementsByTagName(,fhln); var elem;
for (var i=〇; i<headers.length; i++) { elem = getNextElement(headers[i].nextSibling); elem•style•fontWeight = "bold"; elem. style# font Size = f,i^2emnj
}
>
如果决定把紧跟在一级标题之后的那个元素的CSS字号值从1.2em改为1.4em，你就不得不 去修改 styleHeaderSIbllngsO 函数。
如果你引用一个外部CSS样式表，并且其中有一条针对.intm类的样式声明：
•intro {
千ont-weight: bold; font-size: i^2em;
>
现在只需在styleHeaderSIbllngsO函数里把紧跟在一级标题之后的那个元素的class属性设 置为Intro就可以达到同样的目的。
可以用setAttribute方法来做这件事：
elenusetAttribute("class","intro”）；
更简单的办法是更新className属性。className属性是一个可读何写的属性，凡是元素节点 都有这个属性。
你可以用className属性得到一个元素的class属性：
element•className
用className属性和赋值操作符设置一个元素的class属性:

168 第 9 章 CSS-DOM
element•className = value
下面是利用className属性编写出来的styleHeaderSIbllngs函数，它在设置样式时不需要直 接与style属性打交道：
function styleHeaderSiblings() { if (!document•getElementsByTagName) return false; var headers = document^getElementsByTagName(,lhln); var elem;
for (var i=〇; i<headers^length; i++) {
elem = getNextElement(headers[i].nextSibling);	、
elenuclassName = n intro11;
现在，不论你什么时候想改变紧跟在一级标题之后的那个元素的样式，只需在css里修 改.1 ntm类的样式声明：
•intro {
font-weight: bold; font-size: 1^4em;
>
这个技巧只有一个不足：通过className属性设置某个元素的class属性时将替换（而不是 追加）该元素原有的class设置：	•
<hl>Man bites dog</hl>
<p class=lldisclaimerll>This is not a true story</p>
如果对包含以上标记的文档使用styleHeaderSiblings函数，那个“文本段”元素的class属
姓将从disclaimer被替换为Intro，而这里实际需要的是“追加”效果	class属性应该变成
dlsclalmeMntro，也就是disclaimer和Intro两种样式的叠加。
你可以利用字符串拼接操作，把新的class设置值追加到className属性上去（请注意，Intro 的第一个字符是空格)，如下所示：
elerruclassName += " intro";
不过，实际上你只希望在原来确实有一个class的情况下才这么做。如果原来没有任何class， 直接对cl assName属性赋值就可以了。
在需要给一个元素追加新的class时，你可以按照以下步骤操作：
检查cl assName属性的值是否为null;
如果是，把新的cl ass设置值直接赋值给cl assName属性；
如果不是，把一个空格和新的class设置值追加到cl assName属性上去。
你可以把以上步骤封装为一个函数addClass。这个函数带两个参数：第一个是需要添加新 class的元素（element)，第二个是新的class设置值（value):
function addClass(element,value) { if (!element•className) { element•className = value;
} else {

9A className 属性 169
newClassName = element•className; newClassName+= •’ "； newClassName+- value; element.className = newClassName;
在 styleHeade「Sibl1ngs 函数里调用 addClass 函数:
function styleHeaderSiblings() { if (!document•getElementsByTagName) return false; var headers = document^getElementsByTagName(,!hlH); var elem;
for (var i=0; i<headers^length; i++) { elem = getNextElement(headers[i]^nextSibling); addClass(elem/f intro,f);
你也可以更新一下strlpeTables函数。这个函数现在是通过直接改变奇数表格行的背景颜色 来实现斑马线效果的：
function stripeTables() { if,(!document•getElementsByTagName) return false; var tables = document.getElementsByTagName(丨’table”)； var odd, rows;
for (var i=0； i<tables.length; i++) { odd = false;
rows = tables[i].getElementsByTagName(!ltrfl); for (var j=0; j<rows*length; j++) { if (odd true) {
rows[j] • style •backgroundColor = lf#ffcM;
odd = false;
} else { odd = true;
先在format .css文件里增加一条对应于class="odd"的样式声明：
• odd {
background-color: #ffc;
}
然后修改strlpeTables函数，让它通过询用addClass函数来实现同样的效果:
function stripeTables() { if (!documentreturn false; var tables = document^getElementsByTagName(,ltable!l); var odd, rows;
for (var i=〇; ictables.length; i++) { odd = false;
rows = tables[i] •getElementsByTagName(Mtrlf) j for (var j=〇; j<rows^length; j++) { if (odd ~ true) { aiidClass(rowst;j],"odd"); odd = false;
} else { odd = true;

170 第 9 章 CSS-DOM



最终结果与前面完全相同。区别在于现在是通过CSS而不是DOM去设置样式。JavaScript函 数现在更新的是className属性，根本没碰style属性。这确保了网页的表示层和行为层分离得更 加彻底。
对函数进行抽象
你所有的函数都工作得很好，完全可以让它们保持现状。不过，只需再做一些小小的改动， 它们就会变得更加通用。把一个非常具体的东西改进为一个较为通用的东西的过程叫做抽象 (abstraction) 〇
仔细看看styl eHeaderSI bl 1 ngs函数，就会发现它仅适用于hi元素，而且cl assNeme属性值1 ntm 也是硬编码在函数代码里的：
function styleHeaderSibling$() { if (!document.getElementsByTagName) return false; var headers = document•getElementsByTagNamef’hl"); var elem;
for (var i=〇; i<headers*length; i++) { elem = getNextElement(headers[i]•nextSibling); addClass(elem/fintro!T);
}
}
把这些具体的值转换为这个函数的参数，就可以让它成为一个更通用的函数。把改进后的新 函数命名为styleElementSIbling并给它增加两个参数	tag和theclass:
function styleElementSiblings(tag,theclass)
接下来，把函数代码中的字符串“hi”全部替换为参数变量tag，再把字符串“intro”全部 替换为参数变量theclass。为了增加代码的可读性，你也可顺便把原来的headers变量名替换成 elems以增加可读性：
function styleElementSiblings(tag,theclass) { if (!document•getElemervtsByTagName) return false; var elems = document.getElementsByTagNaine(tag); var elem;
for (var i=〇; i<elems.length; i++) { elem = getNextElement(elems[i]^nextSibling); addClass(elem,theclass);
现在，如果把字符串值“hi”和“intro”作为参数传递给这个新函数，就可以获得原来的效 果：
addloadEvent(function(){ styleElementSiblings("hi"/• intro");
})；
不论何时你发现可以像上面这样对某个函数进行抽象，都应该马上去做，这总是一个好主 意。今后你或许会需要对另一种元素或另一个className属性值进行类似的处理。如果真是那样，

那就是写一个styleElementSibl化gs通用函数的最好时机。
9.5小结
9.5 小结 171
在本章里，你看到了 DOM完整全新的一面。此前介绍的DOM方法和属性要么属于DOM Core，要么属于HTML-DOM〇本章介绍的CSS-DOM技术针对的是如何得到（读）和设置（写) style对象的各种属性，而style对象本身又是文档中的每个元素节点都具备的属性。
style属性的最大限制是它不支持获取外部CSS设置的样式。但你仍可以利用style属性去 改变各种HTML元素的呈现效果。这在我们无法或是难以通过外部CSS去设置样式的场合非常 有用。只要有可能，就应选择更新className属性，而不是去直接更新style对象的有关属性。 在本章里，我们向大家介绍了以下几种CSS-DOM技术的具体应用示例。
□根据元素在节点树里的位置设置它们的样式（styleHeaderSibllngs函数)。
遍历一个节点集合设置有关元素的样式（stripeTables函数)
□在事件发生时设置有关元素的样式（hlghlightRows函数)。
这几种应用都属于用JavaScript入侵CSS领地的情况，而我们这么做的理由不外乎两点：其 一是CSS无法让我们找到想要处理的目标元素，其二是用CSS寻找目标元素的办法还未得到广 泛的支持。或许，未来的CSS技术能够让我们远离这种“不务正业”的DOM脚本编程技术。
不过，有一种应用大概是CSS永远也无法与DOM竞争的：JavaScript脚本能定时重复执行 一组操作。通过不断改变样式，我们就能实现CSS根本不可能实现的效果。
在下一章里，你会看到一个这样的例子。你将写一个能够随着时间的推移而不断刷新元素位 置的函数。简单地说，你将用JavaScript实现动画效果。
