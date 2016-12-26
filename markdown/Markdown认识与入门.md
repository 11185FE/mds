---
title: Markdown认识与入门
date: 2016-08-17 18:26:31
tags:
---

by zy

------

>Markdown一些基本语法的介绍

------

### 所谓Markdown

* Markedown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。
* 用于编写说明文档，并且以“README.md”的文件名格式保存在软件的目录下面。
* 拥有RStudio这种神级编辑器，可以将Markdown转化为演讲PPT/Word产品文档。

### 常用语法

常见得Markdown格式选项和键盘快捷键

|输出后的效果    |Markdown                |快捷键      |
|:--------------:|:----------------------:|:----------:|
|Bold            |`**text**`              |ctrl+B      |
|Emphasize       |`*text*`                  |ctrl+i      |
|Strike-thtough  |`~~text~~`                |ctrl+Alt+U  |
|Link            |`[content](url "title")`|ctrl+K      |
|Inline Code     |`code`                  |Ctrl+Shift+K|
|Image           |`![alt](url)`           |Ctrl+Shift+i|
|List            |`* item`                   |Ctrl+L      |
|Blockquote      |`> quote`                 |Ctrl+Q      |
|H1              |# Heading                |            |
|H2              |## Heading               |            |
|H3              |### Heading              |            |
|H4              |#### Heading             |            |
|H5              |##### Heading            |            |
|H6              |###### Heading           |            ||
<p style="text-align:center;">表（1）</p>

### 标题
标题能显示出文章的结构。行首插入1-6个#，几号标题就用几个#表示
```
	H1:# Heading      
	H2:## Heading      
	H3:### Heading     
	H4:#### Heading   
	H5:##### Heading    
	H6:###### Heading 
```

### 文本样式
* 斜体:`*Emphasize*/_Emphasize_`    _Emphasize_
* 加粗:`**Bold**/__Bold__`    __Bold__
* 删除线:`~~delete~~` ~~delete~~
* 段落:段落之前空一行
* 无序列表:添加\*加一个空格成为一个新的列表项
* 有序列表:数字加.加空格
* 引用:\>引用内容
* 水平线：------

### 链接

markdown支持两种形式的链接语法:*行内式和参考式*，这两种形式都是用[方括号]来标记

要建立一个*行内式*的链接，只要在方括号后面紧接着圆括号并插入网址链接即可，如果你还要加上链接的title文字，只要在网址后面，用双引号将title文字包起来即可，例如：

	this is [an example](http://example.com/ "example") inline link.
	[This link](http://example.net/) has no title attribute.

会产生：

	<p>This is <a href="http://example.com/" title="example">an example</a>inline link</p>
	<p><a href="http://example.com/">This link</a>has no title attribute</p>

如果要链接到同样主机上的资源，可以使用相对路径：

	See my [About](/about/) page for details.

*参考式*的链接是链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填写用以标识链接的标记：

	This is [an example][id] reference-style link.

接着，在文章的任意处，可以把这个标记的链接内容定义出来：

	[id]:http://example.com/ "Optional Title Here"

链接内容定义的形式为：
* 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
* 接着一个冒号
* 接着一个以上的空格或制表符
* 链接链接的网址
* 选择性地接着title内容，可以用单引号/双引号或是括弧包着

### 图片

行内式图片语法看起来像是：

	![Alt text](/path/to/img.jpg)
	![Alt text](/path/to/img.jpg "optional title")

详细叙述如下：
* 一个感叹号!
* 接着一个方括号，里面放上图片的替代文字
* 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的title文字。

参考式的图片语法长得像这样：

	![Alt text][id]

### 表格

	|输出后的效果    |Markdown                |快捷键      |
	|:--------------:|:----------------------:|:----------:|
	|Bold            |**text**                |ctrl+B      |
	|Emphasize       |*text*                  |ctrl+i      |
	|Strike-thtough  |~~text~~                |ctrl+Alt+U  |
	|Link            |`[content](url "title")`|ctrl+K      |
	|Inline Code     |`code`                  |Ctrl+Shift+K|
	|Image           |`![alt](url)`           |Ctrl+Shift+i|
	|List            |*item                   |Ctrl+L      |
	|Blockquote      |>quote                  |Ctrl+Q      |
	|H1              |# Heading               |            |
	|H2              |## Heading              |            |
	|H3              |### Heading             |            |
	|H4              |#### Heading            |            |
	|H5              |##### Heading           |            |
	|H6              |###### Heading          |            |


生成的表格如表（1）

### 相关文章

* [Markdown写作浅谈](http://www.yangzhiping.com/tech/r-markdown-knitr.html)
* [Markdown工具补完](http://www.appinn.com/markdown-tools/)
* [Drafts + Scriptogr.am + Dropbox打造移动端Markdown风格博客](http://jianshu.io/p/63HYZ6)