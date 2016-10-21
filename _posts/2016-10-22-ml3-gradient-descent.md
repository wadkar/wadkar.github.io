---
layout: post
title:  "机器学习（三）梯度下降算法"
image: ''
date:   2016-10-22 00:33:00
tags:
- computer science
- machine learning
- gradient descent
description: '机器学习Coursera学习笔记：第三部分 梯度下降算法'
categories:
- Machine Learning
twitter_text: '机器学习Coursera学习笔记：第三部分 梯度下降算法'
---

## 简述
前面说到了线性回归，我们需要找到代价函数最小的相应参数。这里介绍一种寻找的方法，梯度下降法。

按字面意思理解，就是顺着斜坡一路向下，最终找到最低点。

再具体一点说，就是通过求导求斜率，按照函数梯度以一定的步进不断迭代，最终到达最小值点。

## 迭代公式

$$ \theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1) $$

$$\alpha$$ 为步进，在这里称为学习速率。

### 向量化公式

$$
\theta := \theta - \frac{\alpha}{m} X^{T} (X\theta - \vec{y}) $$

#### 推导过程

$$ \theta := \theta - \alpha \nabla J(\theta) $$

其中

$$
\nabla J(\theta)  = \begin{bmatrix}\frac{\partial J(\theta)}{\partial \theta_0}   \newline \frac{\partial J(\theta)}{\partial \theta_1}   \newline \vdots   \newline \frac{\partial J(\theta)}{\partial \theta_n} \end{bmatrix}
$$

$$
\begin{align*}
\; &\frac{\partial J(\theta)}{\partial \theta_j} &=&  \frac{1}{m} \sum\limits_{i=1}^{m}  \left(h_\theta(x^{(i)}) - y^{(i)} \right) \cdot x_j^{(i)} \newline
\; & &=& \frac{1}{m} \sum\limits_{i=1}^{m}   x_j^{(i)} \cdot \left(h_\theta(x^{(i)}) - y^{(i)}  \right) \newline
\; & &=& \frac1m  \vec{x_j}^{T} (X\theta - \vec{y})
\end{align*}
$$

即

$$
\begin{align*}\; &\frac{\partial J(\theta)}{\partial \theta_j} &=& \frac1m  \vec{x_j}^{T} (X\theta - \vec{y}) \newline\newline\newline\; &\nabla J(\theta) & = & \frac 1m X^{T} (X\theta - \vec{y}) \newline\end{align*}
$$

故向量化公式为

$$
\theta := \theta - \frac{\alpha}{m} X^{T} (X\theta - \vec{y})
$$

## Octave/Matlab 代码实现

```matlab
function theta = gradientDescent(X, y, theta, alpha, num_iters)
	m = length(y);
	for iter = 1:num_iters
		theta = theta - alpha / m * (X' * (X * theta - y));
	end
end
```

## 注意事项

学习速率$$ \alpha $$的选择应适当：   
- 过大则可能每次步进都跨过最小值点，以至于可能随梯度增大而远离最小值点；
- 过小则可能步进极慢，效率低下

为便于向量化表示，$$X$$向量第一列默认为全1。此时相当于$$\theta_0$$与1相乘。
