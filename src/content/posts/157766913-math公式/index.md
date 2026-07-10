---
title: "math公式"
published: 2026-02-05
description: ""
tags: ["c++", "数学", "算法"]
category: "技术"
draft: false
---

卢卡斯定理 公式 Markdown 版本（适配标准Markdown编辑器，行内公式单，块级公式双，块级公式双，块级公式双）


核心计算目标（行内公式）
- 递归形式（编程常用，块级分段函数）


Lucas(n,m,p)={1m=0(n mod pm mod p)⋅Lucas(⌊np⌋,⌊mp⌋,p) mod pm>0\mathrm{Lucas}(n,m,p) =
\begin{cases}
1 & m=0 \\
\dbinom{n \bmod p}{m \bmod p} \cdot \mathrm{Lucas}\left(\left\lfloor \frac{n}{p} \right\rfloor, \left\lfloor \frac{m}{p} \right\rfloor, p\right) \bmod p & m>0
\end{cases}Lucas(n,m,p)=⎩⎨⎧​1(mmodpnmodp​)⋅Lucas(⌊pn​⌋,⌊pm​⌋,p)modp​m=0m>0​


- 约定（行内公式）

若 m>nm > nm>n，则 (nm)=0\dbinom{n}{m}=0(mn​)=0

(00)=1\dbinom{0}{0}=1(00​)=1


- 进制展开形式（块级公式）


(nm)≡∏i(nimi)(modp)\dbinom{n}{m} \equiv \prod_{i}\dbinom{n_i}{m_i} \pmod{p}(mn​)≡i∏​(mi​ni​​)(modp)


（其中 n=∑nipi, m=∑mipin=\sum n_ip^i,\ m=\sum m_ip^in=∑ni​pi, m=∑mi​pi 是 n,mn,mn,m 的 ppp 进制展开，行内公式：n=∑nipi, m=∑mipin=\sum n_ip^i,\ m=\sum m_ip^in=∑ni​pi, m=∑mi​pi）


- 费马小定理（阶乘逆元推导用，行内公式）


ap−2≡a−1(modp)a^{p-2}\equiv a^{-1}\pmod{p}ap−2≡a−1(modp)


- 示例计算相关公式（行内公式）

拆分：n=10=1×7+3, m=3=0×7+3n=10=1\times7+3,\ m=3=0\times7+3n=10=1×7+3, m=3=0×7+3

计算：Lucas(10,3,7)=(33)×Lucas(1,0,7)\mathrm{Lucas}(10,3,7) = \dbinom{3}{3} \times \mathrm{Lucas}(1,0,7)Lucas(10,3,7)=(33​)×Lucas(1,0,7)

结果：1×1=11 \times 1 = 11×1=1


需要我帮你把这些公式同步替换到当前canvas文档中，替换原有公式格式吗？