---

layout: post
title: Robust audio-visual scene understanding with hybrid probabilistic & deep learning models
category: Paper阅读
tags: 
  - multi-model perception
  - deep learning

---

<style>
img{
    width: 60%;
    padding-left: 20%;
}
</style>


## 课题摘要

目标: Develop machine learning methodologies for robust automatic perception of multi-person conversational scenes

关注点: how many people,  where they are, what they are saying, to whom, which gestures they perform

模型: hybrid probabilistic/deep learning models

方法: 结合视觉行人检测(body, face, appearance, pose, orientation)和语音信息(speech enhancement, speech and speaker automatic recognition), 结合传统的概率信号处理与深度学习

参考论文: [1], [2] 介绍了背景, [3], [4], [5] 介绍了 multi-person tracking 和 sound separation 中使用generative/Bayesian probabilistic models 的方法, [6] 中介绍了将传统概率模型和深度学习结合中的难点, [7] 介绍了组里的最新研究进展和研究实力



## 论文阅读



#### 1. Analyzing Free-standing Conversational Groups: A Multimodal Approach

2015, ACMMM

HBPE: head and body pose estimation

FCGs: free-standing conversational groups

F-formation:  proper organization of three social spaces: *o*-space, *p*-space and *r*-space,



![][1] 



**主要贡献**:

- 解决了multi-modal HBPE
- 提出了一个灵活的框架,用于处理不同来源的信息以及可穿戴传感器和分布式相机的特征提取
- 将HBPE转化为 matrix completion problem, 
- 将 joint HBPE 转化为两个 incomplete matrices 的 coupling
- 推导了一个用于求解 matrix completion 的优化方法
- 在 SALSA 数据集上进行了大量的实验,证明了HBPE用于 F-formation检测和 social attention attractor发现的可行性



visual descriptors:  $v_{kt}^h \in \mathbb{R}^{d_h}​$, $v_{kt}^b \in \mathbb{R}^{d_b}​$

orientation: $\theta_{kt}^h$, $\theta_{kt}^b$ , 离散化, 分为 C 个 sectors

labeled training set: $\mathcal{L} = \lbrace v_{kt}^h, \theta_{kt}^h, v_{kt}^b, \theta_{kt}^b  \rbrace^{K, T_0}_{k=1, t=1}​$ 

unlabeled features: $\mathcal{U} = \lbrace v_{kt}^h, v_{kt}^b \rbrace^{K, T}_{k=1, t=T_0+1}​$ 



**模型：**

模型为已知视觉描述子和某一段已标记的角度数据，来预测未标注的角度数据，根据以下依据将模型化为非线性凸优化问题：

- 角度是描述子的线性分类器，$\Theta^b = W^b \left\lbrack \begin{matrix}  V^b \\ 1^T  \end{matrix}  \right\rbrack$ ，令 $J_b = \lbrack  \Theta^{bT} V^{bT} 1 \rbrack^T $ ， 问题转化为最小化矩阵秩 $\Theta_{\mathcal{U}}^{b*} = \mathop{\arg\min} rank(J_b)​$
- 实际观测 $\tilde{J}_b$ 带有噪声，加入约束项 $\parallel  P_{\mathcal{O}}^b(\tilde{J}_b - J_b) \parallel_F$ ，其中 $P_{\mathcal{O}}^b$ 是 projection on observation，也就是将 $J$ 中 $\Theta$ 的 unlabeled 部分置零
- 对于角度来说，时域上应该是平滑的
- 头和身体的角度应该大致相同



**优化方法：**















**未来:**

- 启发, HPBE和 multiple peaple tracking 可以相互促进
- 缺点, 应用范围过窄,需要可以追踪特定的人,现有方法需要扩展到长时间学习
- 工程的角度, 现有方案不能够实时化



#### 2. SALSA: A Novel Dataset for Multimodal Group Behavior Analysis

2016, TPAMI

相比于其他数据集, SALSA 拥有 vision, audio, IR, BT 和 Accel,数据更为全面



**未来:**

- 拥挤和动态环境下鲁邦的音频分析
- 在 F-formation detection 中使用蓝牙和 accelerometer
- 设计能够使用多模信息的 tracking 和 HBPE 算法



#### 3. Exploiting the complementarity of audio and visual data in multi-speaker tracking

2017, ICCV

**主要贡献:**

- 提出了一个新的 tracking 框架,使用 visual 和 audio 信息,集成在一个 Kalman Filter 之中





#### 4. Online localization and tracking of multiple moving speakers in reverberant environment

2019, JSTSP

DP-RTF: direct-path relative transfer function

IPDs: interaural phase difference

GMM: Gaussian mixted model

CTF: convolutive transger function

RLS: recursive least squares

LMC: least mean squares

EG: exponentiated gradient



**主要贡献:**

- 使用 recursive least squares 来计算DP-RTF features
- 提出 exponentiated gradient 来追踪声源
- 使用 VEM 算法来进行 tracking
- 最终,实现了一个 online 的多人声学定位追踪框架,对于声音的混杂(reverberation)和噪声(nois)非常鲁棒



**未来:**

- 针对声音断断续续,且正在移动的人声的定位需要进一步研究,需要解决人声识别的问题
- VEM tracker 很容易和 frame-wise 的定位算法结合





#### 5. A variational EM algorithm for the separation of time-varying convolutive audio mixtures

2016, TASLP

VEM: variational expectation-maximization

ASS: audio source separation

LGMs: local Gaussian models

NMF: nonnegative matrix factorization

PSD: positive 

STFT: short-time Fourier transform

HMM: hidden Markov model

DOA: direction of arrival

LDS: linear dynamical system

**主要贡献:**

- 解决了分辨 time-varying convolutive mixture 的声源信号的问题,声源会移动,环境声需要被考虑
- variational EM 算法, Kalman smoother



**未来:**

- 面对实际环境需要 更加鲁棒
- 需要能够识别出有多少个声源
- 研究采集设备的物理变化和 mixing filter 之间的关系





#### 6. Deepgum: Learning deep robust regression with a Gaussian-uniform mixture model

2018, ECCV

GUM: Gaussian-uniform mixture

**主要贡献:**

- 提出了一种解决outliers的





#### 7. A comprehensive analysis of deep regression

2019, TPAMI



## References

[1] X. Alameda-Pineda, Y. Yan, E. Ricci, O. Lanz, and N. Sebe, “Analyzing Free-standing Conversational Groups: A Multimodal Approach,” in ACM International Conference on Multimedia, 2015, pp. 4-15.
[2] X. Alameda-Pineda, J. Staiano, R. Subramanian, L. M. Batrinca, E. Ricci, B. Lepri, O. Lanz, and N. Sebe, “SALSA: A Novel Dataset for Multimodal Group Behavior Analysis,” IEEE Transactions on Pattern Analysis and Machine Intelligence, vol. 38, iss. 8, 2016.
[3] Y. Ban, L. Girin, X. Alameda-Pineda, and R. Horaud, “Exploiting the complementarity of audio and visual data in multi-speaker tracking,” in Proceedings of International Conference on Computer Vision Workshop on Computer Vision for Audio-Visual Media, 2017.
[4] X. Li, Y. Ban, L. Girin, X. Alameda-Pineda, and R. Horaud, “Online localization and tracking of multiple moving speakers in reverberant environment,” IEEE Journal of Selected Topics in Signal Processing, 2019.
[5] D. Kounades-Bastian, L. Girin, X. Alameda-Pineda, S. Gannot, and R. Horaud, “A variational EM algorithm for the separation of time-varying convolutive audio mixtures,” IEEE/ACM Transactiosn on Audio, Speech and Language Processing, vol. 24, no. 8, pp. 1408–1423, 2016.
[6] S. Lathuilière, P. Mesejo, X. Alameda-Pineda, and R. Horaud, “Deepgum: Learning deep robust regression with a Gaussian-uniform mixture model,” in Procedings of European Conference on Computer Vision, 2018.
[7] S. Lathuilière, P. Mesejo, X. Alameda-Pineda, and R. Horaud, “A comprehensive analysis of deep regression,” IEEE Transactions on Pattern Analysis and Machine Intelligence, 2019.





[1]: https://res.cloudinary.com/bxy1994/image/upload/v1555572592/MultiModel_Perception/F-formation_twezlh.png