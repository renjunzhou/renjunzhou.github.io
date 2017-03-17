---
layout: post
title: HTML Introduction
---
<h1>Introduction</h1>
<p>什么是 HTML？<br/>
HTML 是用来描述网页的一种语言。<br/>
HTML 指的是超文本标记语言 (Hyper Text Markup Language)<br/>
HTML 不是一种编程语言，而是一种标记语言 (markup language)<br/>
标记语言是一套标记标签 (markup tag)<br/>
HTML 使用标记标签来描述网页<br/>

HTML 文档也被称为网页<br/>
</p>

<h1>Tag</h1>
Tag show as a couple, the first one is called "BeginTag" and second one is "EndTag".<br/>

HTML 标题
HTML 标题（Heading）是通过 &lt;h1&gt; - &lt;h6&gt; 等标签进行定义的。

HTML 段落
HTML 段落是通过 &lt;p&gt; 标签进行定义的。

HTML 链接
HTML 链接是通过 &lt;a&gt; 标签进行定义的。
&lt;a href=&quot;http://www.w3school.com.cn&quot;&gt;This is a link&lt;/a&gt;

HTML 图像
HTML 图像是通过 &lt;img&gt; 标签进行定义的。
实例
&lt;img src=&quot;w3school.jpg&quot; width=&quot;104&quot; height=&quot;142&quot; /&gt;

HTML 属性
HTML 标签可以拥有属性。属性提供了有关 HTML 元素的更多的信息。
属性总是以名称/值对的形式出现，比如：name="value"。
属性总是在 HTML 元素的开始标签中规定。

-&quot;&lt;h1 align=&quot;center&quot;&gt;&quot; 拥有关于对齐方式的附加信息。
-&lt;body bgcolor=&quot;yellow&quot;&gt; 拥有关于背景颜色的附加信息。
-&lt;table border=&quot;1&quot;&gt; 拥有关于表格边框的附加信息。


请确保将 HTML heading 标签只用于标题。不要仅仅是为了产生粗体或大号的文本而使用标题。
搜索引擎使用标题为您的网页的结构和内容编制索引。

&lt;hr /&gt; 标签在 HTML 页面中创建水平线。
&lt;br /&gt; 换行

&lt;table border=&quot;1&quot;&gt;
&lt;tr&gt;
  &lt;th&gt;someheader&lt;/th&gt;
  &lt;th&gt;someheader&lt;/th&gt;
&lt;/tr&gt;
&lt;tr&gt;
  &lt;td&gt;sometext&lt;/td&gt;
  &lt;td&gt;sometext&lt;/td&gt;
&lt;/tr&gt;
&lt;/table&gt;

&lt;h1&gt;速查手册&lt;/h1&gt;

HTML Basic Document
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Document name goes here&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
Visible text goes here
&lt;/body&gt;
&lt;/html&gt;
Text Elements
&lt;p&gt;This is a paragraph&lt;/p&gt;
&lt;br&gt; (line break)
&lt;hr&gt; (horizontal rule)
&lt;pre&gt;This text is preformatted&lt;/pre&gt;
Logical Styles
&lt;em&gt;This text is emphasized&lt;/em&gt;
&lt;strong&gt;This text is strong&lt;/strong&gt;
&lt;code&gt;This is some computer code&lt;/code&gt;
Physical Styles
&lt;b&gt;This text is bold&lt;/b&gt;
&lt;i&gt;This text is italic&lt;/i&gt;
Links, Anchors, and Image Elements
&lt;a href=&quot;http://www.example.com/&quot;&gt;This is a Link&lt;/a&gt;
&lt;a href=&quot;http://www.example.com/&quot;&gt;&lt;img src=&quot;URL&quot;
alt=&quot;Alternate Text&quot;&gt;&lt;/a&gt;
&lt;a href=&quot;mailto:webmaster@example.com&quot;&gt;Send e-mail&lt;/a&gt;A named anchor:
&lt;a name=&quot;tips&quot;&gt;Useful Tips Section&lt;/a&gt;
&lt;a href=&quot;#tips&quot;&gt;Jump to the Useful Tips Section&lt;/a&gt;
Unordered list
&lt;ul&gt;
&lt;li&gt;First item&lt;/li&gt;
&lt;li&gt;Next item&lt;/li&gt;
&lt;/ul&gt;
Ordered list
&lt;ol&gt;
&lt;li&gt;First item&lt;/li&gt;
&lt;li&gt;Next item&lt;/li&gt;
&lt;/ol&gt;
Definition list
&lt;dl&gt;
&lt;dt&gt;First term&lt;/dt&gt;
&lt;dd&gt;Definition&lt;/dd&gt;
&lt;dt&gt;Next term&lt;/dt&gt;
&lt;dd&gt;Definition&lt;/dd&gt;
&lt;/dl&gt;
Tables
&lt;table border=&quot;1&quot;&gt;
&lt;tr&gt;
  &lt;th&gt;someheader&lt;/th&gt;
  &lt;th&gt;someheader&lt;/th&gt;
&lt;/tr&gt;
&lt;tr&gt;
  &lt;td&gt;sometext&lt;/td&gt;
  &lt;td&gt;sometext&lt;/td&gt;
&lt;/tr&gt;
&lt;/table&gt;
Frames
&lt;frameset cols=&quot;25%,75%&quot;&gt;
  &lt;frame src=&quot;page1.htm&quot;&gt;
  &lt;frame src=&quot;page2.htm&quot;&gt;
&lt;/frameset&gt;
Forms
&lt;form action=&quot;http://www.example.com/test.asp&quot; method=&quot;post/get&quot;&gt;
&lt;input type=&quot;text&quot; name=&quot;lastname&quot;
value=&quot;Nixon&quot; size=&quot;30&quot; maxlength=&quot;50&quot;&gt;
&lt;input type=&quot;password&quot;&gt;
&lt;input type=&quot;checkbox&quot; checked=&quot;checked&quot;&gt;
&lt;input type=&quot;radio&quot; checked=&quot;checked&quot;&gt;
&lt;input type=&quot;submit&quot;&gt;
&lt;input type=&quot;reset&quot;&gt;
&lt;input type=&quot;hidden&quot;&gt;
&lt;select&gt;
&lt;option&gt;Apples
&lt;option selected&gt;Bananas
&lt;option&gt;Cherries
&lt;/select&gt;
&lt;textarea name=&quot;Comment&quot; rows=&quot;60&quot;
cols=&quot;20&quot;&gt;&lt;/textarea&gt;
&lt;/form&gt;
Entities
&amp;lt; is the same as &lt;
&amp;gt; is the same as &gt;
&amp;#169; is the same as &copy;
Other Elements
&lt;!-- This is a comment --&gt;
&lt;blockquote&gt;
Text quoted from some source.
&lt;/blockquote&gt;
&lt;address&gt;
Address 1&lt;br&gt;
Address 2&lt;br&gt;
City&lt;br&gt;
&lt;/address&gt;

&lt;h1&gt;标签大全&lt;/h1&gt;
基础
标签	描述
&lt;!DOCTYPE&gt; 	定义文档类型。
&lt;html&gt;	定义 HTML 文档。
&lt;title&gt;	定义文档的标题。
&lt;body&gt;	定义文档的主体。
&lt;h1&gt; to &lt;h6&gt;	定义 HTML 标题。
&lt;p&gt;	定义段落。
&lt;br&gt;	定义简单的折行。
&lt;hr&gt;	定义水平线。
&lt;!--...--&gt;	定义注释。
格式
标签	描述
&lt;acronym&gt;	定义只取首字母的缩写。
&lt;abbr&gt;	定义缩写。
&lt;address&gt;	定义文档作者或拥有者的联系信息。
&lt;b&gt;	定义粗体文本。
&lt;bdi&gt;	定义文本的文本方向，使其脱离其周围文本的方向设置。
&lt;bdo&gt;	定义文字方向。
&lt;big&gt;	定义大号文本。
&lt;blockquote&gt;	定义长的引用。
&lt;center&gt;	不赞成使用。定义居中文本。
&lt;cite&gt;	定义引用(citation)。
&lt;code&gt;	定义计算机代码文本。
&lt;del&gt;	定义被删除文本。
&lt;dfn&gt;	定义定义项目。
&lt;em&gt;	定义强调文本。
&lt;font&gt;	不赞成使用。定义文本的字体、尺寸和颜色
&lt;i&gt;	定义斜体文本。
&lt;ins&gt;	定义被插入文本。
&lt;kbd&gt;	定义键盘文本。
&lt;mark&gt;	定义有记号的文本。
&lt;meter&gt;	定义预定义范围内的度量。
&lt;pre&gt;	定义预格式文本。
&lt;progress&gt;	定义任何类型的任务的进度。
&lt;q&gt;	定义短的引用。
&lt;rp&gt;	定义若浏览器不支持 ruby 元素显示的内容。
&lt;rt&gt;	定义 ruby 注释的解释。
&lt;ruby&gt;	定义 ruby 注释。
&lt;s&gt;	不赞成使用。定义加删除线的文本。
&lt;samp&gt;	定义计算机代码样本。
&lt;small&gt;	定义小号文本。
&lt;strike&gt;	不赞成使用。定义加删除线文本。
&lt;strong&gt;	定义语气更为强烈的强调文本。
&lt;sup&gt;	定义上标文本。
&lt;sub&gt;	定义下标文本。
&lt;time&gt;	定义日期/时间。
&lt;tt&gt;	定义打字机文本。
&lt;u&gt;	不赞成使用。定义下划线文本。
&lt;var&gt;	定义文本的变量部分。
&lt;wbr&gt;	定义可能的换行符。
表单
标签	描述
&lt;form&gt;	定义供用户输入的 HTML 表单。
&lt;input&gt;	定义输入控件。
&lt;textarea&gt;	定义多行的文本输入控件。
&lt;button&gt;	定义按钮。
&lt;select&gt;	定义选择列表（下拉列表）。
&lt;optgroup&gt;	定义选择列表中相关选项的组合。
&lt;option&gt;	定义选择列表中的选项。
&lt;label&gt;	定义 input 元素的标注。
&lt;fieldset&gt;	定义围绕表单中元素的边框。
&lt;legend&gt;	定义 fieldset 元素的标题。
&lt;isindex&gt;	不赞成使用。定义与文档相关的可搜索索引。
&lt;datalist&gt;	定义下拉列表。
&lt;keygen&gt;	定义生成密钥。
&lt;output&gt;	定义输出的一些类型。
框架
标签	描述
&lt;frame&gt;	定义框架集的窗口或框架。
&lt;frameset&gt;	定义框架集。
&lt;noframes&gt;	定义针对不支持框架的用户的替代内容。
&lt;iframe&gt;	定义内联框架。
图像
标签	描述
&lt;img&gt;	定义图像。
&lt;map&gt;	定义图像映射。
&lt;area&gt;	定义图像地图内部的区域。
&lt;canvas&gt;	定义图形。
&lt;figcaption&gt;	定义 figure 元素的标题。
&lt;figure&gt;	定义媒介内容的分组，以及它们的标题。
音频/视频
标签	描述
&lt;audio&gt;	定义声音内容。
&lt;source&gt;	定义媒介源。
&lt;track&gt;	定义用在媒体播放器中的文本轨道。
&lt;video&gt;	定义视频。
链接
标签	描述
&lt;a&gt;	定义锚。
&lt;link&gt;	定义文档与外部资源的关系。
&lt;nav&gt;	定义导航链接。
列表
标签	描述
&lt;ul&gt;	定义无序列表。
&lt;ol&gt;	定义有序列表。
&lt;li&gt;	定义列表的项目。
&lt;dir&gt;	不赞成使用。定义目录列表。
&lt;dl&gt;	定义定义列表。
&lt;dt&gt;	定义定义列表中的项目。
&lt;dd&gt;	定义定义列表中项目的描述。
&lt;menu&gt;	定义命令的菜单/列表。
&lt;menuitem&gt;	定义用户可以从弹出菜单调用的命令/菜单项目。
&lt;command&gt;	定义命令按钮。
表格
标签	描述
&lt;table&gt;	定义表格
&lt;caption&gt;	定义表格标题。
&lt;th&gt;	定义表格中的表头单元格。
&lt;tr&gt;	定义表格中的行。
&lt;td&gt;	定义表格中的单元。
&lt;thead&gt;	定义表格中的表头内容。
&lt;tbody&gt;	定义表格中的主体内容。
&lt;tfoot&gt;	定义表格中的表注内容（脚注）。
&lt;col&gt;	定义表格中一个或多个列的属性值。
&lt;colgroup&gt;	定义表格中供格式化的列组。
样式/节
标签	描述
&lt;style&gt;	定义文档的样式信息。
&lt;div&gt;	定义文档中的节。
&lt;span&gt;	定义文档中的节。
&lt;header&gt;	定义 section 或 page 的页眉。
&lt;footer&gt;	定义 section 或 page 的页脚。
&lt;section&gt;	定义 section。
&lt;article&gt;	定义文章。
&lt;aside&gt;	定义页面内容之外的内容。
&lt;details&gt;	定义元素的细节。
&lt;dialog&gt;	定义对话框或窗口。
&lt;summary&gt;	为 &lt;details&gt; 元素定义可见的标题。
元信息
标签	描述
&lt;head&gt;	定义关于文档的信息。
&lt;meta&gt;	定义关于 HTML 文档的元信息。
&lt;base&gt;	定义页面中所有链接的默认地址或默认目标。
&lt;basefont&gt;	不赞成使用。定义页面中文本的默认字体、颜色或尺寸。
编程
标签	描述
&lt;script&gt;	定义客户端脚本。
&lt;noscript&gt;	定义针对不支持客户端脚本的用户的替代内容。
&lt;applet&gt;	不赞成使用。定义嵌入的 applet。
&lt;embed&gt;	为外部应用程序（非 HTML）定义容器。
&lt;object&gt;	定义嵌入的对象。
&lt;param&gt;	定义对象的参数。
