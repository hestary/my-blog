<<<<<<< HEAD
卢卡斯定理 公式 Markdown 版本（适配标准Markdown编辑器，行内公式单$，块级公式双$）
=======
---
title: "math公式"
published: 2026-02-05
description: ""
tags: ["c++", "数学", "算法"]
category: "技术"
draft: false
---
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
1. 核心计算目标（行内公式） 
2. 递归形式（编程常用，块级分段函数）

$$\mathrm{Lucas}(n,m,p) =
=======
卢卡斯定理 公式 Markdown 版本（适配标准Markdown编辑器，行内公式单，块级公式双，块级公式双，块级公式双）


核心计算目标（行内公式）
- 递归形式（编程常用，块级分段函数）


Lucas(n,m,p)={1m=0(n mod pm mod p)⋅Lucas(⌊np⌋,⌊mp⌋,p) mod pm>0\mathrm{Lucas}(n,m,p) =
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650
\begin{cases}
1 & m=0 \\
\dbinom{n \bmod p}{m \bmod p} \cdot \mathrm{Lucas}\left(\left\lfloor \frac{n}{p} \right\rfloor, \left\lfloor \frac{m}{p} \right\rfloor, p\right) \bmod p & m>0
\end{cases}$$

<<<<<<< HEAD
3. 约定（行内公式）
=======

- 约定（行内公式）
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
- 若 $$m > n$$，则 $$\dbinom{n}{m}=0$$

- $$\dbinom{0}{0}=1$$
=======
若 m>nm > nm>n，则 (nm)=0\dbinom{n}{m}=0(mn​)=0
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
4. 进制展开形式（块级公式）

$$\dbinom{n}{m} \equiv \prod_{i}\dbinom{n_i}{m_i} \pmod{p}$$
=======
(00)=1\dbinom{0}{0}=1(00​)=1
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
（其中 $$n=\sum n_ip^i,\ m=\sum m_ip^i$$ 是 $$n,m$$ 的 $$p$$ 进制展开，行内公式：$$n=\sum n_ip^i,\ m=\sum m_ip^i$$）
=======

- 进制展开形式（块级公式）
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
5. 费马小定理（阶乘逆元推导用，行内公式）
=======

(nm)≡∏i(nimi)(modp)\dbinom{n}{m} \equiv \prod_{i}\dbinom{n_i}{m_i} \pmod{p}(mn​)≡i∏​(mi​ni​​)(modp)
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
$$a^{p-2}\equiv a^{-1}\pmod{p}$$
=======

（其中 n=∑nipi, m=∑mipin=\sum n_ip^i,\ m=\sum m_ip^in=∑ni​pi, m=∑mi​pi 是 n,mn,mn,m 的 ppp 进制展开，行内公式：n=∑nipi, m=∑mipin=\sum n_ip^i,\ m=\sum m_ip^in=∑ni​pi, m=∑mi​pi）
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
6. 示例计算相关公式（行内公式）
=======

- 费马小定理（阶乘逆元推导用，行内公式）
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
- 拆分：$$n=10=1\times7+3,\ m=3=0\times7+3$$
=======

ap−2≡a−1(modp)a^{p-2}\equiv a^{-1}\pmod{p}ap−2≡a−1(modp)
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
- 计算：$$\mathrm{Lucas}(10,3,7) = \dbinom{3}{3} \times \mathrm{Lucas}(1,0,7)$$
=======

- 示例计算相关公式（行内公式）
>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650

<<<<<<< HEAD
- 结果：$$1 \times 1 = 1$$

=======
拆分：n=10=1×7+3, m=3=0×7+3n=10=1\times7+3,\ m=3=0\times7+3n=10=1×7+3, m=3=0×7+3

计算：Lucas(10,3,7)=(33)×Lucas(1,0,7)\mathrm{Lucas}(10,3,7) = \dbinom{3}{3} \times \mathrm{Lucas}(1,0,7)Lucas(10,3,7)=(33​)×Lucas(1,0,7)

结果：1×1=11 \times 1 = 11×1=1


>>>>>>> 4ce3a7801c3c0a2582fa73c60d120a29cb813650
需要我帮你把这些公式同步替换到当前canvas文档中，替换原有公式格式吗？
