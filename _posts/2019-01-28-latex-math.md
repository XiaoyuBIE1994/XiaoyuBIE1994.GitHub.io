---
layout: post
title: LaTex常用数学符号整理
category: 实用工具
tags: latex
---



在论文和博客的写作中，经常会用到Latex的语法来书写数学公式，一份详细的数学符号对照表必不可少，本文重写了部分[常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)，用以熟悉相关的语法，也以免在这一网站宕机给公式的书写带来不便



## 一、常用公式

|     描述     |                  写法                  |                效果展示                |
| :----------: | :------------------------------------: | :------------------------------------: |
|    上下标    |               a_1 / e_x                |             $a_1$ / $e_x$              |
|    平方根    |               \sqrt\{x\}               |               $\sqrt{x}$               |
| 上下方水平线 |  \overline\{m+n\} / \underline\{m+n\}  |  $\overline{m+n}$ / $\underline{m+n}$  |
| 上下方大括号 | \overbrace\{m+n\} / \underbrace\{m+n\} | $\overbrace{m+n}$ / $\underbrace{m+n}​$ |
|     向量     |                 \vec a                 |                $\vec a$                |
|     分数     |            \frac\{1\}\{2\}             |             $\frac{1}{2}$              |
|     求和     |             \sum_\{i=1\}^n             |         $\sum\limits_{i=1}^n$          |
| 积分 | \int_0^\{\pi/2\} | $\int_0^{\pi/2}​$  |
| 累乘 | \prod_\epsilon | $\prod\limits_\epsilon$ |
| 优化 | \mathop\{\arg\min\}_\{\theta\} | ​$\mathop{\arg\min}\limits_{\theta}$ |



## 二、重音符

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\hat{a}$ | \hat\{a\} | $\check{a}$ | \check\{a\} | $\tilde{a}$ | \tilde\{a\} | $\acute{a}$ | \acute\{a\} |
| $\grave{a}$ | \grave\{a\} | $\dot{a}$ | \dot{a\} | $\ddot{a}$ | \ddot{a\} | $\breve{a}$ | \breve{a\} |
| $\bar{a}$ | \bar{a\} | $\vec{a}$ | \vec{a\} | $\widehat{A}$ | \widehat{A\} | $\widetilde{A}$ | \widetilde{A\} |



## 三、小写希腊字母

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\alpha$ | \alpha | $\theta$ | \theta | $o$ | o | $\upsilon$ | \upsilon |
| $\beta$ | \beta | $\vartheta$ | \vartheta | $\pi$ | \pi | $\phi$ | \phi |
| $\gamma$ | \gamma | $\iota$ | \iota | $\varpi$ | \varpi | $\varphi$ | \varphi |
| $\delta$ | \delta | $\kappa$ | \kappa | $\rho$ | \rho | $\chi$ | \chi |
| $\epsilon$ | \epsilon | $\lambda$ | \lambda | $\varrho$ | \varrho | $\psi$ | \psi |
| $\varepsilon$ | \varepsilon | $\mu$ | \mu | $\sigma$ | \sigma | $\omega$ | \omega |
| $\zeta$ | \zeta | $\nu$ | \nu | $\varsigma$ | \varsigma |  | |
| $\eta$ | \eta | $\xi$ | \xi | $\tau$ | \tau |  | |



## 四、大写希腊字母

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\Gamma$ | \Gamma | $\Lambda$ | \Lambda | $\Sigma$ | \Sigma | $\Psi$ | \Psi |
| $\Delta$ | \Delta | $\Xi$ | \Xi | $\Upsilon$ | \Upsilon | $\Omega$ | \Omega |
| $\Theta$ | \Theta | $\Pi$ | \Pi | $\Phi$ | \Phi |  | |

## 五、二元关系符

可以在下述的命令中加上 \not 来得到

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $<$ | < | $>$ | > | $=$ | = | $\leq$ | \leq or \le |
| $\geq$ | \geq or \ge | $\equiv$ | \equiv | $\ll$ | \ll | $ \gg$ | \gg |
| $\doteq$ | \doteq | $\prec$ | \prec | $\succ$ | \succ | $\sim$ | \sim |
| $\preceq$ | \preceq | $\succeq$ | \succeq | $\simeq$ | \simeq | $\approx$ | \approx |
| $\subset$ | \subset | $\supset$ | \supset | $\subseteq$ | \subseteq | $\supseteq$ | \supseteq |
| $\sqsubset$ | \sqsubset | $\sqsupset$ | \sqsupset | $\sqsubseteq$ | \sqsubseteq | $\sqsupseteq$ | \sqsupseteq |
| $\cong$ | \cong | $\Join$ | \Join | $\bowtie$ | \bowtie | $\propto$ | \propto |
| $\in$ | \in | $\ni$ | \ni or \owns | $\vdash$ | \vdash | $\dashv$ | \dashv |
| $\models$ | \models | $\mid$ | \mid | $\parallel$ | \parallel | $\perp$ | \perp |
| $\smile$ | \smile | $\frown$ | \frown | $\asymp$ | \asymp | $:$ | : |
| $\notin$ | \notin | $\neq$ | \neq or \ne |  | |  | |


## 六、二元运算符

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $+$ | + | $-$ | - | $\times$ | \times | $\div$ | \div |
| $\pm$ | \pm | $\mp$ | \mp | $\triangleleft$ | \triangleleft | $\triangleright$ | \triangleright |
| $\cdot$ | \cdot | $ \setminus$ | \setminus | $\star$ | \star | $\ast$ | \ast |
| $\cup$ | \cup | $\cap$ | \cap | $\sqcup$ | \sqcup | $\sqcap$ | \sqcap |
| $\vee$ | \vee or \lor | $\wedge$ | \wedge or \land | $\circ$ | \circ | $\bullet$ | \bullet |
| $\oplus$ | \oplus | $\ominus$ | \ominus | $\odot$ | \odot | $\oslash$ | \oslash |
| $\otimes$ | \otimes | $\bigcirc$ | \bigcirc | $\diamond$ | \diamond | $\uplus$ | \uplus |
| $\bigtriangleup$ | \bigtriangleup | $\bigtriangledown$ | \bigtriangledown | $\lhd$ | \lhd | $\rhd$ | \rhd |
| $\unlhd$ | \unlhd | $\unrhd$ | \unrhd | $\amalg$ | \amalg | $\wr$ | \wr |
| $\dagger$ | \dagger | $\ddagger$ | \ddagger | | | | |


## 七、大尺度运算符

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\sum$ | \sum | $\bigcup$ | \bigcup | $\bigvee$ | \bigvee | $\bigoplus$ | \bigoplus |
| $\prod$ | \prod | $\bigcap$ | \bigcap | $\bigwedge$ | \bigwedge | $\bigotimes$ | \bigotimes |
| $\coprod$ | \coprod | $\bigsqcup$ | \bigsqcup | | | $\bigodot$ | \bigodot |
| $\int$ | \int | $\oint$ | \oint | | | $\biguplus$ | \biguplus |


## 八、箭头

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $\gets$ | \leftarrow or \gets | $\to$ | \rightarrow or \to | $\longleftarrow$ | \longleftarrow | $\longrightarrow$ | \longrightarrow |
| $\uparrow$ | \uparrow | $\downarrow$ | \downarrow | $\updownarrow$ | \updownarrow | $\leftrightarrow$ | \leftrightarrow |
| $\Uparrow$ | \Uparrow | $\Downarrow$ | \Downarrow | $\Updownarrow$ | \Updownarrow | $\longleftrightarrow$ | \longleftrightarrow |
| $\Leftarrow$ | \Leftarrow | $\Longleftarrow$ | \Longleftarrow | $\Rightarrow$ | \Rightarrow | $\Longrightarrow$ | \Longrightarrow |
| $\Leftrightarrow$ | \Leftrightarrow | $\Longleftrightarrow$ | \Longleftrightarrow | $\mapsto$ | \mapsto | $\longmapsto$ | \longmapsto |
| $\nearrow$ | \nearrow | $\searrow$ | \searrow | $\swarrow$ | \swarrow | $\nwarrow$ | \nwarrow |
| $\hookleftarrow$ | \hookleftarrow | $\hookrightarrow$ | \hookrightarrow | $\rightleftharpoons$ | \rightleftharpoons | $\iff$ | \iff |
| $\leftharpoonup$ | \leftharpoonup | $\rightharpoonup$ | \rightharpoonup | $\leftharpoondown$ | $\leftharpoondown | $\rightharpoondown$ | \rightharpoondown |
| $\leadsto$ | \leadsto | | | | | | |


## 九、定界符

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $($ | ( | $)$ | ) | $\uparrow$ | \uparrow | $\Uparrow$ | \Uparrow |
| $\lbrack$ | \\[ or \lbrack | $\rbrack$ | \\] or \rbrack | $\downarrow$ | \downarrow | $\Downarrow$ | \Downarrow |
| $\lbrace$ | \\{ or \lbrace | $\rbrace$ | \\} or \rbrace | $\updownarrow$ | \updownarrow | $\Updownarrow$ | \Updownarrow |
| $\langle$ | \langle | $\rangle$ | \rangle | $\vert$ | \| or \vert | $\Vert$ | \\| or \Vert |
| $\lfloor$ | \lfloor | $\rfloor$ | \rfloor | $\lceil$ | \lceil | $\rceil$ | \rceil |
| $/$ | / | $\backslash$ | \backslash |  | |  | |
| $\lgroup$ | \lgroup | $\rgroup$ | \rgroup | $\lmoustache$ | \lmoustache | $\rmoustache$ | \rmoustache |
| $\arrowvert$ | \arrowvert | $\Arrowvert$ | \Arrowvert | $\bracevert$ | \bracevert | | |



## 十、其他符号

|      符号      | 写法          | 符号         | 写法       | 符号        | 写法      | 符号         | 写法       |
| :------------: | ------------- | ------------ | ---------- | ----------- | --------- | ------------ | ---------- |
|    $\dots$     | \dots         | $\cdots$     | \cdots     | $\vdots$    | \vdots    | $\ddots$     | \ddots     |
|    $\hbar$     | \hbar         | $\imath$     | \imath     | $\jmath$    | \jmath    | $\ell$       | \ell       |
|     $\Re$      | \Re           | $\Im$        | \Im        | $\aleph$    | \aleph    | $\wp$        | \wp        |
|   $\forall$    | \forall       | $\exists$    | \exists    | $\mho$      | \mho      | $\partial$   | \partial   |
|      $'$       | '             | $\prime$     | \prime     | $\emptyset$ | \emptyset | $\infty$     | \infty     |
|    $\nabla$    | \nabla        | $\triangle$  | \triangle  | $\Box$      | \Box      | $\Diamond$   | \Diamond   |
|     $\bot$     | \bot          | $\top$       | \top       | $\angle$    | \angle    | $\surd$      | \surd      |
| $\diamondsuit$ | \diamondsuit  | $\heartsuit$ | \heartsuit | $\clubsuit$ | \clubsuit | $\spadesuit$ | \spadesuit |
|     $\neg$     | \neg or \lnot | $\flat$      | \flat      | $\natural$  | \natural  | $\sharp$     | \sharp     |



## 十一、非数学符号

| 符号 | 写法 | 符号 | 写法 | 符号 | 写法 |
| :-: | :-: | :-: | :-: | :-: | :-: |
| $\S$ | \S | $P\$ | \P |  |  |



PS: 原文中还有其他符号（如AMS运算符，希伯来字母等），但MathJax中或是不支持，或是使用频率太低，故而在这里不再写入






