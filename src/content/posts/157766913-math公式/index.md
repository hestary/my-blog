---
title: "math公式"
published: 2026-02-05
description: ""
tags: ["c++", "数学", "算法"]
category: "技术"
draft: false
---

卢卡斯定理 公式 Markdown 版本（适配标准Markdown编辑器，行内公式单$，块级公式双$）

1. 核心计算目标（行内公式） 
2. 递归形式（编程常用，块级分段函数）

$$\mathrm{Lucas}(n,m,p) =
\begin{cases}
1 & m=0 \\
\dbinom{n \bmod p}{m \bmod p} \cdot \mathrm{Lucas}\left(\left\lfloor \frac{n}{p} \right\rfloor, \left\lfloor \frac{m}{p} \right\rfloor, p\right) \bmod p & m>0
\end{cases}$$

3. 约定（行内公式）

- 若 $$m > n$$，则 $$\dbinom{n}{m}=0$$

- $$\dbinom{0}{0}=1$$

4. 进制展开形式（块级公式）

$$\dbinom{n}{m} \equiv \prod_{i}\dbinom{n_i}{m_i} \pmod{p}$$

（其中 $$n=\sum n_ip^i,\ m=\sum m_ip^i$$ 是 $$n,m$$ 的 $$p$$ 进制展开，行内公式：$$n=\sum n_ip^i,\ m=\sum m_ip^i$$）

5. 费马小定理（阶乘逆元推导用，行内公式）

$$a^{p-2}\equiv a^{-1}\pmod{p}$$

6. 示例计算相关公式（行内公式）

- 拆分：$$n=10=1\times7+3,\ m=3=0\times7+3$$

- 计算：$$\mathrm{Lucas}(10,3,7) = \dbinom{3}{3} \times \mathrm{Lucas}(1,0,7)$$

- 结果：$$1 \times 1 = 1$$ 
