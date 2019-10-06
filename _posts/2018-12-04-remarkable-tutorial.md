---
layout: post
title: Remarkable Linux/Windozs双平台Markdown编辑器
category: 环境配置
tags: markdown
---

Mardown是我最喜欢的记笔记语言，没有之一。功能强大而且操作简单，其中猪场推出的云笔记虽然很不错，支持云端储存，但是它使用了KaLex语法，让常年用Latex写报告的我十分的不适应，加上在国外云端的加载速度还是太慢，最后选择了Remarkable这样一款简单实用而且免费的Markdown编辑器，这款软件支持Linux/Windozs双平台操作，而且可以很方便的转换成pdf和html格式，如果只是想写博客，不需要转pdf或者不介意充钱买会员的，也可以考虑[印象笔记 Cmd Markdown](https://www.zybuluo.com/cmd/)

#### 下载地址
> [Remarkable](https://remarkableapp.github.io/index.html)

Ubuntu系统可以下载**.deb**的安装包，然后执行
```linux
$ sudo dpkg -i remarkable_1.87_all.deb
$ sudo apt-get -f install # 安装需要的依赖库
```
1.87是目前的Remarkable的版本号，目前的版本有一个小bug,就是无法输入行间公式，具体的讨论[见这里](https://github.com/jamiemcg/Remarkable/issues/160) 大概意思是源码里面的MathJax的插入有一点问题，解决办法是将	**RemarkableWindow.py** 中第87行的代码修改一下

```python
self.default_html_end = '<script src="http://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.1/highlight.min.js"></script><script>hljs.initHighlightingOnLoad();</script><script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script><script type="text/javascript">MathJax.Hub.Config({"showProcessingMessages" : false,"messageStyle" : "none","tex2jax": { inlineMath: [ [ "$", "$" ] ] }});</script></body></html>' # 源码

self.default_html_end = '<script src="http://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.1/highlight.min.js"></script><script>hljs.initHighlightingOnLoad();</script><script type="text/javascript">window.MathJax = {"showProcessingMessages" : false,"messageStyle" : "none", "tex2jax": {"inlineMath": [ ["$","$"] ]}};</script><script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script></body></html>' # 修改后的代码
```
如果是在Ubuntu下安装的话，这一python文件的路径为：
> /usr/lib/python3/dist-packages/remarkable/RemarkableWindow.py

#### Markdown语法
Markdown语法非常的简单，可以看一下Remarkable的[官方简介](https://github.com/jamiemcg/Remarkable/blob/master/README.md)，或者是下面几篇Tutorial
1. [Markdown 简明语法](http://yangfangs.github.io/2015/11/05/How-to-use-Markdown/)
2. [关于Markdown](http://xianbai.me/learn-md/article/about/readme.html)
3. [常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)
