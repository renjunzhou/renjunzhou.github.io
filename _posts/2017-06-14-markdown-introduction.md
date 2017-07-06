---
layout: post
title: Markdown Introduction
---
# Markdown
> 写作与排版同时进行的标记语言

[TOC]

## 标题
```
# 第一级标题 `<h1>`
## 第二级标题 `<h2>`
###### 第六级标题 `<h6>`
```
## 强调
```
*这些文字会生成`<em>`*
_这些文字会生成`<u>`_

**这些文字会生成`<strong>`**
__这些文字会生成`<strong>`__
```
## 换行
```
四个及以上空格加回车
```
## 列表
```
- a
* b
1. c
  1.1 d
```
## 任务列表
- [ ] 任务一 未做任务
- [x] 任务二 已做任务

```
- [ ] 任务一 未做任务 `- + 空格 + [ ]`    

- [x] 任务二 已做任务 `- + 空格 + [x]`
```
## 图片
```
![Alt Text](url)
```
## Link
```
[GitHub](http://github.com)
```
## 区块引用
```
>
```

行内代码
Markdown 语法：

像这样即可：`<addr>` `code`
CMD + K 可插入Markdown语法。
效果如下：

像这样即可：<addr> code

多行或者一段代码
Markdown 语法：

```js
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }

}
```
CMD + Shift + K 可插入Markdown语法。
效果如下：

function fancyAlert(arg) {
    if(arg) {
        $.facebox({div:'#foo'})
    }

}
顺序图或流程图
Markdown 语法：

```sequence
张三->李四: 嘿，小四儿, 写博客了没?
Note right of 李四: 李四愣了一下，说：
李四-->张三: 忙得吐血，哪有时间写。
```

```flow
st=>start: 开始
e=>end: 结束
op=>operation: 我的操作
cond=>condition: 确认？

st->op->cond
cond(yes)->e
cond(no)->op
```
效果如下（ Preferences - Themes - Enable sequence & flow chart 才会看到效果 ）：

张三->李四: 嘿，小四儿, 写博客了没?
Note right of 李四: 李四愣了一下，说：
李四-->张三: 忙得吐血，哪有时间写。
st=>start: 开始
e=>end: 结束
op=>operation: 我的操作
cond=>condition: 确认？

st->op->cond
cond(yes)->e
cond(no)->op
更多请参考：http://bramp.github.io/js-sequence-diagrams/, http://adrai.github.io/flowchart.js/

表格
Markdown 语法：

第一格表头 | 第二格表头
--------- | -------------
内容单元格 第一列第一格 | 内容单元格第二列第一格
内容单元格 第一列第二格 多加文字 | 内容单元格第二列第二格
效果如下：

第一格表头	第二格表头
内容单元格 第一列第一格	内容单元格第二列第一格
内容单元格 第一列第二格 多加文字	内容单元格第二列第二格
删除线
Markdown 语法：

加删除线像这样用： ~~删除这些~~
效果如下：

加删除线像这样用： 删除这些

分隔线
以下三种方式都可以生成分隔线：

***

*****

- - -
效果如下：

MathJax
Markdown 语法：

块级公式：
$$  x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$

\\[ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } } \\]

行内公式： $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$
效果如下（Preferences - Themes - Enable MathJax 才会看到效果）：

块级公式：
\[ x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} \]

\[ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } } \]

行内公式： \(\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N\)

脚注（Footnote）
Markdown 语法：

这是一个脚注：[^sample_footnote]
效果如下：

这是一个脚注：1

注释和阅读更多
Actions->Insert Read More Comment 或者 Command + .
注 阅读更多的功能只用在生成网站或博客时，插入时注意要后空一行。

TOC
Markdown 语法：

[TOC]
效果如下：

Markdown 的设计哲学
本文约定
标题
第一级标题 <h1>
第二级标题 <h2>
第六级标题 <h6>
强调
换行
列表
无序列表
有序列表
任务列表（Task lists）
图片
链接
区块引用
行内代码
多行或者一段代码
顺序图或流程图
表格
删除线
分隔线
MathJax
脚注（Footnote）
注释和阅读更多
TOC
