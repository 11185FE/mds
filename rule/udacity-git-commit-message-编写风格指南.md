# Udacity Git Commit Message 编写风格指南
date: 2016-07-11 10:17:18
tags: rule

By gxh

---------

> Git Commit 编写规范

--------

本文参考自 [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)

## 介绍
*Udacity Git Commit Message Style Guide* 是由 *Udacity* 官方为统一学员编写风格而推出的一款 *Style Guide*，因项目组将使用该编写风格，故在此记录下对原文的学习。

## Commit Messages
### 文本结构
一个 *commit message* 由三个不同的部分组成：*标题（title*、*详细描述（body）* 以及 *结尾（footer）* 组成，它的布局如下：

```
type: subject

body

footer
```

*标题（title）* 包括了 *类型（type）* 及 *主题（subject）*。

### 类型（type）
*类型（type）* 包含在 *标题（title）* 内，可以是一下的任意一个：
* **feat**: 项目代码修改
* **fix**: bug修复
* **docs**: 文档修改
* **style**: 代码格式更改; no code change
* **refactor**: production code重构
* **test**: 添加或重构测试代码; no production code change
* **chore**: 更新脚手架、环境配置等; no production code change

### 主题（subject）
*主题（subject）* 应控制在50个字符之内，以大写字母开头，且不能以句点结尾。

### 详细描述（body)
可选，用来解释此次更改的 *内容(what)* 及 *原因(why)*，不需要解释其实现(how)，在编写时需要注意控制每行的字符长度应该72个之内

### 结尾（footer）
可选，用来引用 *issue tracker* ID

### 示例
```
feat: Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```
