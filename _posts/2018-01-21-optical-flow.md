---
layout: post
title: 光流算法
category: 知识整理
tags: 
  - visual odometry
description: 
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

## 基本原理
光流法实际是通过检测图像像素点的强度随空间和时间的变化进行对物体移动速度和方向的预测的方法，我们有:

$$
I(x,y,t) = I(x+\Delta x, y+\Delta y, t+\Delta t)
$$

假设位移很小，那么可以根据泰勒级数得到：

$$
I(x+\Delta x, y+\Delta y, t+\Delta t) = I(x,y,t)+\frac{\partial I}{\partial x}\Delta x + \frac{\partial I}{\partial y}\Delta y + \frac{\partial I}{\partial t}\Delta t
$$

因此我们可以得到:

$$
\frac{\partial I}{\partial x}\Delta x + \frac{\partial I}{\partial y}\Delta y + \frac{\partial I}{\partial t}\Delta t = 0
$$

$$
\Rightarrow \frac{\partial I}{\partial x}\frac{\Delta x}{\Delta t} + \frac{\partial I}{\partial y}\frac{\Delta y}{\Delta t} + \frac{\partial I}{\partial t}\frac{\Delta t}{\Delta t} = 0
$$

最后可得到:

$$
\frac{\partial I}{\partial x} V_x + \frac{\partial I}{\partial y} V_y + \frac{\partial I}{\partial t} = 0
$$

我们通常表达为:

$$
I_x V_x + I_y V_y = -I_t
$$

或：

$$
\bigtriangledown I^T \cdot \vec{V} = -I_t
$$

## 二、Lucas-Kanade 方法
L-K方法是实际应用中的一种求取光流向量的方法。通过结合几个邻近像素点的信息，L-K方法能够消除光流方程的多义性，而且与逐点计算的方法相比，L-K方法对图像噪声不敏感。 但由于这是一种局部方法，所以在图像的均匀区域内部，此方法无法提供光流信息。

L-K方法假设两个相邻帧的图像内容位移很小，且位移在p点的领域内大致为常数，那么局部图像流(速度)向量\\((V_x,V_y)\\)满足:

$$
\begin{align*}
& I_x(q_1)V_x + I_y(q_1)V_y = -I_t(q_1) \\
& I_x(q_2)V_x + I_y(q_2)V_y = -I_t(q_2) \\
& \qquad \qquad \vdots \\
& I_x(q_n)V_x + I_y(q_n)V_y = -I_t(q_n)
\end{align*}
$$

其中，\\(q_1,q_2,\dots,q_n\\) 是窗口中的像素，\\(I_x(q_i),I_y(q_i),I_t(q_i)\\)是图像在点\\(q_i\\)在当前时间对位置x,y和时间t的偏导。这些等式可以写成\\(Av=b\\),

$$
A = \left[\begin{matrix}
I_x(q_1) & I_y(q_1) \\
I_x(q_2) & I_y(q_2) \\
\vdots & \vdots \\
I_x(q_n) & I_y(q_n) \\
\end{matrix}\right],\quad
v = \left[\begin{matrix}
V_x \\ V_y
\end{matrix}\right],\quad
and \quad b = \left[\begin{matrix}
-I_t(q_1) \\
-I_t(q_2) \\
\vdots \\
-I_t(q_n) \\
\end{matrix}\right]
$$

这一方程组等式个数多余未知数，所以通常它是over-determined，L-K方法就是使用最小平方法，即计算一个2x2的矩阵:

$$
A^TAv = A^Tb \quad 或 \quad v = (A^T A)^{-1}A^Tb
$$

得到:

$$
\left[\begin{matrix}
V_x \\ V_y
\end{matrix}\right] = 
\left[\begin{matrix}
\sum_i I_x(q_i)^2 & \sum_i I_x(q_i)I_y(q_i) \\ 
\sum_i I_y(q_i)I_x(q_i) & \sum_i I_y(q_i)^2
\end{matrix}\right]
\left[\begin{matrix}
-\sum_i I_x(q_i)I_t(q_i) \\ -\sum_i I_y(q_i)I_t(q_i)
\end{matrix}\right]
$$

矩阵\\(A^TA\\)通常被称为图像在点p的结构张量。

