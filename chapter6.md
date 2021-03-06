# JavaScript Dom编程艺术

<h1>第6章 案例研究：图片库改进版</h1>
<h2>6.1 快速回顾</h2>
<h2>6.2 它支持平稳退化吗</h2>
<h2>6.3 它的JavaScript与HTML标记是分离的吗</h2>
<h3>6.31 添加事件处理函数</h3>
<h3>6.32 共享onload事件</h3>
<h2>6.4 不要做太多的假设</h2>
<h2>6.5 优化</h2>
<h2>6.6 键盘访问</h2>
<h2>6.7 把JavaScript与CSS结合起来</h2>
<h2>6.8 DOM Core和HTML-DOM</h2>
<h2>6.9 小结</h2>




<style>

p{text-indent:20px;}
</style>
# 6

## 61
或者
var supported = document•getElementsByTagName && document.getElementByld;
if ( !supported ) return;
不过，上面这样的代码开始变得比较冗长并难以阅读。事实上，从可读性的角度看，把多项 测试写在同一行上的做法不一定是最好的主意。有不少程序员喜欢像下面这样把return语句单独 写在一行上：
if (Idocument.getElementsByTagName) return false;
if (丨document•getElementByld) return false;	•
如果你也喜欢这样的写法，建议最好是用花括号把return语句括起来，如下所示：
if (!document.getElementsByTagName) { return false;
}
if (!document•getElementByld) { return false;

6.3 它的JavaScript与HTML标记是分离的吗 79
这或许是最清晰、最具有可读性的代码书写方式。
把这些测试写在同一行上还是写成好几行是你的自由，你完全可以根据自己的喜好来选
#。
完成这两项具有普遍适用性的测试后，我还安排了一个更具针对性的测试。我正在编写的这 兮函数将处理Id等于Imagegallery的那个元素所包含的链接，假如这个元素并不存在，我的这 个函数也就无需继续执行了。
与前面两项测试一样，我将使用“逻辑非”操作符来进行这一测试：
if (! document •getElementById(,rimagegalleryM)) return 干alse;
出于个人偏好，你也许更喜欢下面这样的写法：
if (!document•getElemerrtByld(丨丨imagegallery1’））{ return false;
这项测试是一个预防性措施。现在我知道调用这个JavaScript函数的文档里有一个Id属性值 等于Imagegallery的列表清单元素，但我不敢确定这在将来会不会发生变化。有了这个预防性措 室，即使以后我决定从网页上删掉图片库，也用不着担心这个网页的JavaScript代码会突然出错。 茫HTML文档的内容与JavaScript代码所实现的行为分离开来的重要性由此可见一斑。作为一条 M則，如果想用JavaScript给某个网页添加一些行为，就不应该让JavaScript代码对这个网页的 结构有任何依赖。

二麵蝨膽化程序紐备麵
我们在学校里学过一种理论，叫結构化程序设计（stmctedprogramming) 9其中有这样一
条原则;函数应该只有一个入口和一个出口
我刚才的做法已经违背了这一原则:我在prepareGa〗"lery()函数的开头部分使用了多条
return false语句，它们全都是这个函数的出口。根据轉构化程序设计理讼，应该把这些出口
点减少到一个。	\	^	。
从埋论上讲，我很赞同这项原则;但在实际工作中心迸分拘泥于这项原测往往会使我码变
得非常难以阅读/如果为了避免留下多个出口点而去改写那些IT语句的话—这个馬数的杨母
♦ ♦ ♦
代码就会被掩埋在一层又一层的花括号里，就像下面这样：
. . 	 .
function prepareGalleryO {
if (document•getEl^merrtsByTagName^ {
，ii (document•getsiementByW) {
if (document •getEIeinentByld^	{
statements go here…
我个人认为，如果一个函数有多个出口，只要这些出口集中出现在函数的开头部分^就:
♦ • « *
♦ « ♦
是可以接受的。

80 第6章案例研究：图片库改进版
出于可读性的考虑，我把那些return false语句全部集中到prepareGallery的开头部分：
function prepareGallery() { if (!document.getElementsByTagName) return false; if 〇 documentreturn false; if (!document•getElementById(fliinagegalleryn)) return false;
必要的测试和检査工作就绪之后，我现在开始写事件处理函数的核心功能。
变量名里有什么
首先，我想把事情弄得稍微简单些：重复多次地敲入像document.getElementByldrimage gallery")这么长的一串实在很麻烦，所以我决定创建一个名为gallery的变量来简化它：
var gallery = document^getElementById(nimagegallerytr);
完全可以给变量起一个另外的名字。我之所以选用“gallery”来命名，是因为它的含义就是 图片库。选择一些有意义的单词来命名可以让代码更容易阅读和理解。
注意在为变量命名时一定要谨慎从事。有些单词在JavaScript语言里有特殊的含义和用途，这 些统称为“保留字”的单词不能用做变量名。另外，现有JavaScript為数或方法的名字也 不能用来命名变量。不要使用诸如alert、var或If之类的单词作为变量的名字。
按照计划，需要遍历Imagegallery元素中的所有链接，我会用到getElementsByTagName。利用 刚刚创建的gallery变量，可以把对getElementsByTagName的调用简单地写成下面这个样子：
gallery. getElementsByTagName(ffa,t)
它等价于下面这个长长的记号：
document •getElementById(<limagegalleryll).getElementsByTagName(?ra,,)
现在，我想把事情弄得更简单些。我决定把上面这个记号所代表的数组（更准确地说，是一 个节点列表）赋值给一个短变量，并将该变量命名为links:
var links = gallery.getElementsByTagName(l,alf);
下面是prepareGallery函数目前的样子：
function prepareGallery() { if (!document•getElementsByTagName) return false; if 〇documentgetElementByld) return false; if (!document♦getElementById(friii]agegalleryM)) return false; var gallery = document•getElementById(nimagegallery"); var links = gallery•getElementsByTagName(fla,f);
准备工作已就绪。我已经安排好了必要的检查工作，还创建了几个变量。
3.遍历
我想遍历处理links数组里的各个元素，可以用一个fo「循环来完成这项工作。
首先，把计数器的初始值设置为零。每处理links数组里的一个元素，这个计数器就增加一 个1。下面是对计数器进行初始化的语句：

6.3 它的JavaScript与HTML标记是分离的吗 81
var i = 0;
j	把充当循环计数器的变量命名为“i”是一种传统做法。字母“i”在这里的含义是“increment”
丨t递増），许多程序设计语言里都习惯使用“i”作为递增的变量的名字。 j	下面是这个循环的控制条件：
丨 i < links,length;
上面这个表达式的含义是：只要变量彳的值小于links数组的length属性值，这个fo「循环 釐一直循环下去。length的值总是等于links数组里的元素总个数。因此，如果links数组包含4 个元素，那么只要i小于4,我的for循环就将一直循环下去。
最后，使用下面这个记号来给循环计数器加上一个1: i++;
这个记号是下面这条语句的简写形式：
i = i+l;
上面这几条语句的效果是：这个for循环每执行一次，变量1的值就会加1; 一旦变量1的 置不再小于links.length，循环就结束。因此，如果links数组包含4个元素，这个循环将在1 等于4时结束执行。这个循环将总共执行4次——别忘了，变量1是从零开始计数的。
下面是f〇「循环的开头部分：
for ( var i=0; i < links.length; i++) {
改变行为
具体到这个例子，我想要完成的操作是改变links数组中的各个元素的行为。事实上，与其 锭links是一个数组，不如说它是一个节点列表（nodelist)来得更准确。它是一个由DOM节点 fe成的集合，这个集合里的每个节点都有自己的属性和方法。
我最感兴趣的是它的oncllck方法，像下面这样为它添加一个行为：
linksfi]•onclick = function() {
这条语句定义了一个匿名函数。这是一种在代码执行时创建函数的办法。具体到上面这条语- 句，它把"Mnksn]元素的oncllck事件处理函数指定为这个匿名函数。这个匿名函$里的所有语 旬将在1彳nks[1]元素所对应的链接被点击时执行。	’
11nks[1]元素的值会随着变量1的递增而变化。如果假设links集合里包含4个元素，那么第 丨一个元素将是11nks[0]，最后一个元素是links[3]。
1 我传递给showPIc函数的参数是关键字this，它代表此时此刻与oncllck方法相关联的那个 元素。也就是说，this在这里代表11nks[1]，而11nks[i]又对应着links节点列表里的某个特定 钓节点：
showPic(this);
我还需要再多做一件事，即禁用有关链接的默认行为。如果showP1c()函数执行成功，就不 让浏览器执行某个链接被点击时的默认操作。和以前一样，我想取消这种默认行为，不让浏览器

















82 第6章案例研究：图片库改进版
前进到那个链接所指向的目的地:
return false
返回布尔值false相当于向浏览器传递了这样一条消息：“按照这个链接没被点击的情况采 取行动。”
最后，还需要用一个右花括号来结束这个匿名函数。下面是我最终完成的匿名函数：
links[i].onclick = function() { showPic(this); return false;
>
5■完成JavaScript函数
现在，需要用一个右花括号来结束for循环:
for ( var i=〇; i < links♦length; i++) { links[i]*onclick = function() { showPic(this); return false;
最后，再用一个右花括号结束prepareGallery函数。下面是这个函数完整代码清单:
function prepareGallery() {
if (!document•getElementsByTagName) return false;
if (!document•getElementByld) return false;
if (!document•getElementById(!fimagegallery11)) return false;
var gallery = document•getElenfientById(!limagegalleryM);
var links = gallery#getElementsByTagName(llafl);
for ( var i=〇; i < links•length; i++) {
links[i]^onclick = function() {
showPic(this);
return false;
\
调用此函数， 上。
就会把oncllck事件绑定到id等于“imagegallery”
的元素内的各个链接元素
注意如果想了解JavaScript的其他信息，可以参考Aaron Gustafon与我合著的AdvancED DOM Scripting: Dynamic Web Design Techniques (Apress，2007)。
6.3.2共享onload事件
我必须执行prepareGallery函数才能对oncllck事件进行绑定。
如果马上执行这个函数，它将无法完成其工作。如果在HTML文档完成加载之前执行脚本， 此时DOM是不完整的。具体到prepareGallery函数，它的第3行代码将测试"Imagegallery"元素 是否存在，如果DOM不完整，这项测试的准确性就无从谈起，事态的发展就会偏离我的计划。

6.3 它的JavaScript与HTML标记是分离的吗 83
应该让这个函数在网页加载完毕之后立刻执行。网页加载完毕时会触发一个onload事件， 这个事件与window对象相关联。为了让事态的发展不偏离计划，必须把p「epa「eGalle「y函数绑 定到这个事件上：
window*onload = prepareGallery;
它解决了我的问题，但像现在这样还不够完美。
假设我有两个函数：flrstFunctlon和secondFunctlon。如果想让它们俩都在页面加载时得 到执行，我该怎么办？如果把它们逐一绑定到onload事件上，它们当中将只有最后那个才会被 实际执行：
window^onload = firstFunction;	♦
window.onload = secondFunction;
secondFunction将取代firstFunctlon。你可能会想：每个事件处理函数只能绑定一条指令。 有一种办法可以让我避过这一难题：可以先创建一个匿名函数来容纳这两个函数，然后把那 个匿名函数绑定到onload事件上，如下所示：
window^onload = function() { firstFunction(); secondFunction();
它确实能很好地工作——在需要绑定的函数不是很多的场合，这应该是最简单的解决方案 了。
这里还有一个弹性最佳的解决方案——不管你打算在页面加载完毕时执行多少个函数，它都 可以应付自如。这个方案需要额外编写一些代码，但好处是一旦有了那些代码，把函数绑定到 window. on 1 oad事件就非常易行了。
这个函数的名字是 addLoadEvent，它是由 Simon Willison (详见 http://simon.incutio.com)编
写的。它只有一个参数：打算在页面;&卩载完毕时执行的函数的名字。
下面是addLoadEvent函数将要完成的操作。
口把现有的window.onload事件处理函数的值存入变量oldonload。
口如果在这个处理函数上还没有绑定任何函数，就像平时那样把新函数添加给它。
口如果在这个处理函数上已经绑定了一些函数，就把新函数追到现有指令的末尾。 下面是addLoadEvent函数的代码清单：
function addLoadEvent(func) { var oldonload = window^onload; if (typeof window^onload != 'function1) { window.onload = func;
} else {	v
window.onload = function() { oldonload(); func();
这将把那些在页面加载完毕时执行的函数创建为一个队列。如果想把刚才那两个函数添加到

84 第6章案例研究：图片库改进版
这个队列里去，只需写出以下代码就行了 ：
addLoadEvent(firstFunction);
addLoadEvent(secondFunction);
我发现这个函数非常实用，尤其是在代码变得越来越复杂的时候。无论打算在页面加载完毕 时执行多少个函数，只要多写一条语句就可以安排好一切。
这个解决方案对prepareGallery函数来说好像有点儿大材小用，因为只有这一个函数需要在 页面加载完毕时执行。可是，为以后的扩展做一些准备工作总不是件坏事。我决定把addLoadEvent 函数收录到我的脚本里，这使我只需写出下面这行代码就可以了 ：
addLoadEvent(prepareGallery);
到这一步，P「epa「eGalle「y函数已经足够安全了，至少在我的能力范围内。接下来，我将怀 疑的目光转向第4章编写的showPic函数。.
6.4不要做太多的假设
我在showPic函数里发现的第一个问题是，我没有让它进行任何测试和检查。 showPic函数将由prepareGallery函数调用，而我已经在后者的开头对getElementByld和 getElementsByTagName等DOM方法是否存在进行过检査，所以我确切地知道用户的浏览器不会因 为不理解这两个方法而出问题。
不过，我还是做出了太多的假设。别的先不说，我在代码里用到了 Id属性值等于palceholder 和description的元素，但我并未对这些元素是否存在做任何检査：
function showPic(whichpic) { var source * whichpic.getAttribute(lfhrefTf); var placeholder = document• getElementById(,fplaceholdern); placeholder •setAttribute(Msrc?f, source); var text = whichpic.getAttribute(f,title11); var description = document .get ElementById(ffdescriptionlr); description^firstChild^nodeValue = text;	.
}
需要增加一些语句来检査这些元素是否存在。
showPic函数负责完成两件事：一是找出Id属性值是palceholder的图片并修改其src属性； 二是找出Id属性是description的元素并修改其第一个子元素（flrstOrild)的nodeValue属性。
第一件事是这个函数必须完成的任务，第二件事只是一项锦上添花的补充。0此，我决定把检查 工作分成两个步骤以获得这样一种效果：只要palceholder图片存在，即使description元素不存
在，切换显示新图片的操作也将照常进行。
正如你在prepareGallery函数里看到的那样，检查某个特定的元素是否存在是一件很简单的 事情：
if (!document•getElementById(?tplaceholderfr)) return false;
紧随其后的是用来修改palceholder图片的six属性的代码，它们的效果是切换显示一张新 图片：

6.4不要做太多的假设 85
var source = whichpic.getAttribute(Mhrefn);
var placeholder = document.getElementByld卜placeholder”）；
placeholder •setAttribute(frsrcM, source);
以上代码负责完成函数的主要任务。接下来，采用一种稍有不同的方法检査description元 素是否存在：
if (document•getElementById(,,description,<)) {
只有通过了这项检査，负责修改图片说明文字的代码才会得到执行，如下所示：
var text = whichpic^getAttribute(ntitle,f);
var description = document.getElementById(,rdescription11);
description•firstChild.nodeValue = text;
}
将描述部分放在If语句里后，description元素将是可选的。如果它存在，它将被更新，否 購会忽略。
return true;
下面是showPIc函数在我给它增加了检查之后的代码清单:
function showPic(whichpic) {
if (!documentsgetElementById(Mplaceholderu)) return false; var source = whichpic*getAttribute(,,hrefM); var placeholder = document•getElementById(,,placeholderM); placeholder •setAttribute(,!srcu, source); if (document^getElementById(,ldescription,1)) { var text = whichpic*getAttribute(MtitleM); var description = document•getElementBylW"description"); description•firstChild^nodeValue = text;
return true
改进后的showPIcO函数不再假设有关标记文档里肯定存在着palceholde「图片和description 元素。即使文档里没有palceholder图片，也不会发生任何JavaScript错误。
可是，还有一个问题：如果把palceholder图片从标记文档里删掉并在浏览器里刷新这页面， 就会出现这种情况，无论点击imagegellery清单里的哪一个链接，都没有任何响应。
这意味着我们的脚本不能平稳退化。此时，应该让浏览器打开那个被点击的链接，而不是让 什么事情都不发生。
问题在于p「epareGalle「y函数做出了这样一个假设：showPIc函数肯定会正常返回。基于这一 緩设，prepareGallery函数取消了 oncllck事件的默认行为：
links[i].onclick = function() { showPic(this); return false;
是否要返回一个false值以取消oncllck事件的默认行为，其实应该由showPIc函数决定。 showPI c应返回两个可能的值。
□如果图片切换成功，返回true。

86 第6章案例研究：图片库改进版
□如果图片切换不成功，返回false。
为修正这个问题，应该在返回前验证showPIc的返回值，以便决定是否阻止默认行为。如果 showPIc返回t「ue，那么更新placeholder。在〇11(：1化1(事件处理函数中，我们可以利用“！”对showPK 的返回值进行取反。
links[i]tonclick = function() {
return IshowPic(this)	•
}
现在，如果showPIc返回true'，我们就返回false，浏览器不会打开那个链接。
如果showPIc返回false，那么我们认为图片没有更新，于是返回true以允许默认行为发生。 下面是p「epareGallery函数现在的代码清单：
function prepareGallery() { if (!document•getElementsByTagName) return false; if (!document•getElementByld) return false; if (! document •getElementByld^11 imagegallery11)) return false; var gallery = document•getElementById(,,imagegalleryn); var links = gallery•getElementsByTagName(Half); for ( var i=〇; i < links•length; i++) { links[i]^onclick = function() { return !showPic(this);
经过一番周折，终于把最后一个已知问题解决了。如果palceholder图片不存在，浏览器将 按用户所点击的那个链接打开一张新图片。现在可以把palceholde「图片重新放回到标记里去了。
6.5优化
这几个函数已经相当完善了。虽然它们的长度有所增加，但它们对标记的依赖和假设已经比 原先少多了。
尽管如此，在showPIc函数里仍存在一些需要处理的假设。
比如说，假设每个链接都有一个title属性：
var text ^ whichpic.getAttribute(ntitleu);
为了检査title属性是否真的存在，可以测试它是不是等于ml 1:
if (whichpic.g.etAttribute(l,titleH) != null)
如果title属性存在，这个if表达式将被求值为true。如果title属性不存在，whlchplc. getAttributertltle")将等于null，而这个if表达式将被求值为false。
这个If表达式还可以简写为：
if (whichpic•getAttribue("title"))
只要title属性存在，这个"if表达式就将返回一个true值。
作为一种简单的视觉反馈，在title属性不存在时把变量text的值设置为空字符串：

6.5优化 87
if (whichpic*getAttribute(,ftitle11)) { var text = whichpic^getAttribute(!,titlen);
} else { var text = 11 fl;
>
下面是完成同样操作的另一种办法：
var text = whichpic.getAttribute(lltitlei,) ? whichpic.getAttribute(ntitlen) : ,flf;
紧跟在getAttribute后面的问号是一个三元操作符（ternary operator)。这个问号的后面是变 量text的两种可取值。如果getAttr1bute("title")的返回值不是null，text变量将被赋值为第一 个值r如果getAttribute("tnien)的返回值是null，text变量将被赋值为第二个值：
variable = condition ? if true : if false;
如果title属性存在，变量text将被赋值为wh1chp1c.getAttribute("t1tle")。如果title属
性不存在，变量text将被赋值为一个空字符串
三元操作符是1f/else语句的一种变体形式。它比较简短，但逻辑关系表达得不那么明显。 如果你也这么认为，那就使用1f/else语句好了。
现在，如果试图把Imagegallery清单里的某个链接的title属性删掉并重新加载这个页面， 当你再去点击那个链接的时候，description元素将被填入一个空字符串。
如果想做到十全十美的话，可以对任何一种情况进行检查。
比如说，检查palceholde「元素是否存在，但需要假设那是一张图片。为了验证这种情况， 可以用nodeName属性来增加一项测试：
if (placeholdennodeMame != "IMG") return false;
请注意，nodeName属性总是返回一个大写字母的值，即使元素在HTML文档里是小写字母。 我还可以引入更多的检査。比如说，假设description元素的第一个子元素（flrstChlld)是
一个文本节点。我应该对此进行检査。	。
可以利用nodeType属性来进行这项检査。还记得吗，文本节点的nodeType属性值等于3:
if (description•firstChild•nodeType == 3) { description.firstChild^nodeValue = text;
下面是引入了以上几项检査之后showPIc函数的代码清单：
function showPic(whichpic) {
if (! document •get ElementById(,f placeholder11)) return false; var source = wfiichpiogetAttribute("href"); var placeholder document•getElementById(nplaceholder11); if (placeholder•nodeName != ’’IMG") return false; placeholder.setAttribute(nsrcn,source); if (documentsgetElementByld("description”））{ var text = whichpic*getAttribute(ntitleH) ? whichpic.getAttribute(,ltitle,t) : ,MI; var description = docufnent^getElementById(udescriptionn); if (description•干irstChilcLnodeType == B) { description•firstChilcL nodeValue = texij
return true:

88 第6章案例研究：图片库改进版
因为又增加了几项检査，showP1c()函数里的代码变得更多了。在实际工作中，你要自己决定 是否真的需要这些检査。它们针对的是HTML文档有可能不在你控制范围内的情况。理想情况 下，你的脚本不应该对HTML文档的内容和结构做太多的假设。
这方面的决定需要根据具体情况来做出。
6.6键盘访问
在有关oncllck事件处理的脚本里，有一项优化工作是不能不考虑的。
下面是prepareGallery()函数中的核心代码：
links[i]-〇nclick = function() { i千（sGowPic(this)) { return false;
} else { return true;
>
>
首先，为了简洁，将它改为使用三元运算符。
links[i]*onclick = function() { return showPic(this) ? false : true;
}
这段代码本身没有任何毛病。当这个链接被点击时，showP1c()函数就开始执行。不过，这作 了一个假定：用户只会使用鼠标来点击这个链接。
但是，千万不要忘记并非所有的用户都使用鼠标。比如说，有视力残疾的用户往往无法看清 屏幕上四处移动的鼠标指针，他们往往更喜欢使用键盘。
作为一个众所周知的事实，不使用鼠标也可以浏览Web。键盘上的Tab键可以让我们从这个 链接移动到另一个链接，而按下回车键将启用当前链接。
有个名叫onkeyp「ess的事件处理函数是专门用来处理键盘事件的。按下键盘上任何一个按键 都会触发onkeypress事件。
如果想让onkeypress事件与oncllck事件触发同样的行为，可以简单地把有关指令复制一份:
links[i]•onclick = function() { return showPic(this) ? false : true;
}
links[i].onkeypress = function() { return showPic(this) ? false : true;
}
还有一种更简单的办法可以确保onkeypress模仿oncllck事件的行为：
links[i]-onkeypress = links[i].onclick;
上面这条一语句把oncllck事件的所有功能赋给onkeypress事件:
links[i],onclick =干unction() { return showPic(this) ? false : true;
}
linksfi]♦onkeypress = links[i]*onclick;

6.6键盘访问 89
这就是JavaScript与HTML分离带来的方便。
如果你已经把所有的函数和事件处理函数都放在了外部文件里，就可以只在必要时修改 JavaScript代码，而根本不用动HTML文件。你可以随时打开你的脚本文件，优化它们，你做出 的修改将自动作用于每个引用了它的网页。
如果你仍在使用内嵌于HTML文档的事件处理函数，在修改JavaScript功能之后，你可能需 要打开HTML文档去进行大量的修改。比如说，在图片库这个例子里，我当初曾使用过一些如 下所示的内嵌事件处理函数：
<li>
<a href=nimages/fireworks.jpg" onclick=',showPic(this);return false;"title=MA •fireworks displayn>Fireworks</a>
</li>
在对showP1c()函数返回true或false的情况做出调整之后，我不得不对HTML文档里的 oncllck事件处理函数做出相应的修改，如下所示：
<li>
<a href="images/干ireworks^pg” onclick=’_return showPic(t^^ ? false : true;"
title=’’A fireworks display!,>Fireworks</a>
</li>
如果图片库有大量图片的话，这种修改工作真是又累又烦。
设想一下，如果想添加onkeypress事件处理函数，就不得不找出所有的链接，给它们每个 増加一个内嵌事件处理函数：
<li>
<a href=uimages/fireworkStjpgn onclick="return showPic(this) ? false : true;11 ^ onkeypress=ffreturn showPic(this) ? false : true;”
title=”A fireworks displayM>Fireworks</a>
</li>
这是一件苦差事（非常麻烦又非常容易出错)。而现在我只修改了很少几条语句就把一切安 铮妥当。
小心 onkeypress
我最后的决定是不添加onkeypress事件处理函数。原因是这个事件处理函数很容易出问题。 写户每按下一个按键都会触发它。在某些浏览器里，甚至包括Tab键！这意味着如果绑定在 crskeypress事件上的处理函数上返回的是false，那些只使用键盘访问的用户将永远无法离开当前 ^。我的图片库网页就存在这样的问题——只要图片切换成功，showPIc函数就将返回false。 那这些只使用键盘的人可怎么办？
幸运的是，oncllck事件处理函数比我们想象得更聪明。虽然它的名字“ondick”给人一种 它只与鼠标点击动作相关联的印象，但事实却并非如此：在几乎所有的浏览器里，用Tab键移动 焉某个链接然后按下回车键的动作也会触发oncllck事件。从这一点来看，把它命名为onactivate
■
备许更恰如其分。
围绕着oncllck和onkeypress有许多让人困惑的东西，它们的名字是造成这些困惑的主要原 有些可用性指南建议我们在处理oncllck事件时也一定要处理onkeypress事件。事实上，这

90 第6章案例研究：图片库改进版
种搭配导致的问题远比它们解决的更多。
最好不要使用onkeypress事件处理函数。oncllck事件处理函数已经能满足需要。虽然它叫 “onclick”，但它对键盘访问的支持相当完美。
下面是最终完成的prepareGaller^O和showP1c()函数的代码清单：
function prepaxeGallery() { if (!document•getElementsByTagName) return false; if (!document•getElementByld) return false; if (! document•getElernentById(,timagegallery,1)) return false; var gallery = documentsgetElementById(nimagegallery11 )j var links = gallery^getElementsByTagName(t,atl);
千or ( var i=0; i < links•length; i++) {
links[i]-〇nclick = function() { return showPic(this) ? false : true;
function showPic(whichpic) {
if (!document•getElementById(nplaceholderH)) return false; var source = whichpic^getAttribute(flhreftr); var placeholder = document•getElefnentById(,,placeholder,<); if (placeholder♦nodeName != ltIMG,f) return false; placeholder •setAttribute(Msrc11, source); if (documerr^getElementByldC’description")) { var text = whichpic^getAttribute(fltitle,f) ? whichpic.getAttribute(MtitleM) : IM,; var description = document.getElementByl^"description”）； if (description.firstChild^nodeType == 3) { description•firstChild•nodeValue = text;
注意可以在Friends of ED网站（http://www.friendsofed.com)上找到本书的页面来下载这两个 函数的最终完整版本。
6.7把JavaScript与CSS结合起来
把JavaScript代码从HTML文档里分离出去还带来另一个好处。在把内嵌型事件处理函数移 出标记文档时，我在文档里为JavaScript代码留下了一个“挂钩”：
这个挂钩完全可以用在CSS样式表里。
比如说，如果不想把图片清单显示成一个带项目符号的列表，则完全可以利用这个imagegallery 写出一条如下所示的CSS语句：



return true;
<ul id=flimagegalleryn>
#imagegallery { list-style: none;













6.7把JavaScript与CSS结合起来	91
我可以把这条CSS语句存入一个外部文件，比如layout.css文件，然后再从gallery.html 文件的<head>部分引用它：
<link rel=nstylesheetn href=nstyles/layout.css" type="text/css" media=,,screenn />
利用css，甚至可以让这份清单里的列表项从按纵向显示变成按桉向显示：
#imagegallery li { display: inline;
}
上面这两条CSS语句将使我的网页变成如图6-1所示的样子.













Snapshots
Faemviku Coffee Rose pig Ben
圓_響:氧每靈
wrnmm-：my:
p衡鋼释和
於¥1 二,
jOCv^^r. i
•，贫艇，
iMiB
mage
■： ：. ^	* t
_ 一碰礙響纖
|寧,

^ Qalleiy
：^u./Tvi^*.^v<；/,•	1	m.	，v *i；-.
Choose an image.
!©《©

图 6-1
即使把图片链接换成一些缩微图而不是文字，css也依然有效:
<ul id=Mimagegallery?l>	w
<li>
<a hre干="images/+ireworks.jpg" title=HA fireworks display11 >
<img src=l!images/thumbnail_fireworks^ jpg11 alt="Fireworks” /> </a>
</li>
<li>
<a hre千=nimages/coffee*jpg" title="A cup of black coffee" >
<img src^'linages/thumbnail^coffee^ jpgft a It=11 Coffeen />
</a>
</li>
<li>
<a href=Mimages/rose. jpgtf title=nA red, red rose">
<img src=Mimages/thumbnail rose.jpg'1 alt=,!Rosen />

92 第6章案例研究：图片库改进版
</a>
</li>
<li>
<a hre千="images/bigbemjpg" title=,fThe famous clock">
<img src=nimages/thurnbnail_bigben.jpgM alt=’fBig Ben” />
</a>
</li>
</ul>
图6-2是这个网页的新形象，图片链接都显示为缩略图而不是文本。



F面是layout.css文件的完整清单:
body {
font-family: "Helvetica","Arial",serif; color: #333； background-color: #ccc; margin: lem 10%;
}
hi {
color: #333；
background-color: transparent;
color: #c6〇;
background-color: transparent; font-weight: bold; text-decoration: none;



padding: 0；

6.8 DOM Core 和 HTML-DOM 93
float: left; padding: lem; list-style: none;
>
#imagegallery { list-style: none;
}
#imagegallery li { display: inline;
}
#imagegallery li a img { border: o；
>
这份样式表将把我的图片库页面装点得既美观又大方，如图6-3所示。
CO..




图 6-3
6.8 DOM Core 和 HTML-DOM
至此，我在编写JavaScript代码时只用到了以下几个DOM方法：
getElementByld
getElementsByTagName 口 get At tribute
setAttribute	.
这些方法都是DOM Core的组成部分。它们并不专属于JavaScript，支持DOM的任何一种 程序设计语言都可以使用它们。它们的用途也并非仅限于处理网页，它们可以用来处理用任何一 幹标记语言（比如XML)编写出来的文档。
在使用JavaScript语言和DOM为HTML文件编写脚本时，还有许多属性可供选用。例如， 表已经使用了一个属性oncllck，用于图片库中的事件管理。这些属性属于HTML-DOM，它们

94 第6章案例研究：图片库改进版
在DOM Core出现之前很久就已经为人们所熟悉了。
比如说，HTML-DOM提供了一个forms对象。这个对象可以把下面这样的语句：
document ♦getElementsByTagName(,'form11)
简化为：
document•forms
类似地，HTML-DOM还提供了许多描述各种HTML元素的属性。比如说，HTML-DOM为 图片提供的src属性可以把下面这样的语句：
elementsgetAttribute(nsrcH)
简化为：
element.src
这些方法和属性可以相互替换。同样的操作既可以只使用DOM Core来实现，也可以使用 HTML-DOM来实现。正如大家看到的那样，HTML-DOM代码通常会更短，必须提醒一下，它 们只能用来处理Web文档。如果你打算用DOM处理其他类型的文档，请千万注意这一点。
如果使用HTML-DOM的话，就可以把showPIc写得简短一些。
下面这条语句使用了 DOM Core来得到whlchp^ic元素的href属性并赋给变量source:
var source = whichpic^getAttribute("href”）；
下面是使用HTML-DOM达到同样目的的语句：
var source = whichpic,href;
下面是使用DOM Core的另一个例子，这次把placeholde「元素的src属性设置为变量source 的值：
placeholdersetAttribute("srcr、source);
下面是使用html_dom达到同样目的的语句：
placeholder.src = source;
即使你决定只使用DOMCore方法，也应该了解HTML_DOM。在阅读别人编写的脚本 时难免会遇到各种HTML-DOM记号，你至少应该知道都是干什么用的。
在本书的绝大多数章节里，我只使用DOM Core来编写代码。虽然代码会因此而变得有点儿 冗长，但我认为DOM Core方法更容易使用。当然，你不必和我一样，完全可以根据个人喜好和 具体情况来做出选择。我会尽可能地告诉你，在哪些地方可以用HTML-DOM来简化代码。
6.9小结
在本章里，我对图片库进行了多项优化，我的HTML标记变得更加整齐。我还为我的图片 库网页提供了一个基本的CSS。当然，最重要的是改进了 JavaScript代码。下面是我在本章完成 的几项主要工作。

6.9 小结 95
□尽量让我的JavaScript代码不再依赖于那些没有保证的假设，为此我引入了许多项测试和 检査。这些测试和检査使我的JavaScript代码能够平稳退化。
口没有使用onkeypress事件处理函数，这使我的JavaScript代码的可访问性得到了保证。 □最重要的是把事件处理函数从标记文档分离到了一个外部的JavaScript文件。这使我的 JavaScript代码不再依赖于HTML文档的内容和结构。	_
图6-4是图片库在经过本章的种种优化之后的样子。	^

^	图 6-4
我认为，结构与行为的分离程度越大越好。
在图片库的标记文档部分还有一些内容让我感到不太满意。比如说，placeholder和 riptlon元素是单纯为了 showPic函数而存在的，但不支持或禁用了 JavaScript功能的浏览器 f番会把它们呈现出来，这就难免会给访问者带来不便甚至是困扰。
理想的情况是，让这两个元素只在遇到那些支持DOM的浏览器时才出现在HTML文档里。 芒下一章里，你将会看到如何利用DOM提供的方法和属性去创建HTML元素，并把它们插入 HTML文档的。



