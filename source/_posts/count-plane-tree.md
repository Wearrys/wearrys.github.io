---
title: 平面树计数
date: 2017-12-01 11:03:04
tags:
    - Burnside
    - Combinatorial
---

不常见的经典问题, 顺便总结一下Burnside引理吧.

<!-- more -->

### 问题描述

> 给定 $N$, 求 $N$ 个点的本质不同的平面树的数量. 
> 两棵平面树是等价的当且仅当其中一棵能够移动点的位置与另一棵重合, 并且在整个过程中仍然是一棵平面树.

### 做法

首先考虑模型转化(计算 $N+1$ 个点的答案): 
取一个单位圆, 在上面等距的取 $2N$ 个点, 然后将这些点两两配对连边, 满足所有连边不相交.
发现它的对偶图恰好是一棵平面树, 像这样:

![](/img/plane-tree.png)

那么就只需要考虑本质不同的这样的圆的数量即可.
两个圆是等价的当且仅当一个圆可以通过旋转一定的角度与另一个圆重合.
而在这个圆上共有 $2N$ 个点, 就意味着有 $2N$ 个置换, 构成一个置换群.

置换群下的计数可以用到 Burnside引理 :
> $$ N(G, C) = \frac{1}{|G|} { \sum_{f \in G} c(f) } $$

则转化为求置换下的不动点的数量:

- 不存在置换的情况下, 答案为 $c_N$, $\mathrm{Catalan}$ 数的第 $N$ 项.
即将相互匹配的位置看作左右括号, 则所有合法的括号序列都对应一个满足条件的圆.

- $N$ 为奇数时, 可能存在一条平分圆的对角线在置换下不变, 计算 $\frac{N+1}{2}$ 个点的答案即可.

- 考虑旋转置换.
  为了满足旋转之后的边重合, 点 $i$ 和它的匹配点 $p_i$ 在旋转后应该仍然是相匹配的.
  则环的数量一定是偶数 $2d$, 所以环的长度可以表示为 $\frac{2N}{2d} = \frac{N}{d}$.

  假定置换的阶是 $e$, $e > 1, e | N$, 环的数量 $2d = \frac{2N}{e}$.
  环上与 $0$ 匹配的点为 $i$, 不难发现在这些点之间的点的方案数为 $c_{i-1}$.
  当这些点确定之后, 它们在环上依次经过的 $(i+1)e$ 个点就确定了.

  令 $f(x)$ 表示 $\mathrm{Catalan}$ 数的生成函数, 根据 $\mathrm{Catalan}$ 数的递推式, 不难得到:

  $$ f(x) = xf^2(x) + 1 $$

  构造 $b_d$ 表示包含 $2d$ 个环的置换下不动点的数量.

  $$ b_d = 2\sum_{i = 0}^{d-1} c_i b_{d-i-1} $$

  其中因子 $2$ 考虑的是 $i > 2d$ 时用当前置换的逆来计算的情况.
  则 $b_d$ 的生成函数 $g(x)$ 满足:

  $$ g(x) = 2x g(x) f(x) + 1 $$

  解得:

  $$ g(x) = (1 - 4x) ^ {-\frac{1}{2}} $$

### 问题解决

  $$ p(n) = \frac{1}{2n} \( [n \, is \, odd]\binom{n}{\lfloor\frac{n}{2}\rfloor} - \binom{2n}{n-1} + \sum_{d|n}{\varphi(n/d)\binom {2d}{d}} \)$$