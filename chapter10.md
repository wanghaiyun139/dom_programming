# JavaScript Dom编程艺术

- [第10章 用JavaScript实现动画效果](chapter10.md)
  - [10.1 动画基础知识](chapter10.md#101)
    - [10.11 位置](chapter10.md#1011)
    - [10.12 时间](chapter10.md#1012)
    - [10.13 时间递增量](chapter10.md#1013)
    - [10.14 抽象](chapter10.md#1014)
  - [10.2 实用的动画](chapter10.md#102)
    - [10.21 提出问题](chapter10.md#1021)
    - [10.22 解决问题](chapter10.md#1022)
    - [10.23 CSS](chapter10.md#1023)
    - [10.24 JavaScript](chapter10.md#1024)
    - [10.25 变量作用域问题](chapter10.md#1025)
    - [10.26 改进动画效果](chapter10.md#1026)
    - [10.27 添加安全检查](chapter10.md#1027)
    - [10.28 生成HTML标记](chapter10.md#1028)
  - [10.3 小结](chapter10.md#103)


10.1动画基础知识
前面的章节介绍了如何利用DOM技术修改文档的样式信息。用JavaScript添加样式信息可 以节约你的时间和精力，但总的来说，CSS仍是完成这类任务的最佳工具。
不过，有一个应用领域是目前的CSS尚且无能为力的。如果我们想随着时间的变化而不断 改变某个元素的样式，则只能使用JavaScript。JavaScript能够按照预定的时间间隔重复调用一个 函数，而这意味着我们可以随着时间的推移而不断改变某个元素的样式。
动画是样式随时间变化的完美例子之一。简单地说，动画就是让元素的位置随着时间而不断 地发生变化。	_
位置
网页元素在浏览器窗口里的位置是一种表示性的信息。因此，位置信息通常是由css负责 设置的。下面这些css代码对某个元素在网页上的位置做出了规定：
这将把元素摆放到距离浏览器窗口的左边界100像素，距离浏览器窗口的上边界50 像素的位置上。下面是实现同样效果的DOM代码：
element {
position: absolute; top: 5〇px; left: lOOpx;
element. style • position = "absolute11; element •style •left = !,l〇〇px,f; element, style, top = n5〇px,f;

10.1动画基础知识	173
position 属性的合法值有 statric、fixed、relative 和 absolute 四种。static是 position 属性 的默认值，意思是有关元素将按照它们在标记里出现的先后顺序出现在浏览器窗口里。relative 的含义与static相似，区别是position属性等于relative的元素还可以（通过应用float属性）
从文档的正常显示顺序里脱离出来。
如果把某个元素的position属性设置为absolute，我们就可以把它摆放到容纳它的“容器” 的任何位置。这个容器要么是文档本身，要么是一个有着fixed或absolute属性的父元素。这个 元素在原始标记里出现的位置与它的显示位置无关，因为它的显示位置由top、left、right和 bottom等属性决定。你可以使用像素或百分比作为单位设置这些属性的值。
设置一个元素的top属性将把该元素摆放到距文档顶特定距离的位置，一个元素的bottom属 性将把该元素摆放到距文档底边界特定距离的位置。类似地，left或right属性可用来分别把该 元素摆放到距文档左边界或右边界特定距离的位置。为防止它们发生冲突，最好只使用top或只 使用bottom属性；left或right属性也是如此。
把文档里的某个元素摆放到一个特定的位置是很容易的事。不妨假设有一个这样的元素：
<p id=Mmessageu>Whee!</p>
于是，你可以用一个JavaScript函数来设置这个元素的位置：
function positionMessage() { if (!document•getElementByld) return false; if (! document •getElementByld^11 message11)) return false; var elem = document•getElementById(,fmessage11); elerru style .position = ” absolute"; elem•style,left = ”5〇pxn; elem • style .top - nl〇〇pxlf;
}
在页面加载时调用这个posItlonMessage函数，会把这段文本摆放到距浏览器窗口的左边界 50像素、距浏览器窗口的顶边界100像素的位置：
window«onload = positionMessage;
不过，最好是用addLoadEvent函数来完成，如下所示：
function addLoadEvent(func) { • var oldonload = window^onload; if (typeof window.onload != 'function1) { window^onload = func;
} else {
window.onload = function() { oldonload(); func〇;
addLoadEvent(positionMessage);
图10-1是按P〇s1t1on="absolute"的情况来摆放这个元素的效果。







174 第10章用JavaScript实现动画效果
图 10-1	.1
• i
改变某个元素的位置也很简单，只要执行一个函数去改变这个元素的style.top或style.left"
等属性就行了 ：
千unction moveMessage() { if (!document,getElementById) return false; if (!document•getElementById(f,message11)) return false; var elem = document •get ElementById(tfmessage,t); elem. style, left = "200pxf’；
1
编写一个这样的函数并不难，问题是该如何去调用这个函数呢？如果让moveMessage函数在 页面加载时运行，这个元素的位置将立刻发生变化——由posItlonMessage函数给出的原始位置会 被立刻覆盖：
addLoadEvent(positionMessage);
addLoadEvent(moveMessage);	,
如图10_2所示，这个元素的显示位置立刻发生了变化。





W 夂 1




♦，籙1 S免陳
]© C 0

图 10-2
元素的显示位置立刻发生变化并不是我们想要的动画效果。要获得真正的动画效果，必须让 元素的位置随着时间不断地发生变化。

10.1 动画基础知识	175
导致元素的显示位置立刻发生变化的根源是JavaScript太有效率了 ：函数一个接一个地执行， 其间根本没有我们所能察觉的间隔。为了实现动画效果，我们必须“创造”出时间间隔来，而这 正是我们将要探讨的问题。
1〇_1.2时间
JavaScript函数setTimeout能够让某个函数在经过一段预定的时间之后才开始执行。这个函 数带有两个参数：第一个参数通常是一个字符串，其内容是将要执行的那个函数的名字；第二个 参数是一个数值，它以毫秒为单位设定了需要经过多长时间后才开始执行第一个参数所给出的函 数：
$etTimeout(ff/w/?ctionfl, interval)
在绝大多数时候，把这个函数调用赋值给一个变量将是个好主意：
variable = setJimeoutCJunction99 ^interval)
如果想取消某个正在排队等待执行的函数，就必须事先像上面这样把setTImeout函数的返回 值赋值给一个变量。你可以用一个名为clearTImeout的函数来取消“等待执行”队列里的某个函 数。这个函数需要一个参数	保存着某个setTImeout函数调用返回值的变量：
cleBrTimeout(variable)
修改posItlonMessage函数，让它在5秒（或者说5000毫秒）之后才去调用moveMessage函数:
function positionMessage() {	—
if (!document•getElementByld) return false; if (!document.getElementById(Hmessagefl)) return false; var elem = document^getElementById(l,messagen); elem.style•position = ”absolute"; elenustyle.left = ”5〇pxn; elem • style • top = ni〇〇px!,; movement = setTimeout(i,moveMessage(),lJ5〇〇〇)；
posItlonMessage函数仍将在页面加载时得到执行：
addLoadEvent(positionMessage);
这样一来，那条消息将先出现在它的原始位置上，然后在5秒之后才向右“跳跃” 150像素。
在那5秒钟的等待时间里，我可以随时使用下面这条语句取消这一 “跳跃”行为：
clearTimeout(movement);
movement变量对应着在posItlonMessage函数里定义的setTImeout调用。它是一个全局变量， 我在声明它时未使用关键字var。这意味着那个“跳跃”行为可以在posItlonMessage函数以外的 免方被取消。
10.1.3时间递增量
把某个元素在5秒钟之后向右移动150像素的显示效果称为动画实在有点儿勉强。真正的动 效果是一个渐变的过程，元素应该从出发点逐步地移动到目的地，而不是从出发点一下子跳跃

176 第10章用JavaScript实现动画效果
到目的地。
我们更新一下moveMessage函数，让元素的移动以渐变的方式发生。下面是新_eMessage函 数的逻辑。
获得元素的当前位置。
如果元素已经到达它的目的地，则退出这个函数。
如果元素尚未到达它的目的地，则把它向目的地移近一点儿。
经过一段时间间隔之后从步骤1开始重复上述步骤。
第一步是确定元素的当前位置。这一点可以通过査询元素的style.top和style.left等位置 属性做到。我们把styl e. top和styl e. 1 eft属性的值分别赋给变量xpos和ypos:
var xpos = eleirustyle• left;
var ypos = elenustyle_topj
当moveMessage函数在posItlonMessage函数之后被调用时，xpos变量将被赋值为50px，ypos 变量将被赋值为l〇〇px。我遇到了一点儿小麻烦：这两个值都是字符串，而接下来的代码需要进 行许多算术比较操作。我需要的是数，不是字符串。
JavaScript函数parselnt可以把字符串里的数值信息提取出来。如果把一个以数字开头的字符 串传递给这个函数，它将返回一个数值：
paxselr\t(string)
下面是一个例子：
parselnt(fl39 steps'1);
这个函数调用将返回数值“39”（不包括引号)。
parselnt函数的返回值通常是整数。如果需要提取的是带小数点的数值（也就是浮点数)，就 应该使用相应的parseFloat函数：
parseFloat(strirtg)
我们在_eMessage函数里只与整数打交道，所以使用parselnt函数：
var xpos = parselnt(elem.style.left);
var ypos = parselnt(eleir)^style.top);
parselnt函数将把字符串“50px”转换为整数50,把字符串“100px”转换为整数100。现在， xpos和ypos变量分别包含整数50和100。
注意只有使用了 DOM脚本或style属性为元素分配了位置后，这里的parselnt函数才起作用。
在moveMessage函数里，接下来的几个步骤需要用到大量的比较操作符。
第一次测试是否相等，我们需要知道变量xpos和ypos的值是否等于目的地那里的“左” 位置和“上”位置。如果是，退出这个函数。相等操作符由两个等号构成。（记住，一个等号是 赋值。）

if (xpos 200 && ypos == 100) { return true;
10.1动画基础知识	177
如果mesage元素还没有到达它的目的地，则继续执行下面的代码。
接下来，根据mesage元素的当前位置及其目的地的关系更新变量xpos和ypos的值。我们希 望把它们移动到一个距目的坐标更近的地方。如果xpos小于终点的left,给它加1:
if (xpos < 200) { xpos++;
如果xpos大于终点的left，给它减1:
if (xpos > 200) { xpos--;
根据ypos的值和终点top的关系，对变量ypos进行类似的更新：
if (ypos < 1〇〇) { ypos++;
if (ypos > 100) {
1 ypos—;
现在，你知道把变量xpos和ypos由字符串转换为数的原因了：我要用大于和小于操作符进 行数值比较，并根据比较的结果更新它们的值。
接下来，需要把变量xpos和ypos的值应用到mesage元素的style属性。我们需要把字符串 *px”追加到这两个值的末尾，并把它们赋给left和top属性：
elerru style, left = xpos + "px__; elerru style, top = ypos + "px";
最后，我们需要在一个短暂的停顿之后重复执行这个函数。我们把停顿时间设置为百分之一 秒，也就是10毫秒：
movement = setTimeout(tlmoveMessage()n,iO);
下面是moveMessage函数的代码清单：
function moveMessage() { if (!document•getElementByld) return false; if <!document•getElementByld("message")) return false; var elem = document,getElefnentById("message”）； var xpos = parselnt(elem*style♦left); var ypos = parselnt(elem.style^top); if (xpos == 200 && ypos == 100) { return true;
if (xpos < 200) { xpos++;
if (xpos > 200) { xpos--;

178 第10章用JavaScript实现动画效果
if (ypos < 100) { ypos++;
}
if (ypos > 100) { ypos--;
}
elem. style, left = xpos + npxlf;
elenu style•top = ypos + "px”；
movement = setTimeout(l,moveMessage()n>lO);
>
这个函数使得message元素以每次1像素的方式在浏览器窗口里移动。一旦这个元素的top 和left属性同时等于100px和200px，这个函数就停止执行。这可是实实在在的动画效果——虽 然它没有什么实际的意义。稍后，我们将利用同样的原理实现一个有实用价值的例子。
1〇丄4抽象
刚才编写的moveMessage函数只能完成一项非常特定的任务。它将把一个特定的元素移动到 一个特定的位置，两次移动之间的停顿时间也是一段固定的长度。所有这些信息都是硬编码在函 数代码里的：‘
function moveMessage() { if (!document.getEiementByld) return false; if (!document♦getElementById(flinessagen)) return false;
var elem = document^getElementById(iImessagen);
var xpos = parselnt(elem^style.left); var ypos = parselnt(elem.style♦top); i千（xpos == 200 && ypos == 100) { return true;
}
if (xpos < 2〇o) { xpos++;
}
if (XpOS > 200) {
xpos—;
}
if (ypos < ioo) { ypos++;
}
if (ypos > ioo) { ypos—;
}
elem •style, left = xpos + upxf,; elem • style .top = ypos + ”px"; movement = setTimeout(,lmoveMessage()lt,iO);
如果把这些常数都改为变量，这个函数的灵活性和适用范围就会大大提高。通过 moveMessage函数进行抽象，你可以让它变得更加通用（便于重用）。
1.创建moveElement函数
把新函数命名为moveElement。与moveMessage函数不同，新函数的参数将会有多个。
每次调用这个新函数时可能变化的东西。
F面是

10.1 动画基础知识	179
打算移动的元素的ID。
该元素的目的地的“左”位置。
该元素的目的地的“上”位置。
两次移动之间的停顿时间。
这些参数都应该取一个描述性的名字：
elementID
final_x
final—y
interval
定义moveElement函数的第一步是声明它的各个参数：
function moveElemerrt(elementID,final_x,final一y,interval) {
用这些变量把前面硬编码在moveMessage函数里的有关常数全部替换掉。在moveMessage函数 开头是以下几条语句：
if (! document	return false;
if (!document•getElementById(Hmessagen)) return false;
^ var elem = document •get ElementById(tTmessageM);
j	把这几条语句里的 getElementById("message")全部替换为 getElementByld (elementID):
if (!document•getElementByld) return false; if (!document♦getElementByld(elementID)) return false; var elem = document•getElementByld(elementlD);
elem变量现在对应着你想移动的任何元素。
接下来的两行语句用不着修改。它们负责把给定元素的left和top属性转换为数值，并把转 果分别赋值给变量xpos和ypos:
var xpos var ypos


parselnt(elei style•left);
parselnt(elem•style.top);
接下来，检査给定元素是否已经到达目的地。在moveMessage函数里，目的地的坐标值是200 left位置）和100 (top位置）。
if (xpos == 200 && ypos == 100) { return true;
}
在moveElement函数里，目的地坐标值将由变量finalj(和final』提供：
if (xpos == final一x && ypos == finally) { return true;
>
再往后是对变量xpos和ypos进行刷新的几条语句。如果变量xpos的值小于目的地的“左” 置，给它加1。
原来的目的地的top位置是硬编码在函数代码里的常数200:
if (xpos < 200) {
XD0S++；

180 第10章用JavaScript实现动画效果
现在的目的地的1 eft位置由变量f 1 nal_x提供：
if (xpos < finaljc) { xpos++;
}
类似地，如果xpos大于目的地的left位置，xpos减1:
if (xpos > final_x) { xpos—;
}
对负责更新变量:/P〇s的语句做同样的修改。如果ypos小于final_y，给它加1;如果它大于 final_y，给它减 1:
if (ypos < finally) { ypos++;
}
if (ypos > finally) {	•
yp〇s--;
} ^
接下来的两行语句不用修改。它们负责把字符串"px"追加到变量xpos和ypos的末尾，并将 其赋值给el em元素的1 eft和top样式属性：
elenu style•left = xpos + "px"; elenu style•top = ypos + "px";
最后，在经过一段适当的时间间隔之后再次调用同一个函数。在moveMessage函数里，这个 环节相当简单：每隔10毫秒调用一次moveMessage函数：
movement = setTimeout(,,moveMessage(),,,l〇);
在moveElement函数里，事情变得有一点儿复杂。因为在下一次调用moveElement时，我们还 需要把elementID、final_x、finalj/和Interval等参数传给它。这将形成一个如下所示的字符串：
"moveElement(!"+elementID+"l,H+final_x+u,"+final_y+","+interval+")"
字符串拼接操作实在不少！与其把一个这么长的字符串直接插入到setTImeout函数里去，不 如先把这个字符串赋值给repeat变量：
var repeat = "moveElement("*+elementID+"、"+final-X+"/+firial-y+"/+interval+")";
现在，我们只需把repeat变量插入到setTImeout函数里作为它的第一个参数就行了。第二个 参数是再次调用第一个参数所指定的函数之前需要等待的时间间隔。这个间隔在moveMessage函 数里被硬编码为10毫秒，它现在将由变量interval提供：
movement = setTimeout(repeat,interval);
用一个右花括号结束这个函数：
>
下面是moveElement函数的代码清单：
干unction moveElement(elementID,final_x,finally, into { if (!document.getElementByld) return false;

10.1 动画基础知识	181
if (!document^getElementById(elementID)) return false;
var elem = document•getElementByld(elementlD);
var xpos = parselnt(elem^style^left);
var ypos = parselnt(elem.style.top);
if (xpos -= final_x && ypos == final_y) { return true;
}
if (xpos < final_x) { xpos++;
}
if (xpos > final_x) { xpos--;
}
if (ypos < final_y) {
ypos++;
}
if (ypos > finally) { ypos-;	~
}
elem. style, left = xpos + Irpx"; elerru style • top = ypos + "px”；
var repeat = llmoveElement(’’’+elernentID+"l,"+final_x+”,"+final_y+”/’+interval+")"; movement = setTimeout(repeat>interval);
把moveElement函数保存为moveElementJs文件。把这个文件放入scripts文件夹，别忘了把 丨LoadEvent. js文件也放到那里。
2.使用moveElement函数 现在，我们来测试一下这个函数。
首先重新创建前面的示例，创建一个名为message.html的文档，让它包含一个Id属性值是 ssage的文本段：
<!D0CTYPE html>
<html lang=MenM>
<head>
<meta charset=Mutf-8n />
<title>Message</title>	•
</head>
<body>
<p id=lfmessagen>Whee!</p>
</body>
</html>
要想看到动画效果，我们必须先设定它的初始位置。编写一个名为posItlonMessage.js的 JavaScript文件。在 posItlonMessage 函数的末尾，调用 moveElement 函数：
function positionMessage() {
if (!document•getElementByld) return false;
if (! document •getElementByld (lr message11)) return false;
var elem = document •getElementByld(11 message11);
elem. style • position = ” absolute1’；
elem •style •left = n5〇px,f;
elem•style•top = "lOOpx";
moveElement ("message’1,2〇〇, 100,10) j
}
addLoadEvent(positionMe^ssage);
上面这段代码中的moveElement函数调用语句将把字符串值“message”传递给elementID参

182 第10章用JavaScript实现动画效果
数，把数值200传递给f1nal_x参数，把数值100传递给final)参数，把数值10传递给intend 参数。	I
scripts 文件夹现在包含三个文件：addLoadEvent.js、posItlonMessage.js 和I moveEleinent.jsl 我们需要在message.html文档里插入一些<scr1pt>标签来引用这几个脚本文件，如下所示：|
<!D0CTYPE html>
<html lang=Menlf>
<head>
<meta charset=Hutf-8n />
<title>Message</title>
</head>
<body>
<p id=!ifnessageM>Whee!</p>
<script src=,fscripts/addLoadEvent^jsffx/script>
<script src=lfscripts/positionMessage#js,?x/script>
<script src=lfscripts/moveElement^jsl,x/script>
</body>
</html>
■


现在，把message.html文档加载到一个Web浏览器里就可以看到我们所实现的动画效果7? 如图10-3所示，那个元素将在浏览器窗口里横向移动。	|
WlioeWheemcc Wheel

图 10-3

至此，一切都进行得很顺利。moveElement函数与moveMessage函数的效果完全一样。不过
因为我们已经对这个函数进行过抽象处理，所以现在可以把任意的参数传递给它。比如说，^
改变参数1"^1^(和finally的值，就可以改变动画的移动方向；如果改变参数"interval的
就可以改变动画的移动速度：	I

function moveElement(elementID>final_x>final_y,interval)
在posItlonMessage. js文件里修改posi'fionMessage函数的最后一行，让这三个值发生点儿
function positionMessage() {
if (!document.getElementByld) return false;
if (!document•getElementById(,,[nessage,1)) return false;
var elem = docufnent^getElementById(f,messageM);
elem.style.position = "absolute";
elem•style♦left = "5〇px”；
elem.style.top = "lOOpx”；
moveElement (,f message11,125>25,20) j

addLoadEvent(positionMessage);

10.1 动画基础知识	183
在Web浏览器里刷新message.htrrH文件，就可以看到新的动画效果了：那个元素现在将斜向 移动，移动的速度也变慢了，如图10-4所示。



还可以改变nioveElement函数的element ID参数值：
干unction moveElement(elementID,final_xJfinally,interval)
在message.html文件里增加一个新元素，把它的Id属性设置为message2:
<!D0CTYPE html> chtml lang="en">
<head>
<meta charset=lfutf-8M />
<title>Message</title>
</head>
<body>
<p id=,tmessage,l>Whee!</p>
<p id="message2">Whoa!</p>
<script src=!,scripts/addLoadEvent^jsrrx/script>
〈script src=lfscripts/positionMessage^jsfrx/script> xscript src=,rscripts/moveElement.jsnx/script>
</body>
</html>
现在，在posItlonMessage.js文件里增加一些代码。先为message2元素设定一个初始位置， 然后增加一条moveElement函数调用语句	把message〗作为它的第一个参数传递：
function positionMessage() { if (!documentsgetElementByld) return false; if (! documents get ElementById(,f message1')) return false; var elem = document •getElementById(11 messagetr); elem•style•position = "absolute"; elenustyle.left = "5〇px"; elem.style,top = "l〇〇px"; moveElement(M(nessagen,l25>25,2〇);
if (!document^getElementById(flmessage2,f)) return false; var elem = document.getElem€ntById(!lmessage2,f)j elem •style •position = "absolute’1; elem • style • left = 115〇px"; elenustyle.top = "5〇px”；

184 第10章用JavaScript实现动画效果
moveElement("message2", 125,125,20);
}
addLoadEvent(positionMessage);
在Web浏览器里刷新message.html文件就可以看到新的动画效果了，如图10-5所示。两个 元素将沿着不同的方向同时移动。
傷0:覷巧寒漁滅；秀爾，

圈0 C %
Whos!
W!
Wfe
Whee*
/ *kC 4
€tefi«

* ^-iV ^ • :».-Ah; Jt
图 10-5
在这两个例子里，所有工作都是moveElement函数完成的。只需简单地改变一下传递给这个 函数的参数值，你就可以随意重用它。这正是用参数变量代替硬编码常数的最大好处。
10.2实用的动画	广
有了 irioveElement这个通用的函数，你就可以用它沿任意方向移动页面元素。从程序设' 的角度看，这会给人留下相当深刻的印象；但从实用的角度看，它的意义似乎并不大。
网页上的动画元素不仅容易引起访问者的反感，还容易导致各种各样的可访问性问题。W3C 在它们的Web Content Accessibility Guidelines (Web内容可访问性指南）7.2节里给出了这样的建
议：“除非浏览器允许用户“冻结”移动着的内容，否则就应该避免让内容在页面中移动。（优先 级2)。如果页面上有移动着的内容，就应该用脚本或插件的机制允许用户冻结这种移动或动态更 新行为。”	,
这里的关键在于用 > 能不能控制。解决了这个问题，根据用户行为移动一个页面元素可能 到增强网页的效果。让我们看一个能够起到增强页面效果的例子。
10.2.1提出问题
我们有一个包含一系列链接的网页。当用户把鼠标指针悬停在其中的某个链接上时，我们想 用一种先睹为快的方式告诉用户这个链接将把他们带往何方。我们可以展示一张预览图片。
这个网页的基本文档是11st:html文件，下面是它的代码清单:

















10.2 实用的动画 185
<!D0CTYPE html>
<html lang=Men!l>
<head>
<meta charset="utf-8u />
<title>Web De$ign</title>
</head>
<body>
<hl>Web Design</hl>
<p>These are the things you should know“/p>	-
<ol id="linklist">
<li>
<a href=MstrMcture^htmln>Structure</a>
</li>
<li>
<a href=flpresentation•htmlf,>Presentation</a>
</li>
<li>
<a href=f,behavior•htmllf>Behavior</a>
</li>
</ol>
</body>
</html>
这个网页里的每个链接分别指向一个介绍相关网页设计技巧的页面。这些链接内文本已经简 单介绍了目标页面的内容（如图10-6所示)。
'©：© ©
::觀尋:.驗_賴麵睡麵u.:..: ' .







Web Design
These are things you should know
Sdructiae
PresentatkHi
Behavior
1©,C- 0

图 10-6
事实上这个网页已经足够完美。也就是说，为它增加一种视觉提示效果会让这个网页更有吸 引力。	，
从某种意义上讲，这个案例与我们在本书前面的有关章节里实现的图片库颇为相似：它们都 包含着一系列链接，我想对它们做的改进都是显示一张图片。但我们这一次要在onmouseover事 件（请注意，不是oncllck事件）被触发时显示一张图片。
我们将沿用图片库案例中的脚本——只需把每个链接上的事件处理函数从oncllck改为 onmouseover。它能工作，但图片显示得不够流畅：当用户第一次把鼠标指针悬停在某个链接上时， 新图片将被加载过去。即使是在一个髙速的网络连接上，这多少也需要花费点儿时间，而我们希 望能够立刻响应。

186 第10章用JavaScript实现动画效果
1022解决问题
如果为每个链接分别准备一张预览图片，在切换显示这些图片时总会有一些延迟。除此之外， 简单地切换显示这些图片也不是我们期望的效果。我们想要的是一种更快更好的东西。
下面是我们要做的事情。
□为所有的预览图片生成为一张“集体照”形式的图片。
□隐藏这张“集体照”图片的绝大部分。
□当用户把鼠标指针悬停在某个链接的上方时，只显示这张“集体照”图片的相应部分。 我已经制作出了一张这样的“集体照”图片，它由三张预览图片和一张默认图片构成，如图1〇-7 所示。
Choose a topic









图 10-7
这个图片的文件名是top1cs.gif。它的宽度是400像素，髙度是100像素。
我们把top1cs.gif图片插入到11st.html文档里，并把这个图片元素的Id属性设置为preview:
<!D0CTYPE html>
<html lang=flenf,>
<head>
<meta charset=,,utf-8H />
<title>Web Design</title>
</head>
<body>
<hl>Web Design</hl>
<p>These are the things you should knowx/p>
<ol id="linklist">
<li>
<a href=ffstructure.htmlM>Structure</a>
</li>	,
<li>
<a href=,,presentation^html,l>Presentation</a>
</li>
<li>
<a href=flbehavior.html,f>Behavior</a>
</li>
</ol>
<img src=l,images/topics^gif11 alt=Mbuilding blocks of web design11 id="preview" />
</body>
</html>
图10-8是带着那些链接和那张“集体照”图片的网页显示效果。

10.2实用的动画 187



图 10-8
现在，整张“集体照”图片都是可见的。每次我们都只想让这个图片的某个100x100像素 的部分出现。我们无法用JavaScript做到这一点，但可以用CSS来做。
CSS
CSS的overflow属性用来处理一个元素的尺寸超出其容器尺寸的情况。当一个元素包含的内 容超出自身的大小时，就会发生内容溢出，这种情况，你可以对内容进行“裁剪”，只让一部分 内容可见。你还可以通过overflow属性告诉浏览器是否需要显示滚动条，以便让用户能够看到内 容的其余部分。
overflow属性的可取值有 4种：visible、hidden、scroll 和 auto。
visible:不裁剪溢出的内容。浏览器将把溢出的内容呈现在其容器元素的显示区域以外， 全部内容都可见。
hidden:隐藏溢出的内容。内容只显示在其容器元素的显示区域里，这意味着只有一部分 内容可见。
scroll:类似于hidden，浏览器将对溢出的内容进行隐藏，但显示一个滚动条以便让用户 能够滚动看到内容的其他部分。
auto:类似于scroll，但浏览器只在确实发生溢出时才显示滚动条。如果内容没有溢出， 就不显示滚动条。
如此说来，在overflow属性的4种可取值当中，最能满足我们要求的显然是hidden。我们有 张实际尺寸是400x 100像素的图片，但我每次只想显示这张图片中一个尺寸为100像素x 100 素的部分。
首先，需要把这张图片放到一个容器元素。我们把它放入一个dlv元素，并把这个dlv元素

188 第10章用JavaScript实现动画效果
的Id属性值设置为slideshow:
<div id=HslideshowH>
<img src=,,images/topics.gifH alt="building blocks of web design11 id=ffpreviewM /> </div>
创建一个样式表文件layout.css，把它放入styles文件夹。
在layout.css文件里，我们对IcKslIdeshow"的dlv元素的尺寸做了如下设置:
#slideshow { width: 100px; height: lOOpx; position: relative;
把position设置为relative很重要，因为我们想让子图片使用绝对位置。通过使用值 relative，子元素的(0,0)坐标将固定在slideshow dlv的左上角。
把CSS overflow属性设置为hidden,就能确保其中的内容会被裁剪：
#slide$how { width: l〇〇px; height: lOOpx; position: relative; overflow: hidden;
接下来，我们添加一个<11nk>标签，把layout.css样式表引入"Mst.html文档：
<!D0CTYPE html>
<html lang="enM>
<head>
<meta charset=,!utf-8fl />
<title>Web Design</title>
<link rel=f,stylesheet,T href=nstyles/layout^cssM media=flscreen11 />
</head>	•
<body>
<hl>Web Design</hl>
<p>These are the things you should know.</p>
<ol id=Mlinklistn>
<li>
<a href=ffstructure.htmlrf>Structure</a>
</li>	,
<li>
<a href=llpresentation.html,l>Presentation</a>
</li>
<li>
<a href=nbehavior•html,l>Behavior</a>
</li>
</ol>	一
<div id="slideshow">
<img src=,fimages/topics»gifn alt=,fbuilding blocks o干 web design" id=f,preview11 />
</div>
</body>
</html>
现在，把11st.html文档加载到浏览器，就可以看到变化（图片已经被裁剪)。我们只能看到 top化s.gif图片的一部分——它的第一个100像素宽的部分，如图10-9所示。











10.2 实用的动画 189
00©
Web Design














Q C Q
Web Design
These are the tfiings you should know.
K Stmctti坨 2. Pte^eniation 3 秦 Bdiavbr
Choose
a topic
Done
图 10-9
接下来要解决的问题是，让这个网页对用户的操作行为做出正确的响应。我们想在用户把鼠 标指针悬停在某个链接上时，把top1cs.gif图片中与之对应的那个部分显示出来。这是一种行为 上的变化：用JavaScript和DOM来实现再合适不过了。
JavaScript
我们计划用moveElement函数来移动top1cs.gif图片。根据用户正把鼠标指针悬停在哪个链 接上，我们将这个图片向左或向右移动。
我们需要把调用moveElement函数的行为，与链接清单里每个链接的onmouseover事件关联起 来。
编写一个p「epareS11deshow函数来完成这项工作，下面是它的代码清单：
function prepareSlideshow() {
//确保浏览器支持DOM方法	‘
if (!document•getElementsByTagName) return 干alse; if (!document•getElementByld) return false;
//确保元素存在
if (!document.getElementById(,llinklist,f)) return false; if (!document^getElementById(npreview,f)) return false;
//为图片应用样式
var preview = documents get ElementById(,rpreviewn); preview^style•position = "absolute”； preview.style♦left = "Opx"; preview • style • top = _’0px";
//取得列表中的所有链接
var list = document.getElementById(nlinklist11); var links = list.getElementsByTagName(uafT);
//为mouseover事件添加动画效果 links[0]•onmouseover = function() { moveElement(,'preview'%-100,0,10);
}
links[l]t〇nmouseover = function() { moveElement(l,previewM>-200,0,10);

190 第10章用JavaScript实现动画效果
links[2].onmouseover = function() { moveElement("preview",-300,0,10);
}
}
首先，prepareSlIdeshow函数检查浏览器是否支持它用到的DOM方法：
if (!document•getElementsByTagName) return false; if (!document♦getElementByld) return false;
接着，检査llnkllst和preview元素是否存在。别忘了，preview是top1cs.gif图片的Id属 性值：
if (!document.getElementById(Hlinklistfl)) return false; if (!document•getElementById(11 preview11)) return false;
此后，为preview图片设定一个默认位置。我将把它的style.left属性设置为Opx，把它的 style.top属性也设置为Opx:
var preview = document^getEleinentById(,,previewn); preview.style♦position = "absolute"; preview•style•left = "Opx”； preview•style,top = "0pxH;
请注意，这并不意味着toplcs.glf图片将出现在浏览器窗口的左上角。它将出现在它的容器 元素，也就是那个Id属性值是slideshow的dlv元素的左上角。因为那个dlv元素的CSS position 属性值是relative:如果把position属性值是absolute的元素A放入一个position属性值是 rel atl ve的元素B，B就成为A的容器元素，而A将在B的显示区域里按absol ute方式进行摆放。 因此，preview图片将出现在slideshow元素的左上角——与这个dlv元素的左边界和上边界之间 的距离都是〇px。
最后，把onmouseove「行为与链接清单里的各个链接关联起来。首先，把一个由包容在llnkllst 元素里的所有a元素构成的节点集合赋值给变量links。第一个链接对应着11nks[0]，第二个链 接对应着~Mriks[l]，第三个链接对应着11nks[2]:
var list = document•getElementById(ltlinklistM); var links = list*getElementsByTagName(Ma,t);
当用户把鼠标指针悬停在第一个链接上时，moveElement函数将被调用执行。此时，它的 elementID参数的值是preview，flnalj(参数的值是-100，final_y参数的值是0，Interval参数的 值是10毫秒：
links[〇],onmouseover = function() { moveElement(,fpreview?, ,-!〇〇,〇, l〇);
}
第二个链接应该有同样的行为——除了 f1nal_x参数的值变成了-200:
links[1].onmouseover =干unction() { moveElement(,fpreviewM>-200,0,10);
}
第三个链接将把preview图片向左移动-300像素：
links[2].onmouseover = function() {
moveElement(l,preview,,,-3〇〇>〇,l〇)；

10.2实用的动画 191
接下来，用addLoadEvent函数调用prepa「eS"Mdeshow函数，这将使得后者在页面加载时得到 执行并把onmouseover行为绑定到那三个链接上：
addLoadEvent(prepareSlideshow);
把p「epareS11desh〇w函数保存为prepareSlIdeshow. js文件并将其放到scripts文件夹里。把 moveElement.js和addLoadEvent.js文件也放到同一个文件夹中。
为了从11st.html文档里调用这三个脚本，还需要在这个文档的</bociy>标签之前添加一些 〈script〉标签：
<!D0CTYPE html> chtml lang^’en1’〉
<head>
<meta charset=ltutf-8t, />
<title>Web Design</title>
<link rels11 stylesheet,r href=lfstyles/layout昪ss11 itiedia=nscreenu />
</head>
<body>
<hl>Web Design</hl>
<p>These are the things you should know.</p>
<ol id=”linklist__>
<li>
<a href=,fstructure•html,l>Structure</a>
</li>
<li>
<a hre千="presentatioruhtml”>Presentation</a>
</li>
<li>
<a href=f,behavior•htmlll>Behavior</a>
</li>
</〇!>
<div id=,!slideshowM>
<img src=Himages/topicStgifn alt=nbuilding blocks of web design" id=11 preview11 />
</div>
<script srcs^scripts/addLoadEvent^jsHx/script>
<script src=Hscripts/moveElement^jsnx/script>
〈script、src=拻scripts/prepareSlideshow*js"></script>
</body>
</html>
把11st.html文档加载到一个Web浏览器。把
鼠标指针悬停在清单里的某个链接上就可以看到
动画效果，如图10-10所示。
根据鼠标指针正悬停在哪个链接上，
top1cs.gif图片的不同部分将进入我们的视线。
不过，事情好像有点不太对头：如果把鼠标指
针在链接之间快速地来回移动，动画效果将变得混
乱起来。irioveElement函数可能什么地方有问题。



參，潑 IJIIIMm 111,111,11,1 T,VI @ C @
Web Design
These ace the flings you should know.



图 10-10

192 第10章用JavaScript实现动画效果
10.2.5变量作用域问题
动画效果不正确的问题是由一个全局变量引起的。在把moveMessage函数抽象化为moveElement 函数的过程中，我们未对变量movement做任何修改：
function moveElement(elemeritID,干final」/,interval) { if (!document•getElementByld) return false; if (!document.getElementByld(elementlD)) return false; var elem = document.getElementByld(elementlD); var xpos = parselnt(elem.style•left); var ypos = parselnt(elem•style.top); if (xpos == final二x && ypos == finai_y) { return true;
if (xpos < final_x) { xpos++;
if (xpos > final^x) { xpos--;
if (ypos < finally) { ypos++;
if (ypos > finaly) { i ypos--.;
elem. style •left = xpos + "px’f; elem♦style•top = ypos + "px";
var repeat = MmoveElement(,M+elementID+M,J,r+final-x+ll,n+final_y+MJM+interval+,l)M; movement = setTimeout(repeat,interval);
这留下了一个隐患：每当用户把鼠标指针悬停在某个链接上，不管上一次调用是否已经把图 片移动到位，moveElement函数都会被再次调用并试图把这个图片移动到另一个地方去。于是，当 用户在链接之间快速移动鼠标时，movement变量就会像一条拔河绳那样来回变化，而moveElement 函数就会试图把图片同时移动到两个不同的地方去。
如果用户移动鼠标的速度够快，积累在setTImeout队列里的事件就会导致动画效果产生滞 后。为了消除动画滞后的现象，可以用clearTImeout函数清除积累在setTImeout队列里的事件：
clearTimeout(movement);
可是，如果在还没有设置movement变量之前就执行这条语句，我们会收获一个错误。
我不能使用局部变量：
var movement = setTimeout(repeat,interval);
如果这样做，clearTimeout函数调用语句将无法工作，因为局部变量movement在clearTimeout 函数的上下文里不存在。
也就是说，既不能使用全局变量，也不能使用局部变量。我们需要一种介乎它们二者之间的 东西，需要一个只与正在被移动的那个元素有关的变量。
只与某个特定元素有关的变量是存在的。事实上，我们一直在使用它们。那就是“属性”。 到目前为止，我们一直在使用由DOM提供的属性，如element.flrstCIrild、element.styie，

10.2 实用的动画 193
等等。JavaScript允许我们为元素创建属性:
element, property = value
只要愿意，完全可以创建一个名为f〇〇的属性并把它设置为"bar”：
element Aoo = "bar”；
这很像是在创建一个变量，但区别是这个变量专属于某个特定的元素。
我们把变量movement从一个全局变量改变为正在被移动的那个元素（elem元素）的属性。这 样一来，就可以测试它是否已经存在，并在它已经存在的情况下使用clearTImeout函数了：
function moveElement(elementID,final_x>final-y,interval) { if (!document•getElementByld) return 干alsej if (!document.getElementByld(elementlD)) return false; var elem = document•getElementByld(elementlD); if (elem•movement) { ciearTimeout(elenu movement);
}
var xpos = parselnt(elem^style♦left); var ypos = parselnt(elem•style♦top); 1 {
if (xpos == finaljc && ypos == final一y) { return true;
>
if (xpos < final一x) { xpos++;
}
if (xpos > final_x) { xpos—;
}
if (ypos < finally) { ypos++;
}
if (ypos > finally) {
- ypos--;
}
elem • style • left = xpos + Mpxfl;
elem•style.top = ypos + "pxM;	•
var repeat = "moveElement(’"+elementID+"_,"+final_x+","+final_y+lV’+interval+")’’； elem•movement = setTimeout(repeat,interval);
}
于是，不管moveElement函数正在移动的是哪个元素，该元素都将获得一个名为movement的 属性。如果该元素在moveElement函数开始执行时已经有了一个movement属性，就应该用 cleammeout函数对它进行复位。这样一来，即使因为用户快速移动鼠标指针而使得某个元素需 要向不同的方向移动，实际执行的也只有一条setTImeout函数调用语句。
请重新加载11st.html文件。现在，在链接之间快速移动鼠标指针不再有任何问题。setTImeout 队列里不再有积累的事件，动画将随着鼠标指针在链接之间的移动而立刻改变方向。接下来，再 来看看我们还可以对动画效果做哪些改进。
1026改进动画效果
在元素到达由final x和final y参数给出的目的地之前，moveElement函数每次只把它移动

194 第10章用JavaScript实现动画效果
一个像素（lpx)的距离。移动效果很平滑，但移动速度未免有些慢。我们把动画的移动速度加 快一点儿。
仔细看看下面这些简单的代码，它们来自moveElement.js文件：
if (xpos < 干inal_x) { xpos++;
变量xpos是被移动元素的当前左位置，变量final_x是这个元素的目的地的左位置。上面这 段代码的含义是：“如果变量xpos小于变量f1nal_x，就给xpos的值加1。”也就是说，不管那个 元素与它的目的地距离多远，它每次只前进一个像素（lpx)。为了增加趣味性，我们来改变它。
如果那个元素与它的目的地距离较远，就让它每次前进一大步；如果那个元素与它的目的地 距离较近，就让它每次前进一小步。	、
首先，我们需要算出元素与它的目的地之间的距离。如果xpos小于final_x，我们要知道它 们差多少。只要用f1nal_x (目的地的左位置）减去xpos (当前左位置）就可以知道答案：
dist = final_x - xpos;
这个结果就是元素还需要行进的距离。我们决定让元素每次前进这个距离的十分之一。
dist = (final^x - xpos)/i〇;
xpos = xpos + dist;
这将把元素朝它的目的地移动十分之一的距离。选用十分之一的理由是为了计算方便；如果 你愿意，选用其他的值也没问题。
如果xpos与final_x相差500像素，变量dist将等于50。xpos的值将增加50。如果xpos与 final_x相差100像素，xpos的值将增加10。
不过，当xpos与final_x之间的差距小于10的时候，问题来了：用这个差距除以10的结果 将小于1，而我们不可能把一个元素移动不到一个像素的距离。
这个问题可以用Math对象的cell方法来解决，它可以返回不小于dist的值的一个整数。下 面是cell方法的语法：
Math.ceil(nw/wfeer)
这将把浮点数number向“大于”方向舍入为与之最接近的整数。还有一个与此相对的floor 方法，它可以把任意浮点数向“小于”方向舍入为与之最接近的整数。round属性将把任意浮点 数舍入为与之最接近的整数：
Math •千 loor (nw/nhe:r)
Math, round (ww/wfcer)
具体到moveElement函数，我需要向“大于”方向进行舍入。如果错误地选用了 floo「或round 方法，这个元素将永远也不会到达目的地：
dist = Match.ceil((final_x - xpos)/i0); xpos = xpos + dist;
这就解决了 xpos小于final x时的问题：

10.2实用的动画 195
if (xpos < final_x) { dist = Math*ceil((final_x - xpos)/l〇); xpos = xpos + dist;
>
如果xpos大于flnalj(，在计算距离时就应该用xpos减去f1nal_x。把这个减法结果除以10, 大于”舍入为与之最接近的整数，然后赋值给变量dist。此时，我们必须用xpos减去dist 目已让元素更接近它的目的地：
if (xpos > final^x) { dist = Math.ceil((xpos - final—x)/l0); xpos = xpos • dist;
同样的逻辑也适用于变量ypos和final_y:
if (ypos < finally) { dist = Math•ceil((finally - ypos)/i〇); ypos ^ ypos + dist;
}
if (ypos > final_y) { dist = Math#ceil((ypos - final_y)/l〇); ypos = ypos - dist;
不要忘了在xpos和ypos之后声明dl st:
var xpos = parselnt(elem^style.left); var ypos = parselnt(elem^style•top); var dist = 0;
下面是moveElement函数在经过上述改进后的代码清单
function moveElement(elementID,final_x,final_y,interval) { if (!document•getElementByld) return false; if (!document.getElementByld(elementlD)) return false; var elem = document•getElementByld(elementID); if (elem•movement) { clearTimeout(elem•movement);
}
var xpos = parselnt(elem.style•left); var ypos = parselnt(elem.style•top); var dist = 0;
if (xpos == final_x && ypos — final_y) { return true;
>
if (xpos < final_x) { dist = Math•ceil((iinalj< _ xpos)/l〇); xpos = xpos + dist;
} ^ if (xpos > final_x) { dist = Math^ceil((xpos • final_x)/l〇); xpos = xpos • dist;
}
if (ypos < final_y) { dist = Math^ceil((final_y - ypos)/l〇); ypos = ypos + dist;
if (ypos > finally) { dist = Math ♦ceil( (ypos • -finally)/l〇);





196 第10章用JavaScript实现动画效果
ypos = ypos - distj
>
elenu style•left = xpos + "pxn; elem^style^top = ypos + "px";
var repeat = llitioveElernent(l,l+elernentID+,ll/,+final_x+M/l+final_y+!l/l+interval+tl),t; elenu movement = setTimeout(repeat,interval);
}
把这些修改保存到moveElement.js文件。重新加载11st.html就可以看到新的动画效果，如 图10-11所示。

Design ，
m
♦，♦豪@患
〇 e ©
Web Design
These are the filings you should know.
U Stnicttire
2.


• ♦ _ * u
图 10-11
现在，动画效果给人的感觉是更加平滑和迅速。当你第一次把鼠标指针悬停在某个链接上时， 图片将跳跃一大段距离。随着图片越来越接近最终目的地，它会“放慢”自己的脚步。
在(X)HTML、CSS和JavaScript的共同努力下，预期的动画效果终于实现了。一切都显得那
么完美，但凡事都有改进的余地，这一次也不例外。
10.2.7添加安全检查
moveElement函数现在的表现确实非常好，但还有一件事让我不放心：这个函数的开头部分需 要一个假设：
var xpos = parselnt(elem^style^left); var ypos = parselnt(elem.style.top);
看出来了吗？这里需要假设elem元素肯定有一个left样式属性和一个top样式属性。我其 实应该先检査一下这是不是事实。
如果elem元素的left和/或top属性未被设置，我有以下几种选择。首先，可以简单地就此 退出这个函数：
if (!elem•style•left || !elem•style•top) { return false;

10.2 实用的动画 197
如果JavaScript没有读到这些属性，整个函数将静悄悄地结束运行而不是报告出错。
另一种选择是在moveElement函数里为left和top属性分别设置一个默认值：如果这两个属 没有被设置，我将把它们的默认值设置为〇px:
if (!elenustyle•left) { eiem.style.left = "Opx";
>
if (lelem.style^top) { elem^ style, top = n〇pxf,;
>
下面是moveElement函数现在的代码清单：
千unction moveElement(elementID,final一x,finally,interval) { if (!document.getElementByld) return false; if <!documen1^getElementById(elementID)) return false; var elem = document•getElementByld(elementlD); if (elerrumovement) { ciearTimeout(elenumovement);
}
if (!elem^style#left) { eiem.style.left = "opx";
}
if (!elem.style,top) { eleirit style •top = ,r〇pxflj
}
var xpos = parselnt(elem^style.left); var ypos = parselnt(elem^style^top); var dist = 0;
if (xpos == final_x && ypos == final_y) { return true;
>
if (xpos < final_x) { dist = Math.ceil((final_x - xpos)/l0);
xpos = xpos + dist;
}
if (xpos > final_x) {	-
dist = Math.ceil((xpos - final_x)/l〇); xpos = xpos -dist;
}
if (ypos < finally) { dist = Math•ceil((finally - ypos)/l0); ypos = ypos + dist;
>
if (ypos > finally) { dist = Math.ceil((ypos - final_y)/l〇); ypos = ypos • dist;
}
elenu style • left = xpos + Mpx,f; eleiTK style • top = ypos + npxf,;
var repeat = ,lfnoveElernent(,l,+elefnentID+M,/l+final_x+M/t+final_y+H/,+interval+,l)ir; elem.movement = setTimeout(repeat,interval);
}
有了刚才所说的安全措施之后，就用不着再明确地设置preview元素的出发点位置了。这意 味着可以把prepa「eS11deshow函数里的这两条语句删掉：
preview ♦ style • left = "Opx’1; preview.style^top = n〇px";

198 第10章用JavaScript实现动画效果
既然提到了 prepa「eS11deshow函数，就仔细看看它是不是还有地方需要改进。
10.2.8生成HTML标记
list.htnil文档里包含一些只是为了能够用JavaScript代码实现动画效果而存在的标记：
<div id=nslideshow,f>
<img src=nimages/topics.gif11 alt=nbuilding blocks of web design" id="preview" />
</div>
如果用户没有启用JavaScript支持，以上内容就未免太多余了。这里的dlv和img元素纯粹 是为了动画效果才“塞”进来的。既然如此，与其把这些元素硬编码在文档里，不如用JavaScript 代码来生成它们。我们决定在P「epareS11deshow. js文件里做这些事情。
首先，创建chv元素：	-
var slideshow • docufnent*createElement(Hdiv,f);	•	'
slideshow. setAttribute(nidn,M slideshow11);
接着，创建Img元素：
var preview = document.createElement(nimglf); preview.setAttribute(；fsrcM/f images/topics •gifH); preview.setAttribute(flaltM/!building blocks of web design’1); preview^setAttribute(,,id,r,n preview1');
把新创建的Img元素放入新创建的dlv元素：
slideshow^appendChild(preview);
最后，我们想让这些新创建的元素紧跟着出现在链接清单的后面。我们将使用来自本书第7 章的InsertAfter函数来完成这一步骤：
var list = document^getElementById(,llinklistff); insertAfter(slideshow,list);
下面是最终完成的P「印areSlideshow函数的代码清单：
function prepareSlideshow() {
//确保浏览器理解DOM方法 if (!document•getElementsByTagName) return 干alse; if (Idocument.getElementByld) return false;
//确保元素存在
if (!document.getElementById(1!linklist,!)) return false;
var slideshow = documentscreateElement(,rdivf,);
slideshow,setAttribute("idM,"slideshow");
var preview = document •createElement(lfimgff);
preview-setAttribute(_’src%’’images/topics .gif _’）；
preview •set Attribute(,faltl,/Ibuilding blocks of web design11);
preview^setAttribute(fridIT>,,preview,t);
slideshow•appendChild(preview);
var list = document^getElementById(,,linklist11);
insertAfter(slideshow,list);
//取得列表中的所有链接 var links = list^getElementsByTagName(naM);
//为mouseover事件添加动画效果 links[〇]^onmouseover = function() { moveElement(MpreviewM,•!〇〇,〇,l〇);

10.2 实用的动画 199
links[l].onmouseover = function() { moveEiement("preview",-200,0,10);
}
link$[2]f〇nmouseover = function() {
moveElement(npreviewn,-300,〇,i〇);
addLoadEvent(pxepaxeSlideshovj);
接下来，还需要对hst.html文件做一些修改：删除1d="s11deshow"的dlv元素和IcKprevlew" 阁片；添加一组從巾卜标签来调用InsertAfter.js文件。下面是最终完成的11st.html文件的 猜单：
<!D0CTYPE html>
<html lang=Hen">
<head>
<meta charset=,lutf-8H />
<title>Web Design</title>
〈link rel="stylesheet" href=Mstyles/layoirt^css" media="screen" />
</head>
<body>
<hl>Web Design</hl>
<p>These are the things you should know.</p>
<ol id-fflinklistn>
<li>
<a href=nstructure•htmll,>Structure</a>
</li>
<li>
<a hre干="presentatioruhtml">Presentation</a>
</li>
<li>
<a href=,fbehavior•html,,>Behavior</a>
</li>
</ol>
〈script src=,fscripts/addLoadEvent*jsnx/script>
<script src=lfscripts/insertAfter^jsflx/script>
〈script src=flscripts/moveEleinent^js,fx/script>
〈script src=!lscripts/prepareSlideshow.jsnx/script>
</body>
</html>
把InsertAfte「函数写入1nse「tAfte「. js文件，并把它放入scripts文件夹：
function insertAfter(newElementJtargetElement) { var parent = target Element.parentNode; if (parent.lastChild == targetElement) { parent♦appendChild(newElement);
} else {
parent^insertBefore(newElement,targetElement.nextSibling);



^	还需要对样式表文件layout.css做一些修改。因为我们刚才从prepareSlIdeshow.js文件里删
I除了如下所示的一行代码：
preview.style•position = "absolute”；
所以现在需要把以下样式声明添加到layout.css样式表里，这才是样式信息应该属于的地
方:

200 第10章用JavaScript实现动画效果
#slideshow { width: lOOpx; height: lOOpx; position: relative; overflow: hidden;
}
#preview { position: absolute;
现在，在Web浏览器里刷新11st.html文档。从表面上看，功能还是那些功能，行为还是那 些行为。但经过上述改进之后，这份文档的结构层、表示层和行为层已经分离得更加彻底了。如 果在禁用了 JavaScript支持功能的情况下浏览这份文档，动画图片将根本不会出现。
我们用JavaScript实现的动画功能非常完善。如果启用了 JavaScript,这个页面就能根据用户 的操作动作通过动画效果向用户提供一些赏心悦目的视觉反馈；如果没有启用JavaScript,动画 功能将按照我们安排的平稳退化保持静默，不影响用户的浏览体验。	~
如果想进一步加强链接清单和动画图片的视觉联系，可以通过修改layout.css文件去实现一 些更精彩的效果。比如说，可以把动画图片的显示位置从链接清单的下方挪到它的旁边。如果想 让动画部分更加突出的话，还可以给它加上一个边框。
10.3小结
在本章里，我们首先对“动画”进行了定义：随时间变化而改变某个元素在浏览器窗口里的 显示位置。通过结合使用CSS-DOM和JavaScript的setTImeout函数，很容易实现一个简单的动
画。
从技术上讲，实现动画效果并不困难，问题是在实践中应不应该使用动画。动画技术可以让 我们创建出很多种非常酷的效果，但那些四处移动的元素对用户有用或有帮助的场合却并不多。 不过，我们刚才创建的JavaScript动画却是一个例外。我们花了不少功夫才让它有了平滑的动画 效果和平稳退化，最终的结果证明我们付出的努力是非常值得的。我们现在有了一个通用性的函 数，它可以在确有必要创建动画效果时帮上大忙。
下一章将介绍最新的HTML5,你将学会如何利用它的新属性。

已经被整装到一个小集合中，不过也仅仅就是一个集合。HTML5在这个集合中提供了几种旗鼓 相当的技术，让我们可以按需取用或者调用。
例如，在结构层中，HTML5添加了新的标记元素，如<sect1 on>、<a「t1 cl e>、<header^p<footer>3 本书并不想在这里讨论这些新的标签，想知道所有新标记的读者请査看规范（

http://www.w3.org/ TR/html5/)。HTML5还提供了更多交互及媒体元素，例如<ca_s>、〈audio〉和〈video〉。表单得_ 了加强，新增了颜色拾取器、数据选择器、滑动条和进度条。除此之外，你会发现其中很多新X
素都还带有自己的JavaScript和DOM API。	,
在行为层，HTML5规定了 DOM中每个新元素的交互方式，以及新的API。例如，我们可; 以自定义<v1deo>元素的控件，改变其播放方式，<form>元素则支持进度控制，而在<canvas>元素 中，可以绘制各种图形和添加图片及其他对象。
不仅是标记和行为，表现层同样也得到了改进。CSS3的多个模块囊括了高级选择器、渐变、 变换，还有动画。这些模块完全可以替代很多过去需要编写脚本才能实现的效果，比如动画和定 位元素，这些效果在表现层中的位置举足轻重。虽然要实现高级动画效果仍然免不了要编写很多 脚本，但很多简单的交互应该可以跟计时器或JavaScript说拜拜了。
最后，新 JavaScript API 还包括其他很多模块，比如 Geolocation、Storage、Drap-and-Drop、
Socket以及多线程等。
不管打算使用HTML5的什么新特性，请记住：你费尽心思编写的(X)HTML代码仍然有效。 为了与HTML5兼容，你要做的只有一小点改变。想不想把绝大多数文档都“升级”到HTML5? 好，就把文档类型声明改成<!D0CTYPE html>即可。
假如你想让自己的页面验证无误，当然还要把一些废弃的元素替换掉，如把<ac「onym>替换成: <abb「>。不过要知道，验证只是一个工具，它有助于你成为一个好程序员，但它却不是我们追求 的理想。此外，<sect1on>*<art1cle>等新元素在一些老浏览器中也许不会表现得很好，但浏览器 的版本越新，它们的表现就会越好。
第8章我们已经说过了，HTML (包括HTML5)与XHTML相比，对语法的要求要宽松 多。HTML5的目标是和已有的HTML及XHTML文档全部兼容，无论怎么标记文档，无论遵 什么编码规则，都由你说了算。想要关闭所有标签并且做到标记格式良好吗？请便。你懒得关' 所有标签，嫌那样做太麻烦了——没问题。事实上，就连下面这个“缺斤短两”的HTML5文档 也可以完美地通过验证（但愿不会吓着你）：
<!D0CTYPE html>
<meta charset=utf-8 />
<title>This is a valid HTML5 document</title> <p>Try me at http://validator.wB.〇rg/check</p>
抛开验证成功与否不谈，如果你想让自己的工作显得更专业，我猜你一定会自己加上<html>、 <head>^p<body>—无论浏览器会不会为你添加这些基本的结构化元素。
那么，HTML5离我们还有多远？现在我们就可以使用这些令人激动的新特性了吗？答案是: 可以。不过有个前提——尽可能提前检査浏览器对HTML5的支持情况。然而，检査浏览器是 支持全部HTML5特性是不可能的，我们说过，HTML5现在是一个集合，不是一个全有或全
