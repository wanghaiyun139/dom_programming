# JavaScript Dom编程艺术

<h1>第5章 最佳实践</h1>
## 51
<h2>5.1 过去的错误</h2>
## 511
<h3>5.11 不要怪罪JavaScript</h3>
## 512
<h3>5.12 Flash的遭遇</h3>
## 513
<h3>5.13 质疑一切</h3>
## 52
<h2>5.2 平稳退化</h2>
## 521
<h3>5.21 “javascript:”伪协议</h3>
## 522
<h3>5.22 内嵌的事件处理函数</h3>
## 523
<h3>5.23 谁关心这个</h3>
## 53
<h2>5.3 向CSS学习</h2>
## 531
<h3>5.31 结构与样式的分离</h3>
## 532
<h3>5.32 渐进增强</h3>
## 54
<h2>5.4 分离JavaScript</h2>
## 55
<h2>5.5 向后兼容</h2>
## 551
<h3>5.51 对象检测</h3>
## 551
<h3>5.52 浏览器嗅探技术</h3>
## 56
<h2>5.6 性能考虑</h2>
## 561
<h3>5.61 尽量少访问DOM和尽量减少标记</h3>
## 562
<h3>5.62 合并和放置脚本</h3>
## 563
<h3>5.63 压缩脚本</h3>
## 57
<h1>5.7 小结</h1>


我敢说，之所以会有那么多的网站迫不及待地在网页上嵌入一些毫无必要的Flash视频片段， 是因为“大家都有，所以我也要有”的心理而不是因为实际应用的需要。既然别人的网页上有 Hash动画，那么我的网页上也要有Flash动画，有无必要的问题已无人问津了。
JavaScript也遭遇到了类似的命运：人们只关心自己的网页里有没有JavaScript代码，根本不 去考虑那些现成的（尤其是那些由“所见即所得”网页设计工具生成的）JavaScript函数本身有 没有漏洞，以及它们会不会给网页带来负面影响。JavaScript代码被人们剪贴来、剪贴去，结果 弄得网上到处都是似是而非的JavaScript网页，却没人想到应该首先检査一下那些现成的 fevaScript函数是否还需要改进。	'
5.1.3质疑一切	•



不管你想通过JavaScript改变哪个网页的行为，都必须三思而后行。首先要确认：为这个网
更増加这种额外的行为是否确有必要？
网站对JavaScript的滥用已经持续了相当长的时间，因为滥用JavaScript而给自己带来种种
衰烦的网站也绝不是少数。例如，你可以用JavaScript脚本让浏览器窗口在屏幕上四处移动，甚
至让浏览器窗口产生振动效果。
在所有的JavaScript特效当中，最臭名昭著的莫过于那些在人们打开网页时弹出的广告窗口。对
iraScript和DOM脚本编写者来说不幸的是，有不少用户为此干脆彻底禁用了 JavaScript。浏览器厂
赛也在各自的产品里提供了种种内建的广告过滤机制来解决这一问题，但广告还是无孔不入。
弹出的广告窗口和内容覆盖是一个典型的滥用JavaScript的例子。从技术上讲，弹出窗口本
身是一项很实用的功能，它解决了网页设计工作中的一个难题：如何向用户发送信息。但在实践
频繁弹出的广告窗口却让用户不胜其烦。那些弹出窗口必须由用户关闭，而这往往会形成一
丨游拉锯战——用户刚关闭了一个广告窗口，屏幕上又弹出一个。
■ •
那么，这一功能要如何使用户受益呢？
令人感到欣慰的是，这一问题正越来越受到人们的关注，那些不遵循“用户至上”原则的网
兹从长远看，都在自取灭亡。
如果要使用JavaScript，就要确认：这么做会对用户的浏览体验产生怎样的影响？还有个更 ^重要的问题：如果用户的浏览器不支持JavaScript该怎么办？
I.
5.2平稳退化
记住，网站的访问者完全有可能使用的是不支持JavaScript的浏览器，还有一种可能是虽然 满览器支持JavaScript,但用户已经禁用它了（比如，因为讨厌看到弹出广告)。如果没有考虑 爲这种情况，人们在访问你们的网站时就有可能遇到各种各样的麻烦，并因此不再来访问你们
S阚站。
如果正确地使用了 JavaScript脚本，就可以让访问者在他们的浏览器不支持JavaScript的情 芝下仍能顺利地浏览你的网站。这就是所谓的平稳退化（graceMdegmdation)，就是说，虽然某 垄功能无法使用，但最基本的操作仍能顺利完成。

64 第5章最佳实践
我们来看一个在新窗口里打开一个链接的例子。别担心：我们将要讨论的并不是在网页加载 时弹出新窗口。而是在用户点击某个链接时弹出一个新窗口。这其实是一项相当实用的功能。例 如，在许多电子商务网站的结算页面上都有一些指向服务条款或是邮寄费用表的链接，与其让用 户在点击这些链接时被带离当前页面，不如让用户仍停留在当前页面，并用一个弹出窗口来显示 相关信息。
注意应该只在绝对必要的情况下才使用弹出窗口，因为这将牵涉到网页的可访问性问题，例 如，用户使用的屏幕读取软件无法向用户说明弹出了窗口。因此，如果网页上的某个链 接将弹出新窗口，最好在这个链接本身的文字中予以说明。
JavaScript使用window对象的open()方法来创建新的浏览器窗口。这个方法有三个参数：
window.open(url,name,干eatures)
这三个参数都是可选的。
□第一个参数是想在新窗口里打开的网页的URL地址。如果省略这个参数，屏幕上将弹出 一个空白的浏览器窗口。
□第二个参数是新窗口的名字。可以在代码里通过这个名字与新窗口进行通信。
□最后一个参数是一个以逗号分隔的字符串，其内容是新窗口的各种属性。这些属性包括 新窗口的尺寸（宽度和高度）以及新窗口被启用或禁用的各种浏览功能（工具条、菜单 条、初始显示位置，等等)。对于这个参数应该掌握以下原则：新窗口的浏览功能要少而 精。	z
〇pen()方法是使用BOM的一个好案例，它的功能对文档的内容也无任何影响（那是DOM的 地盘)。这个方法只与浏览环境（具体到这个例子，就是window对象）有关。
下面这个函数是window.open()方法的一种典型应用：
function popUp(winURL) {
window^ open (winURL,11 popup11/fwidth=32〇, height=48〇m);
}
这个函数将打开一个320像素宽、480像素高的新窗口 “popup”。因为我在这个函数里已为 新窗口命名，所以当把新的URL地址传递给此函数时，这个函数将把新窗口里的现有文档替换 为新URL地址处的文档，而不是再去创建一个新窗口。
我将把这个函数存入一个外部文件。因此，当需要在某个网页里使用此函数时，只要在这个 网页的<head>部分用一个<script>标签导入那个外部文件即可。函数本身不会对网页的可访问性 产生任何影响，会影响到网页的只是：我将如何使用此函数。
调用popUp函数的一个办法是使用伪协议（pseudo-protocol)。
“javascript:” 伪协议
“真”协议用来在因特网上的计算机之间传输数据包，如HTTP协议(http://)、FTP协议(ftp://)

5.2平稳退化 65
等，伪协议则是一种非标准化的协议。“javascript:”伪协议让我们通过一个链接来调用JavaScript
祿。
下面是通过“javascript”伪协议调用popUp()函数的具体做法：
<a href=,!javascript:popUp(1 http://www^example^com/1)ju>Example</a>
g	这条语句在支持“javascript”伪协议的浏览器中运行正常，较老的浏览器则会去尝试打开那
接但失败，支持这种伪协议但禁用了 JavaScript功能的浏览器会什么也不做。
总之，在HTML文档里通过“javascript:”伪协议调用JavaScript代码的做法非常不好。
52.2内嵌的事件处理函数
我们已经在第4章的图片库脚本见识过事件处理函数的用途和用法了：把oncllck事件处理 运数作为属性嵌入<a>标签，该处理函数将在oncllck事件发生时调用图片切换函数。
这个技巧同样可以用来调用popup函数。但当在某个链接里用oncllck事件处理函数去打开 夢窗口时，这个链接的href属性似乎没有什么用处——与这个链接有关的重要信息已经都包括 £它的oncllck属性里了。这也正是我们经常会看到如下所示的链接的原因：
<a hre干onclick=MpopUp('httpr/Zwww.example• com/1);
• return false; ,r>Example<a>
因为在上面这条HTML指令里使用了 return false语句，这个链接不会真的被打开。“#”符 是一个仅供文档内部使用的链接记号（单就这条指令而言，“#”是未指向任何目标的内部链



戔;。在某些浏览器里，“#”链接指向当前文档的开头。把h「ef属性的值设置为“#”只是为了
一个空链接。实际工作全部由oncllck属性负责完成。
很遗憾，这个技巧与用“javascript”伪协议调用JavaScript代码的做法同样糟糕，因为它们
蔡不能平稳退化。如果用户已经禁用了浏览器的JavaScript功能，这样的链接将毫无用处。
5«2.3谁关心这个 *
或许你对我反复强调“平稳退化”有些不解：让那些不支持或禁用了 JavaScript功能的浏览
香也能顺利地访问你的网站真的那么重要吗？
请想象一下，有个访问者来到了你的网站，他总是在浏览Web时同时禁用图像和JavaScript。
家肯定认为如今这样的用户已非常少见，而事实也正是如此。但这个访问者非常重要。
你想象的那个用户是一个搜索机器人（searchbot)。搜索机器人是一种自动化的程序，它们
氯览Web的目的是为了把各种网页添加到捜索引擎的数据库里。各大捜索引擎都有类似的程序。
目前，只有极少数搜索机器人能够理解JavaScript代码。所以，如果你的JavaScript网页不能平
稳退化，它们在搜索引擎上的排名就可能大受损害。
具体到popUp()函数，为其中的JavaScript代码预留出退路很简单：在链接里把href属性设
置为真实存在的URL地址，让它成为一个有效的链接，如下所示：
<a href=Hhttp://www^example•com/tr
• onclick=l,popUp(,http://www.exaniple^cornl; return false;,f>Example</a>

66 第5章最佳实践
因为URL地址出现了两次，上面这些代码显得有点冗长，但我们可以利用JavaScript语言把 它改写得简明一些。this可以用来代表任何一种当前元素，所以可以用this和getAttrlbuteO方 法提取出h「ef属性的值，如下所示：
<a href="http://www,examplK；om/’’
• onclick="popUp(this.getAttribute(rhref'); return false;”>Example</a>
老实说，上面这条语句没有精简多少。当前链接的h「ef属性还有一个更简明的引用办法 	使用由DOM提供的tlri s. href属性：
<a href=n http ://www* example •corn/11
^ onclick=npopUp(this.href; return false;f,>Example</a>
不管采用哪种方法，重要的是href属性现在已经有了合法的值。与h「ef= "javascript: •••" 或href ="#"相比，这几种变体的效果要好得多。
所以，在把href属性设置为真实存在的URL地址后，即使JavaScript已被禁用（或遇到了 捜索机)，这个链接也是可用的。虽然这个链接在功能上打了点儿折扣（因为它没有打开一个新 窗口），但它并没有彻底失效。这是一个经典的“平稳退化”的例子。
在本书此前介绍的所有技巧当中，这个技巧是最有用的，但它还有改进的余地。这个技巧 最明显的不足是：每当需要打开新窗口时，就不得不把一些JavaScript代码嵌入标记文档中。如 果能把包括事件处理函数在内的所有JavaScript代码全都放在外部文件里，这个技巧将更加完 善。
5.3向CSS学习
此前，我曾以JavaScript和Flash为例，对技术会因为在诞生初期被人们滥用而造成恶劣后 果的问题进行了讨论。我们可以从过去的失误里学到很多东西。
不过，还有一些技术是从一开始就被人们小心谨慎地使用着的。我们可以从它们那里学到更 多的东西。
5.3.1结构与样式的分离
CSS (层叠样式表）是一项了不起的技术。CSS可以让人们对网站设计工作中的各个方面做 出严格细致的控制。表面上看，CSS技术并无新内容，CSS能做到的用<table^fl<font^标签也 可以做到。CSS技术的最大优点是，它能够帮助你将Web文档的内容结构（标记）和版面设计 (样式）分离开来。
我们经常会遇到一些几乎每个元素都带有style属性的Web文档，而这是CSS技术最缺乏 效率的用法之一。真正能从CSS技术获益的方法，是把样式全部转移到外部文件中去。
与JavaScript和Flash相比，CSS的“出生”日期要晚得多。或许是已经从滥用JavaScript和 Flash的后果中吸取了教训的缘故，网页设计人员一开始使用CSS时就采用了一种深思熟虑、渐 进增强的态度。
把文档的结构和样式分为两部分的CSS技术给每个人都带来了方便。如果你的工作是编写

5.3 向CSS学习 67



的内容，现在只要集中精力把文档的内容正确地标记出来就行了，用不着再与充斥着<able> .^f〇nt>等标签的模板打交道，也就用不着再担心会把文档的版面设计弄得一团糟。如果你的工 修是设计网页的版面，现在只要集中精力把诸如颜色、字体和位置等在一些外部文件里设置妥当 盏行了，而无需再接触文档，最多只需要添加些类或是Id属性。
作为CSS技术的突出优点，文档结构与文档样式的分离可以确保网页都能平稳退化。具备 C5S支持的浏览器固然可以把网页呈现得美仑美奂，不支持或禁用了 CSS功能的浏览器同样可 网页的内容按照正确的结构显示出来。
按这种原则使用JavaScript时，我们可以从CSS身上借鉴到很多东西。
&3.2渐进增强
在网页设计人员当中流传着这样一句格言：“内容就是一切”。如果没有内容，创建网站还有
I用？
话虽如此，也不能简单地把原始内容发布到网上，而不加任何描述。内容需要用HTML或 TML之类的标记语言来描述。在创建网站的时候，给内容加上正确的HTML标记是第一个步 或许也是最重要的步骤。我们可以修正那句格言为“标记良好的内容就是一切”。
只有正确地使用标记语言才能对内容做出准确的描述。各种标记负责提供诸如“这是列表 獲\ “这是文本段落”之类的信息。如果不使用<11>、<P>之类的标签，我们就很难把它们区分
在给内容加上各种标记后，就可以使用各种CSS指令控制内容的显示效果。CSS指令构成 了一个表示层。这个表示层就像是一张透明的彩色薄膜，可以包裹到文档的结构上，使文档的内 容呈现出各种色彩。但即使去掉这个表示层，文档的内容也依然可以访问（只是缺乏色彩而已)。 所谓“渐进增强”就是用一些额外的信息层去包裹原始数据。按照“渐进增强”原则创建出 网页几乎（如果不是“全部”的话）都符合“平稳退化”原则。
类似于CSS，JavaScript和DOM提供的所有功能也应该构成一个额外的指令层。CSS代码负 衰提供关于“表示”的信息，JavaScript代码负责提供关于“行为”的信息。行为层的应用方式
与表不层一样。
要想获得最佳的“表示”效果，就应该把CSS代码从HTML文档里分离出来放在一些外部 文件里。像下面这样把CSS代码混杂在HTML文档里也不是不可以，但这种做法弊大于利：
<p style=Mfont-weight: bold; color: red;"> Be careful!.
</p>	、
更值得推荐的办法是，先把样式信息存入一个外部文件，再在文档的head部分用<11nk>标签 妄调用这个文件：
•warning { font-weight: bold;

68	第5章最佳实践
cl ass属性是样式与文档内容之间的联结纽带：
<p class=,lwarning,t>
Be careful!
</p>
这显然更容易阅读和理解，而且样式信息也更容易修改了。例如，假设你在100个文档里使 用了 warning类来排版各种警告信息，而现在想统一改变那些警告信息的显示效果，比如把它们 的颜色都从红色改为蓝色。那么，如果你已经把它们的表示层和结构分开了，就可以很容易地修 改样式了。
•warning { font-weight: bold; color: blue;
>
如果把这个样式混杂在那i〇〇个文档里，则不得不进行大量的“搜索并替换”操作。
显然，把CSS代码从HTML文档里分离出来可以让CSS工作得最好。这个适用于CSS表示 层的结论同样适用于JavaScript行为层。
5_4 分离 JavaScript
你此前见到的JavaScript代码都已经与HTML文档分得很开了。负责实际完成各项任务的 JavaScript函数都已存入外部文件，问题出现在内嵌的事件处理函数中。
类似于使用style属性，在HTML文档里使用诸如oncllck之类的属性也是一种既没有效率 又容易引发问题的做法。如果我们用一个“挂钩”、，就像CSS机制中的class或Id属性那样，把 JavaScript代码调用行为与HTML文档的结构和内容分离开，网页就会健壮得多。那么，可否用 下面这条语句来表明“当这个链接被点击时，它将调用popUpO函数”的意思呢？
<a href-Mhttp://www•example•com/n class=,,popup,l>Example</a>
我很高兴告诉大家：完全可以这样做。JavaScript语言不要求事件必须在HTML文档里处理， 我们可以在外部JavaScript文件里把一个事件添加到HTML文档中的某个元素上：
element.event = action...
关键是怎样才能把应该获得这个事件的元素确定下来。这个问题可以利用class或Id属性 来解决。
如果想把一个事件添加到某个带有特定Id属性的元素上，用getElementByld就可以解决问题:
getElementByld(id).event = action
如果事情涉及多个元素，我们可以用getElementsByTagName和getAttribute把事件添加到有 着特定属性的一组元素上。
具体步骤如下所示。
把文档里的所有链接全放入一个数组里。
遍历数组。
如果某个链接的cl ass属性等于popup，就表示这个链接在被点击时应该调用popUpO函数。

5.4 分离 JavaScript 69
人把这个链接的href属性值传递给popUp()函数；
B.取消这个链接的默认行为，不让这个链接把访问者带离当前窗口。 面是实现上述步骤的JavaScript代码：
var links = document.getElementsByTagName(Mafl); for (var i=0; i<links*length; i++) { if (links[i].getAttribute(Mclass!f) == npopupH) { links[i]^onclick = function() { popUp(this^getAttribute(,!hrefrt)); return false:
以上代码将把调用popUpO函数的oncli'ck事件添加到有关的链接上。只要把它们存入一个外
JavaScript文件，就等于是把这些操作从HTML文档里分离出来了。而这就是“分离JavaScript”
义。
还有个问题需要解决：如果把这段代码存入外部JavaScript文件，它们将无法正常运行。因
段代码的第一行是：
var links = document^getElementsByTagName(,laM);
这条语句将在JavaScript文件被加载时立刻执行。如果JavaScript文件是从HTML文档的
w分用<sc「1pt>标签调用的，它将在HTML文档之前加载到浏览器里。同样，如果<sc「1pt>
位于文档底部</body>之前，就不能保证哪个文件最先结束加载（浏览器可能一次加载多个)。
运为脚本加载时文档可能不完整，所以模型也不完整。没有完整的DOM, getElementsByTagName
等方法就不能正常工作。
必须让这些代码在HTML文档全部加载到浏览器之后马上开始执行。还好，HTML文档全 奪 加载完毕时将触发一个事件，这个事件有它自己的事件处理函数。
文档将被加载到一个浏览器窗口里，document对象又是window对象的一个属性。当window 诗象触发onload事件时，document对象已经存在。
我将把我的JavaScript代码打包在prepareLInks函数里，并把这个函数添加到window对象的 7]oad事件上去。这样一来，DOM就可以正常工作了：

window.onload = prepareLinks;
function prepareLinks() {
var links = document•getElementsByTagName(tlan);
for (var i=〇; i<links^length; i++) {
if (links[i]^getAttribute(HclassH)
links[i]•onclick = function() {
popUp(this^getAttribute(l,href,1));
return false;

"popup”） {
别忘记把popup函数也保存到那个外部JavaScript文件里去:

70 第5章最佳实践
function popUp(winURL) {
window^open(winURL/,popup,f/lwidth=320,height=480n);
这是一个非常简单的例子，但它演示了怎样才能成功地把行为与结构分离开来。在第6章， 我还会介绍几种可以在文档加载时把事件添到元素上去的巧妙办法。	.
5.5向后兼容
正如前面反复强调的那样，你的网站的访问者很可能未启用JavaScript功能。此外，不同的 浏览器对JavaScript的支持程度也不一样。绝大多数浏览器都能或多或少地支持JavaScript，而绝 大多数现代的浏览器对DOM的支持都非常不错。但比较古老的浏览器却很可能无法理解DOM 提供的方法和属性。因此，即使某位用户在访问你的网站时使用的是支持JavaScript的浏览器， 某些脚本也不一定能正常工作。
5.5.1对象检测
针对这一问题的最简单的解决方案是，检测浏览器对JavaScript的支持程度。这有点儿像游 乐园里的警告牌：“你必须达到这一身高才能参与这项游乐活动”。换句话说，需要在D0M脚本 里表达出下面这个含义：“你必须理解这么多的JavaScript语言才能执行这些语句”。
这个解决方案很容易实现：只要把某个方法打包在一个If语句里，就可以根据这条If语句 的条件表达式的求值结果是true (这个方法存在）还是false (这个方法不存在）来决定应该采 取怎样的行动。这种检测称为对象检测（objectdetecticm)。第2章介绍过，几乎所有的东西（包 括各种方法在内)都可以被当做对象来对待，而这意味着我们可以容易地把不支持某个特定D0M 方法的浏览器检测出来：
if (method) { statements
}
例如，如果有一个使用了 getElementByldO方法的函数，就可以在调用getElementByldO方法 之前先检査用户所使用的浏览器是否支持这个方法。在使用对象检测时，一定要删掉方法名后面 的圆括号，如果不删掉，测试的将是方法的结果，无论方法是否存在。
function myFunction() { if (documentsgetElementByld) { statements using getElementByld
}
>
因此，如果某个浏览器不支持getElementByldO方法，它就永远也不会执行使用此方法的语句。
这个解决方案的唯一不足是，如此编写出来的函数会增加一对花括号。如果需要在函数里检 测多个D0M方法和/或属性是否存在，这个函数中最重要的语句就会被深埋在一层又一层的花括 号里。而这样的代码往往很难阅读和理解。
把测试条件改为“如果你不理解这个方法，请离开”则更简单。
为了把测试条件从“如果你理解……”改为“如果你不理解……”，需要使用“逻辑非”操

5.5 向后兼容	71
?，这个操作符在JavaScript语言里表示为一个惊叹号：
if (!method)
測试条件中的“……请离开”可以用一条「eturn语句来实现。因为这相当于中途退出函数， 址它返回布尔值false比较贴切。用来测试getElementByld是否存在的语句如下所示：
if (IgetElementByld) { return false;
因为花括号部分只有「eturn false —条语句，我们可以把它简写成一行：
if (IgetElementByld) return false;
如果需要测试多个方法或属性是否存在，可以用“逻辑或”操作符将其合并，这个操作符在 pfe%BScript语言里表示为两个竖线符号。如下所示：
if (IgetElementByld || IgetElementsByTagName) return false;
如果这是游乐园里的一块警告牌的话，它的意思是“如果你不理解getElementByld和 ^ElementsByTagName，你就不能参与这项游乐活动”。
现在，我将按照这一思路，在用来把oncllck事件添加到链接上去的网页加载脚本里插入一 条if语句。那个脚本里使用了 getElementsB/TagName，所以需要插入一条If语句去检査浏览器是 否理解这个方法：
window^onload = function() { if (!document•getElementsByTagName) return false; var Inks = document•getElementsByTagName(lfalf); for (var i=〇; i<lnks^length; i++) { if (lnks[i].getAttribute("class") == "popup") { lnks[i]^onclick = function() { popUp(this,getAttribute("href")); return false;
虽然只是一条简单的if语句，但它可以确保那些/古老的”浏览器不会因为我的脚本代码 齑出问题。这么做是为了让脚本有良好的向后兼容性。为我在给网页添加各有关行为时始终遵 循了 “渐进增强”的原则，所以可以确切地知道我添加的那些都能平稳退化，我的网页在那些“古 老的”浏览器里也能正常浏览。那些只支持一部分JavaScript功能但不支持DOM的浏览器仍可 以访问我的网页的内容。
5.5.2浏览器嗅探技术
在JavaScript脚本代码里，在使用某个特定的方法或属性之前，先测试它是否真实存在是确 保向后兼容性最安全和最可信的办法，但它并不是唯一的办法。在浏览器市场群雄逐鹿的那个年 代，一种称为浏览器嗅探（browsersniffimg)的技术曾经非常流行。
“浏览器嗅探”指通过提取浏览器供应商提供的信息来解决向后兼容问题。从理论上讲，可

72	第5章最佳实践
以通过JavaScript代码检索关于浏览器品牌和版本的信息，这些信息可以用来改善JavaScript脚 本代码的向后兼容性，但这是一种风险非常大的技术。
首先，浏览器有时会“撒谎”。因为历史原因，有些浏览器会把自己报告为另外一种浏览器， 还有一些浏览器允许用户任意修改这些信息。
其次，为了适用于多种不同的浏览器，浏览器嗅探脚本会变得越来越复杂。如果想让浏览器 嗅探脚本能够跨平台工作，就必须测试所有可能出现的供应商和版本号组合。这是^个无穷尽的 任务，测试的组合情况越多，代码就越复杂和冗长。
最后，许多浏览器嗅探脚本在进行这类测试时要求浏览器的版本号必须得到精确的匹配。因 此，每当市场上出现新版本时，就不得不修改这些脚本。
令人感到欣慰的是，充满着风险的浏览器嗅探技术正在被更简单也更健壮的对象检测技术所 取代。
5.6性能考虑
很多人都会忽视脚本对Web应用整体性能的影响。为保证应用流畅地运行，在为文档编写 和应用脚本时，需要注意一些问题。
5.6.1尽量少访问DOM和尽量减少标记
访问DOM的方式对脚本性能会产生非常大的影响。以下面代码为例：
i千（doamient.getElementsByTagMame(’ra").length > 0) { var links = document•getElementsByTagName(Hafr); for (var i=0; i<links-length; i++) {
//对每个链接做点处理
搞清楚这段代码要干什么，自然就会明白问题在哪里了。首先，它取得了所有<a>元素，然 后检査它们的个数是不是大于〇:
if (document.getElementsByTagMame(na").length > 0) {
然后，如果大于〇,它会再次取得^有<a>元素，循环遍历这些元素并应用某些操作：
var links = documentsgetElementsByTagName(,*a11); for (var i=0; iclinks•length; i++) {
虽然这段代码可以运行，但它不能保持最优的性能。不管什么时候，只要是查询DOM中的 某些元素，浏览器都会搜索整个DOM树，从中査找可能匹配的元素。这段代码居然使用了两次 getElementsByTagName方法去执行相同的操作，浪费了一次搜索。更好的办法是把第一次捜索的结 果保存在一个变量中，然后在循环里重用该结果，比如：
var links = document•getEleir)entsByTagName(Hatl); if (links.length > 0) {
for (var i=〇; i<links•length; i++) {	'
//对每个链接做点处理

5.6性能考虑 73
这样一来，代码功能没有变，但捜索DO。的次数由两次降低到了一次。
前面例子中的问题还比较容易发现。要是你有多个函数重复做同一件事，恐怕就不太好发现 了。比如，要是有一个函数检査每个链接中的popup类，而另外一个函数检查每个链接中的hover 类，那么同样也会造成捜索浪费。在多个函数都会取得一组类似元素的情况下，可以考虑重构代 码，把搜索结果保存在一个全局变量里，或者把一组元素直接以参数形式传递给函数。
另一个需要注意的地方，就是要尽量减少文档中的标记数量。过多不必要的元素只会增加 DOM树的规模，进而增加遍历DOM树以查找特定元素的时间。
5.6_2合并和放置脚本
本书中的多数示例都使用外部脚本文件，在文档中通S<scr1pt>元素把它们包含进来，如下
<script rc=flscript/function^jsfl></script>
包含脚本的最佳方式就是使用外部文件，因为外部文件与标记能清晰地分离开，而且浏览器 也能对站点中的多个页面重用缓存过的相同脚本。不过，类下面这种情况，最好也不要出现：
〈script src=lfscript/functionA^jslfx/script>
〈script src=Mscript/functionB.jsffx/script>
<script src=l!script/functionC^jsffx/script>
<script src=Mscript/functionD*jsnx/script>
推荐的做法是把 functlonA.js、functlonB.js、functlonC.js 和I functlonD.js 合并到一个脚本 文件中。这样，就可以减少载页面时发送的请求数量。而减少请求数量通常都是在性能优化时 首先要考虑的。
脚本在标记中的位置对页面的初次加载时间也有很大影响。传统上，我们都把脚本放在文档 的<head>区域，这种放置方法有一个问题。位于<head>块中的脚本会导致浏览器无法并行加载其 他文件（如图像或其他脚本)。一般来说，根据HTTP规范，浏览器每次从同一个域名中最多只 能同时下载两个文件。而在下载_本期间，浏览器不会下载其他任何文件，即使是来自不同域名 的文件也不会下载，所有其他资源都要等脚本加载完毕后才能下载。
按照本章前面讨论的渐进增强和分离JavaScript观点，把<scr1pt>标签放到别的地方并不是 问题。把所W<scr1pt>标签都放到文档的末尾，</body^记之前，就可以让页面变得更快。即使 这样，在载脚本时，window对象的load事件依然可以执行对文档进行的各种操作。
5.6.3压缩脚本
在写完了脚本，做了优化，而且也将它放到文档中的适当位置之后，还有一件事可以加快力卩 载速度：压缩脚本文件。
所谓压缩脚本，指的是把脚本文件中不必要的字节，如空格和注释，统统删除，从而达到“压 缩”文件的目的。好在，有很多工具都可以替你来做这件事。有的精简程序甚至会重写你的部分 代码，使用更短的变量名，从而减少整体文件大小。
比如，.假设你有如下代码：

74 第5章最佳实践
function showPic(whichpic) {
//取得图片的href属性
var source = whichpic.getAttribute(nhreftf);
//取得占位符
var placeholder = document.getElementById(llplaceholder,t);
//更新占位符
placeholder. setAttribute(f<srcHJ source);
//使用图像的title属性更新文本描述
var text = whichpic.getAttribute(ntitlen);
var description = document"description");
压缩之后的代码就会变成下面这样：
function showPic(a){var b=a• getAttribute(11 href!|);document.get •ElementById("placeholder").setAttribute("src",G);a.getAttribute ^ (Mtitlen);document•getElementById(11 description1')};
精简后的代码虽然不容易看懂，却能大幅减少文件大小。多数情况下，你应该有两个版本， 、一个是工作副本，可以修改代码并添加注释；另一个是精简副本，用于放在站点上。通常，为了 与非精简版本区分开，最好在精简副本的文件名中加上min字样：
<script src=,,scripts/scriptName^min.js,fx/script>	,
下面是推荐给读者的几个有代表性的代码压缩工具：
□ Douglas Crockford 的 JSMin (

http://www.crockford.com/javascript/jsmirLhtml); a 雅虎的 YUI Compressor (

http://devdoper.yahoo.com/yui/compressor); a	Closure Compiler (

http://closure-compiler.appspot.com/home) 〇
这些工具都有选项，可以在必要时用来最大程度地压缩文件。
5.7小结
本章介绍了一些与DOM脚本编程工作有关的概念和实践，它们是：
口平稳退化 。分离 JavaScript 口向后兼容 口性能考虑
在学习和使用Flash和CSS等其他一些技术时获得的经验可以帮助我们用好JavaScript。只 有勤于思考、善于借鉴，才能编写出高品质的脚本。



