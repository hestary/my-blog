---
title: "O(n)递推求乘法逆元和阶乘逆元_乘法逆元o(n)地推"
published: 2022-07-21
description: ""
tags: ["python", "开发语言"]
category: "算法进阶—进阶指南"
draft: false
---

i−1∗i≡1(modp){\LARGE i^{-1}*i\equiv1 \pmod{p}
} 
i−1∗i≡1(modp)

p=k∗i+r(k=⌊pi⌋)(r=p mod i) 
\LARGE p=k*i+r(k=\left  \lfloor  \frac{p}{i}  \right \rfloor ) (r=p \bmod i)
p=k∗i+r(k=⌊ip​⌋)(r=pmodi)

k∗i+r≡0(modp){\LARGE k*i+r\equiv0 \pmod p } k∗i+r≡0(modp)

k∗r−1+i−1≡0(modp){\LARGE k*r^{-1}+i^{-1}\equiv0 \pmod p } k∗r−1+i−1≡0(modp)

i−1≡−⌊pi⌋∗p mod i(modp){\LARGE i^{-1}\equiv -\left  \lfloor  \frac{p}{i}  \right \rfloor*p \bmod i\pmod p } i−1≡−⌊ip​⌋∗pmodi(modp)

i−1≡(p−p/i)∗inv[p  mod  i](modp){\LARGE i^{-1}\equiv (p-p/i)*inv[p \ \ mod\ \  i]\pmod p } i−1≡(p−p/i)∗inv[p  mod  i](modp)

阶乘逆元

inv[i+1]=1(i+1)!inv[i+1]= \frac{1}{(i+1)!} inv[i+1]=(i+1)!1​

inv[i+1]∗(i+1)=1i!=inv[i]{\LARGE \displaystyle inv[i+1]*(i+1)=\frac{1}{i!}=inv[i]} inv[i+1]∗(i+1)=i!1​=inv[i]