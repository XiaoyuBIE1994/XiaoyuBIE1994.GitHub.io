---

layout: post
title: Scalable Recognition with a Vocabulary Tree (词袋树模型)
category: Paper阅读
tags: 

  - SLAM

---

<style>
img{
    width: 60%;
    padding-left: 20%;
}
</style>
## 一、简介

词袋模型通常用于SLAM中的回环检测（loop closure）和重定位(relocalisation)，目的是让相机能够有效的检测出经过同一地点这一事件。在SLAM系统中我们用特征点描述子（descriptor）来标注每一张图像。我们可以通过两张图像之间描述子的相似程度和匹配特征点之间的几何约束（比如极线约束）。这篇文章主要讲的的是第一种方法，通常用于几何约束之前，也即是 pre-geometry stage。



## 二、词袋树模型

Descriptor 可以认为是一个多维向量，已有的地图包含大量的图像，每张图像中有包含大量的特征点。为了快速的检索 descriptor 之间的相似度，将地图中所有的图像的所有特征点放在一起，做聚类算法（K-means），每一类认为是一个 vocabulary，为了能够快速检索，这篇文章讲词袋做成树状结构，也就是先对整体做 k-means， 分成k个类，然后对每一个类继续做 k-means, 依次循环，形成词袋树，如下图所示：



![VocabTree][1]



由于分层分类，所以一个描述子可能对应多个节点。就像对于语句分类一样，不同的单词的权重不应该是一样的，所以文中制定了一个基于 entropy 的打分规则：

$$
q_i = n_i w_i \\
d_i = m_i w_i \\
w_i = ln \frac{N}{N_i}
$$

$i$ 代表节点，$q_i, d_i$ 代表当前图像 query 和 database 在节点 $i$ 处的 scoring，$w_i$ 代表权重，$N$ 代表 database 中图像的数量， $N_i$ 代表出现过节点 $i$ 的图像数量，权重的定义基于 TF-IDF 法则（$TF_I = \frac{n_i}{n}$，单幅图像中出现的频率越高权重越大，$IDF_i = ln \frac{N}{N_i}$，拥有特征的图像越多权重越低），但由于 TF 的效果并不明显，所以只取了 IDF 的定义

两幅图像之间的 relevance score 定义如下：  

$$
s(q,d) = \parallel \frac{q}{\parallel q \parallel} - \frac{d}{\parallel d \parallel} \parallel^p
$$

文中指出使用 $L_1-norm$ 效果好于 $L_2-norm$，可以设定一定的阈值将过小的权重直接设置为0，但文中指出大多数情况下并无改善

使用normalized的向量在实际应用中可以进行简化运算：

$$
\begin{align}
\parallel q - d \parallel^p_p & = \sum_i |q_i - d_i|^p \\
& = \sum_{i|d_i=0} |q_i|^p + \sum_{i|q_i=0} |d_i|^p + \sum_{i | q_i \ne 0,d_i \ne 0}|q_i - d_i|^p \\ 
& = \parallel q \parallel^p_p + \parallel d \parallel^p_p + \sum_{i | q_i \ne 0,d_i \ne 0}(|q_i - d_i|^p - |q_i|^p - |d_i|^p) \\
& = 2 + \sum_{i | q_i \ne 0,d_i \ne 0}(|q_i - d_i|^p - |q_i|^p - |d_i|^p) \\
\end{align}
$$










[1]: https://res.cloudinary.com/bxy1994/image/upload/v1551185359/SLAM/vocabulary_tree.png


