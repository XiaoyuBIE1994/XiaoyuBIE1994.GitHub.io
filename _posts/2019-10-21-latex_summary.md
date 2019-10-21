---
layout: post
title: LaTex 语法总结
category: 实用工具
tags: latex

---


<style>
img{
    width: 60%;
    padding-left: 20%;
}
</style>



第一次接触 LaTex 是刚来法国的时候，那时候有很多的TP实验要做，而法国实验小伙伴都是用 LaTex 来写报告。刚从国内过来的我对此却一窍不通，抱着不能打酱油的心态，开始了 LaTex 的学习路程，中间陆陆续续看过了许多的入门指南和技巧总结。

总体而言，LaTex 的入门非常简单，只需要一个下午的时间就可以进行基本的写作，但实际的使用中还是会碰到各式各样的问题，网上很容易找到答案，但时间过久了后还是容易忘记，所以决定在这里对所学习的 LaTex 知识进行整理，记录下基本使用方法和各类技巧，以备查询。

> 因为暂时没有中文的写作需求，这里暂时不整理中文和中英文混排的相关内容
>
> 详细的文档可以参考刘海洋老师的《LaTex入门》一书，本文只整理了自己常遇到的困难



## 1.  LaTex 介绍

#### 1.1 编辑器

LaTeX 是基于 TeX 的排版系统，利用 Tex 的控制命令，定义了许多新的控制命令并封装成一个可执行的文件，这个可执行文件会解释 LaTex 新定义的命令成为 Tex 的控制命令，并最后交由引擎进行排版。Tex 的源代码是后缀为 `.tex` 的纯文本文件，使用任意的纯文本编辑器都可以对 `.tex` 文件进行编辑，但实际在写 LaTex 时主要使用以下三种方法：

- online编辑方式，推荐使用 [overleaf](https://www.overleaf.com/) ，优点是不用自己配置环境，可以多人同步协作，缺点是需要有网络连接，且刷新较慢
- 通用文本编辑器+latex插件，例如 [MacOS下基于 VS Code 的 LaTex 配置](http://www.biexiaoyu1994.com/%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/2019/08/11/Mac_Latex/) ，缺点是配置麻烦
- 用于 Tex 的编辑+编译集成软件，如 [Texworks](http://www.tug.org/texworks/)，缺点是太丑，功能单一



#### 1.2 排版工具

Tex 可以有不同的排版工具，例如 pdfTeX, pdfLaTeX, XeTeX, XeLaTeX 等，其中大致的区别如下：

- pdfTeX-pdfLaTeX：pdfTeX可以直接输出 pdf 文件，而不是 Tex 引擎输出的 .dvi 文件，而 pdfLaTeX 添加了对 LaTex 语法的解释

-  XeTeX - XeLaTeX：添加了对 Unicode 字符的支持，也就是可以处理中日韩字符



## 2 LaTex 入门

LaTex 的初衷是让人集中精力于内容的创作，所以基本的语法并不复杂，如下：



```latex
\documentclass{article}
% 这里是导言区
\begin{document}
Hello, world!
\end{document}
```











## 参考

[1] [一份其实很短的 LaTeX 入门文档https://www.kancloud.cn/thinkphp/latex/41811)