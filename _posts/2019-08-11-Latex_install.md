---

layout: post
title: MacOS/Ubuntu下基于 VS Code 的 LaTex 配置
category: 环境配置
tags: 
  - latex

---

<style>
img{
    width: 60%;
    padding-left: 20%;
}
</style>



## 1. 相关软件安装

**VsCode**

Visual Studio Code (VS Code) 是微软推出的 Editor，免费开源且支持多平台，并且拥有丰富的插件，拿来写C++, Python都很方便，当然也可以用于写LaTex，[下载地址](https://code.visualstudio.com/Download)  



## 2. MacOS

**MacTex**

Latex 可以看成是一种编程语言，那么 MacTex 就是其在 MacOS 环境下的集成运行环境，在终端输入：

```bash
brew cask install mactex
```

**Skim**

Skim是MacOS下一款好用的 PDF 阅读器，在终端输入：

```bash
  brew cask install skim
```



- 在 VS Code 中安装 Latex Workshop 插件
- 推荐编写 `.latexmkrc` 文件，具体命令意义参考 Latexmk General Command Manual

```
  $pdf_mode = 1;
  #$pdflatex = "xelatex -file-line-error --shell-escape -src-specials -synctex=1 -interaction=nonstopmode %O %S;cp %D %R.pdf";
  $pdflatex = "xelatex -synctex=1 -interaction=nonstopmode";
  $recorder = 1;
  $pdf_previewer = "open -a Skim";
  $preview_continuous_mode = 1;
  $pdf_update_method = 0;
  $cleanup_mode = 1;
  $bibtex_use = 2;
  @default_files = ('main.tex');
  
  # $clean_ext = "synctex.gz acn acr alg aux bbl bcf blg brf fdb_latexmk glg glo gls idx ilg ind ist lof log lot out run.xml toc dvi";
  # $out_dir = "temp";
  # 指定生成PDF文件的文件名，可以与LaTeX主文件名不一致
  # $jobname = "Book";
```



然后在命令行输入  `latexmk xxx.tex`  便可以，但貌似这样并不能删除掉中间文件，设置了 clean_ext 也不行，暂时没有找到解决办法，所以可以写一个 python 小脚本来自动删除（vscode 中运行 python 时，需要打开 command palette，输入 `Python: Select Interpreter` 来选着合适的运行环境，mac自带的 Python 是2.7，并不支持 `subprocess.run()`）

```python
#!/usr/bin/env python3
import os
import sys
import subprocess


files = os.listdir('./')
del_suffix = ['aux', 'fdb_latexmk', 'fls', 'log', 'out', 'synctex.gz']
for file in files:
    for suffix in del_suffix:
        if file.endswith(suffix):
            os.remove(file)
```



- 也可以直接使用命令行进行编译：

```bash
latexmk -pvc -xelatex main.tex
```

- 或者配置 Latex Workshop 插件，在 VS Code 中按下 `Command` + `Shift` + `P` , 输入 `Preference: Open Settings(JSON)` ，添加如下内容，每次保存后回自动编译

```json
{
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.recipes": [
        {
          "name": "xelatex",
          "tools": [
            "xelatex"
          ]
        },
        {
          "name": "pdflatex -> bibtex -> pdflatex*2",
          "tools": [
            "pdflatex",
            "bibtex",
            "pdflatex",
            "pdflatex"
          ]
        },
        {
          // 编译参考文献
          "name": "xelatex -> bibtex -> xelatex*2",
          "tools": [
            "xelatex",
            "bibtex",
            "xelatex",
            "xelatex"
          ]
        }
      ],
      "latex-workshop.latex.tools": [
        {
          "name": "xelatex",
          "command": "xelatex",
          "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
          ]
        },
        {
          "name": "latexmk",
          "command": "latexmk",
          "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
          ]
        },
        {
          "name": "pdflatex",
          "command": "pdflatex",
          "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
          ]
        },
        {
          "name": "bibtex",
          "command": "bibtex",
          "args": [
            "%DOCFILE%"
          ]
        }
      ],
}
```



## 3. Ubuntu

- 先安装相应的软件包

```bash
sudo apt-get install texlive-latex-base
sudo apt-get install latex-cjk-all # 中文环境支持
sudo apt-get install texlive-latex-extra
sudo apt-get install texlive-xetex # 为了使用 xelatex
sudo apt-get install texlive-publishers
```

- 同样在 VS Code 中安装 Latex Workshop 插件
- 配置中搜索latex-workshop.latex.recipes，在 settings.json 中加入如下代码：

```json
"latex-workshop.latex.recipes": [
  {
    "name": "xelatex",
    "tools": [
      "xelatex"
    ]
  },
  {
    "name": "xelatex->bibtex->exlatex*2",
    "tools": [
      "xelatex",
      "bibtex",
      "xelatex",
      "xelatex"
    ]
  }],

"latex-workshop.latex.tools":[
  {
    "name":"xelatex",
    "command": "xelatex",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "%DOC%"
    ]
  }, {
    "name":"bibtex",
    "command": "bibtex",
    "args": [
      "%DOCFILE%"
    ]
  }
],
"latex-workshop.view.pdf.viewer": "external",
```

- 新建 `.tex` 文件后，会发现 vs code 的左侧出现了 `LaTex` 的选项，点击其中的按钮便可进行相应的操作





## 参考

[1. macOS 下基于 VS Code 的 LaTeX 环境配置](https://www.jianshu.com/p/c09b3409317f)

[2.[使用 Latexmk 编译 tex 文件](https://macplay.github.io/posts/shi-yong-latexmk-bian-yi-tex-wen-jian/) ](https://macplay.github.io/posts/shi-yong-latexmk-bian-yi-tex-wen-jian/#id8)

[3. Mac下LaTeX环境的搭建](https://fengxc.me/Mac%E4%B8%8BLaTeX%E7%8E%AF%E5%A2%83%E7%9A%84%E6%90%AD%E5%BB%BA.html)

[4. Latexmk General Command Manual](http://personal.psu.edu/jcc8//software/latexmk-jcc/latexmk-465.pdf)

[5.在Ubuntu下使用visual studio code 使用LaTeX,中文支持的配置教程](https://blog.csdn.net/qq_36265860/article/details/82972402)