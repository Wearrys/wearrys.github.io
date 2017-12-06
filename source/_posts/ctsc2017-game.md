---
title: CTSC2017 游戏
date: 2017-08-22 20:21:17
tags:
    - Probability
---

### Description
> 有$N$ 局游戏, 除第一局游戏外每一局游戏的获胜机率均与上一局游戏的结果有关. 现在对游戏进行$Q$次修改, 每次告诉你某一局游戏的结果或者删除之前给你的信息, 求修改后期望下获胜的场数为多少.
$ N, Q \le 2 \times 10 ^ 5 $

<!--more-->

### Solution
首先不难发现, 某一局的游戏的胜率只与其左右的最近游戏结果相关, 所以答案可以分段计算.

考虑期望的线性性, 可以将期望胜利场数表示成每一局游戏的胜率之和.
记 $X _ i$  表示第$i$ 场游戏的状态. 所求即为 $ \sum _ {l < m < r} P( X _ m = 1 | X _ l, X _ r) $. 

由贝叶斯公式:
$$
\begin{align}
P(X _ m = 1 | X _ l, X _ r) &= \frac{P(X _ m = 1, X _ l, X _ r)}{P(X _ l) \cdot P(X _ r | X _ l) } \\
&= \frac{P(X _ l) \cdot P(X _ m = 1 | X _ l) \cdot P(X _ r | X _ l, X _ m = 1)}{P(X _ l) \cdot P(X _ r | X _ l)} \\
&= \frac{P(X _ m=1 | X _ l) \cdot P(X _ r | X _ l, X _ m = 1)}{P(X _ r | X _ l)} \\
&= \frac{P(X _ m=1 | X _ l) \cdot P(X _ r | X _ m = 1)}{P(X _ r | X _ l)} 
\end{align}
$$

发现分母是常数, 于是可以合并分子. 
考虑分子的意义, 大概是合法状态下当前位置为胜的概率.
每一段就可以直接用$dp$来处理出答案, 记录某场比赛为胜/ 负的概率以及分子的期望即可.
这个复杂度是每次询问$O(n)$的.

其实这道题要讲的已经讲完了, 最后只要用矩乘快速合并$dp$值, 维护一下就可以了.