第一步：
1.为了方便文件管理。单独把parser拆到文件中
2.parser接受html文本作为参数，返回一棵DOM树

第二步：
1.使用主囊太极FSM实现HTML的分析
2.在HTML标准中，已经规定了HTML的状态，我们只是完成一个最简版本。



三种标签：开始标签；结束标签；自封闭标签。


第三步：
1.暂时忽略属性 //。。。
自封闭标签的 '/' 之前可能会跟一个空格，感觉是个疏漏


第四步：
1.在状态机中，除了状态迁移，我们还要加入业务逻辑。
2.在标签结束状态提交标签token。

第五步：
1.属性分为单引号、双引号、无引号三种写法。
2.处理属性对方式和标签类似。
3.属性结束时，我们把属性加到标签Token上。

第六步：
1.使用栈构建DOM树
2.遇到开始标签入栈，遇到结束标签出栈。
3.自封闭节点视为入栈后立刻出栈
4.任何元素的父元素是他入栈前的栈顶。

第七步：
1.文本节点也一样，认为入栈后立刻出栈
2.多个文本节点需要合并


*****************CSS计算*****************
第一步：
1.遇到style标签时，保存CSS规则
2.我们调用cssParser来分析CSS规则。

第二步：
1.创建一个元素后，立即计算CSS
2.理论上当我们分析元素时，所有的css规则已经收集完毕，准备匹配了。
3.真实浏览器中，可能会有写在body的style标签，需要重新计算CSS。

第三步：
1.在computedCSS函数中，我们必须知道元素的父元素才能判断元素与规则是否匹配
2.我们从stack可以获取本元素的所有父元素
3.我们首先获取的是 当前元素， 所有我们获得和计算 父元素的匹配顺序是从内向外，
 （所有不会有父元素选择器）
我们写css的时候要把最能体现独特性的class、id写在最右

第四步：
1.选择器也从当前元素向外排列
2.复杂选择器拆成针对单个元素的选择器，用循环匹配父元素队列

第五步：
1.根据选择器的类型和元素属性，计算是否与当前元素匹配

第六步：
一旦选择器匹配，就应用选择器到元素上

第七步：
优先级比较。
1.css规则根据specificity和后来优先规则覆盖
2.speicificity是个四元组，越左边权重越高
3.一个css规则的specificity根据包含的简单选择器相加而成。