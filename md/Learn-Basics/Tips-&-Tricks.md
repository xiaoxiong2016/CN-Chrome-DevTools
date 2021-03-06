#小窍门

##控制台

####写跨行命令

处于控制台的多行编辑模式时，你可以像在一个标准文本编辑器中那样进行文本块的处理。在控制台中你可以通过**Shift + Enter**可进入跨行模式。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consolemultiline.png)

当写一段比单行程序复杂得多的JavaScript程序时这非常有用。当你完成一个文本块的输入，在命令行的末尾按回车键即可运行。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consolerun.png)

关于支持持久化的多行控制台，阅读[Snippets](https://developer.chrome.com/devtools/docs/authoring-development-workflow.html#snippets)-一个可以保存和执行客户端JavaScript代码片段的功能(该功能可以在开发者工具中找到)。

####开启元素查看模式的快捷键

**Ctrl + Shift + C**或者**Cmd + Shift + C**将在元素查看模式中打开开发者工具(开发者工具已经打开的情况下将切换到元素查看模式)，以便你可以马上查看当前网页的元素。再次按快捷键将把焦点移到网页上(如果你使用的事Mac，快捷键为Cmd + Shift + C)。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_10.png)

[更多:使用控制台 | 开发者工具文档](https://developer.chrome.com/devtools/docs/console.md)

####支持console.table命令

该命令以表格形式打印任何数据。有几个如何使用它的例子:

    console.table([{a:1, b:2, c:3}, {a:"foo", b:false, c:undefined}]);
    console.table([[1,2,3], [2,3,4]]);

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consoleg1.png)

还有一个可选的“列”参数，该参数为字符串数组的形式。下面，我们定义一个包含多个人的家庭类，然后使用该参数选择展示哪些列。

    function Person(firstName, lastName, age) {
      this.firstName = firstName;
      this.lastName = lastName;
      this.age = age;
    }

    var family = {};
    family.mother = new Person("Susan", "Doyle", 32);
    family.father = new Person("John", "Doyle", 33);
    family.daughter = new Person("Lily", "Doyle", 5);
    family.son = new Person("Mike", "Doyle", 8);

    console.table(family, ["firstName", "lastName", "age"]);

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consoleperson.png)

假如你只想输出前列，使用:

    console.table(family, ["firstName", "lastName"]);

[更多:关于console.table命令 | G+](https://plus.google.com/u/0/115133653231679625609/posts/PmTC5wwJVEc)

####预览在控制台打印出来的对象

在开发者工具中可以直接查看使用console.log()打印出来的对象，不用做额外的工作。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_12.png)

####传入多个参数来格式化控制台输出

正如我们已经用文档说明过的，你可以通过**%c**给你的控制台输出添加样式，就像在firebug中所能做的那样。

    console.log("%cBlue!", "color: blue;");

还支持给多块文本指定不同样式:

    console.log('%cBlue! %cRed!', 'color: blue;', 'color: red;');

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_13.png)

[更多:开发者工具中的样式化的控制台打印 | G+](https://plus.google.com/115133653231679625609/posts/TanDFKEN9Kn)

####清除控制台历史记录的快捷键

控制台打开状态下，你可以使用[快捷键](https://developer.chrome.com/devtools/docs/shortcuts.html)**Ctrl + L**或者**Cmd + L**轻易地清除历史记录。在提示符中使用clear()命令，就像通过控制台API使用[ console.clear()](https://developer.chrome.com/devtools/docs/console.md#clearing-the-console-history)一样。

####成为一个键盘忍者

在开发者工具开启状态下，你可以仅仅通过“?”来打开通用设置，然后你可以找到快捷键面板来通览所有[支持的快捷键](https://developer.chrome.com/devtools/docs/shortcuts.html)。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_14.png)

####在控制台中访问元素

选择一个元素，然后在控制台中输入$0，它就可以被用于写脚本了。如果你在网页中引入了jQuery，你可以使用$($0)来重选网页中该元素。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_15.png)

你也可以通过在任意输出到控制台元素上点击鼠标右键然后选择“Reveal in Elements Panel”来在DOM面板中定位该元素。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_16.png)

####使用XPath表达式查询DOM

xPath是一种查询语言，它被用来从文档中选择节点并返回一个节点集合、字符串、布尔值或数字。你可以在调试工具的JavaScript控制台中使用xPath表达式来查询DOM。

$x(xpath)命令允许你执行查询。看下面使用$x('//img')查询图片元素的例子：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_17.png)

这个函数还接收第二个可选的参数，该参数指定xpath的上下文。$x(xpath, context)。这可以允许我们在一个特定上下文(比如一个iframe)内运行XPath进行元素选择。

    var frame = document.getElementsByTagName('iframe')[0].contentWindow.document.body;
    $x('//'img, frame);

这是一个在特定的上下文中查询图片元素的例子。

####访问最近的控制台结果

使用$_可以帮你快速查看最近一次控制台结果。我们使用另一个xpath示例来演示一下:

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_17a.png)

####使用console.dir

[console.dir(object)](https://developer.chrome.com/devtools/docs/console-api.md#consoledirobject)命令将以可展开的JavaScript对象的形式罗列出给定的对象的所有属性。下面是一个展示可展开的对象的例子，该对象代表document.body所有的属性。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_18.png)

####在特定的iframe中运行JS控制台

开发者工具底部的工具条是随当前标签的上下文变化的下拉选项。当你处于控制台面板时，会有一个下拉选项，该下拉允许你选择控制台将要运行于其中的frame上下文。在下拉中选择你的frame既可以立即切换到你想要的上下文中了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_19.png)

####打开新页面时保留控制台信息

有时你想要在打开新页面时保留你的控制台历史打印信息。在控制台中点击鼠标右键然后选择“Preserve Log upon Navigation(即保留历史信息)”，就可以启用此功能了。当你打开另一个页面时，控制台历史信息将不会被清掉。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_20.png)

####使用*console.time()*和*console.timeEnd()*进行闭环基准测试

[console.time()](https://developer.chrome.com/devtools/docs/console-api.md#consoletimelabel)使用特殊标记开启一个新的计时器。当使用同一标记的[console.timeEnd()](https://developer.chrome.com/devtools/docs/console-api.md#consoletimeendlabel)被调用时，开始时间和结束时间之间的信息将被打印到控制台。这在进行闭环基准测试或没有函数调用的代码段而言尤其有用。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_21.png)

####使用*console.profile()*和*console.profileEnd()*进行性能分析

开发者工具打开状态下，使用[console.profile()](https://developer.chrome.com/devtools/docs/console-api.md#consoleprofilelabel)开始JavaScript CPU性能分析。可以像下面console.profile("Processing")这样为性能分析传一个可选的标记。使用onsole.profileEnd()来结束性能分析。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_22.png)

每一个性能分析都被添加到[性能分析](https://developer.chrome.com/devtools/docs/profiles.html)面板:

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_23.png)

该性能分析也会被添加到console.profiles数组，过后用来查看。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_24.png)

更多关键的使用控制台的小技巧请参阅[使用控制台](https://developer.chrome.com/devtools/docs/console.md)

- 一个通过[控制台API](https://developer.chrome.com/devtools/docs/console-api.md)提供的方法(例如console.log(), console.profile())打印调试信息的地方。
- [命令行API](https://developer.chrome.com/devtools/docs/commandline-api.md)提供的方法，比如用于选取元素的*$()*命令或者用于CPU性能分析的*profile()*。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/preview_console.png)

##时间轴

####使用时间轴帧模式进行帧性能分析

当加载web应用时，时间轴面板告诉你时间花在什么地方。例如，处理DOM事件用了多久，渲染页面布局用了多久，绘制元素到屏幕用了多久等。它允许你从三个不同方面深入探究为什么你的应用会慢: 事件、帧和实际内存占用。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_0.png)

默认状态时间轴不展示任何数据，你可以通过打开你的应用并点击时间轴面板底部的小圆点![](https://developer.chrome.com/devtools/images/recording-off.png)来开始记录。使用*Ctrl + E *或者*Cmd + E*也可以触发记录。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_1.png)

该记录按钮将从灰色变为红色，时间轴开始为你的网页捕获时间轴。在你的应用中完成几个动作然后几秒种后重新点击该按钮来停止记录。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_2.png)

帧模式助你深入了解你的应用中生成单个帧时谷歌浏览器做必须要做的工作。这个模式下，纵条相当于重新计算样式，混合等等。每个纵条的透明部分相当于空闲时间(至少就你的页面而言是空闲的)。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_3.png)

例如，假设你的第一帧的执行花了15毫秒，下一帧的执行花了30毫秒。一般情况是这样：帧之间是同步的帧刷新率，这种情况下第二帧将会花费多于15毫秒的时间来开始渲染。这里,第三帧错过了“真正”的硬件帧和并在下一个帧之前被渲染,因此,第四帧的耗时已经翻了一倍。

如果你的应用中没有很多动画，当浏览器因处理输入事件而必须重复执行一系列动作时，使用帧分析是很有用的。在一帧中当你有足够的时间处理上述事件时，你的应用将更具响应能力也就是更好的用户体验。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_4.png)

当我们的目标帧率是60fps(60帧/秒)时，我们最多可以拥有16.66毫秒去处理任何事。那并不是一段很长的时间，所以尽可能地从动画时间中压榨出更多时间是十分重要的。

[更多:使用开发者工具的时间轴提升性能 | 开发者工具文档](https://developer.chrome.com/devtools/docs/timeline.md)

####使用警示标出强制layout事件

在开发者工具的时间轴面板，如果你在记录视图中看到黄色的三角图标，它指示你你的代码正在触发强制/同步的layout事件。

你想要理想地避免不必要的layout事件被触发，因为它们对你的网页性能有着显著的影响。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_5.png)

[更多:时间轴警示是一种性能信号 | G+](https://plus.google.com/u/0/115133653231679625609/posts/A7rYqkMMmW8)

####分享和分析由别人记录的时间轴

你可以通过导入/导出功能与其他开发者查看和分享时间轴。使用快捷键*Ctrl + E*或者*Cmd + E*来开始和停止记录，然后在时间轴中点鼠标右键保存时间轴数据。在上述右键的菜单中还有一个加载时间轴数据的功能，使用它把曾经导出的时间轴数据导入进来进行查看。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_6.png)

####标注时间轴记录

你可以使用[console.timeStamp()](https://developer.chrome.com/devtools/docs/console.md#marking-the-timeline)来给你的时间轴记录添加标注。这有助于你将你的应用的代码关联到其他正在进行的活动或浏览器事件。在下面的例子中，时间轴被用字符串“Adding result”进行了标注。查看在“使用控制台”中“标记时间轴”的有关内容来获取例子代码。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_7.png)

[更多:开发者工具Console API - 标记时间轴 | 开发者工具](https://developer.chrome.com/devtools/docs/console.md#marking-the-timeline)

####帧率计数器/HUD 展示

A useful tool for visualizing frame rate and jank is the real-time FPS counter

(尚未翻译完，待续……)
