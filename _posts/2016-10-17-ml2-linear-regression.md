---
layout: post
title:  "机器学习（二）线性回归"
image: ''
date:   2016-10-16 13:13:00
tags:
- machine learning
- linear regression
- introduction
description: '机器学习Coursera学习笔记：第二部分 线性回归'
categories:
- Machine Learning
twitter_text: '机器学习Coursera学习笔记：第二部分 线性回归'
---

线性回归，顾名思义，用一条直线来拟合数据的分布情况。当然，回归是解决连续性问题的。

## 单特征变量

### 回归函数

$$ \hat{y} = h_\theta(x) = \theta_0 + \theta_1 x $$

### 代价函数

假设有m个训练数据样本，则为

$$ J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left ( \hat{y}_{i}- y_{i} \right)^2  = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2 $$

很明显，就是某一自变量情况下，算出回归函数与实际值的距离平方的和，然后取平均值的一半。也就是方差的一半。

之所以要取一半，是为后面求解参数$$\theta$$更加方便（涉及求导，后面的2和这个1/2正好相消）。

## 多特征变量

为了便于表示多特征变量时的各个参数和特征变量，引入以下标记：

$$
\begin{align*}
x_j^{(i)} &= \text{特征 } j \text{ 的值（在 }i^{th}\text{ 个训练数据中）} \newline
x^{(i)}& = \text{一条数据中所有特征的值组成的列向量（在 }i^{th}\text{ 个训练数据中）} \newline
m &= \text{训练数据样本大小（个数）} \newline
n &= \left| x^{(i)} \right| ; \text{(特征数量)} 
\end{align*}
$$

### 回归函数

$$h_\theta (x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \theta_3 x_3 + \cdots + \theta_n x_n$$

矩阵形式为

$$
\begin{align*}
h_\theta(x) =
\begin{bmatrix}
\theta_0 \hspace{2em}  \theta_1 \hspace{2em}  ...  \hspace{2em}  \theta_n
\end{bmatrix}
\begin{bmatrix}
x_0 \newline
x_1 \newline
\vdots \newline
x_n
\end{bmatrix}
= \theta^T x
\end{align*}
$$

### 代价函数

$$ J(\theta) = \dfrac {1}{2m} \displaystyle \sum_{i=1}^m \left (h_\theta (x^{(i)}) - y^{(i)} \right)^2 $$

乍一看和单特征变量的形式几乎一样，但请回顾之前引入的标记，这里的$$x^{(i)}$$是一个列向量，可不只是一个数。

向量化形式为

$$ J(\theta) = \dfrac {1}{2m} (X\theta - \vec{y})^{T} (X\theta - \vec{y}) $$

其中$$\vec{y}是由所有的y值组成的向量。
