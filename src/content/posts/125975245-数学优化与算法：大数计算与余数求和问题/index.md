---
title: "数学优化与算法：大数计算与余数求和问题"
published: 2022-09-11
description: ""
tags: ["学习"]
category: "当前文章被以下社区和专栏收录："
draft: false
---

- 

## 

∑i=1n⌊ni⌋{\Large \sum_{i=1}^n \lfloor\frac{n}{i}\rfloor} i=1∑n​⌊in​⌋

## 

当n≤1e8n\le1e8n≤1e8时，我们显然可以O(n)O(n)O(n)暴力算答案

但是当n≤1e18n\le1e18n≤1e18时，我们肯定会超时，如何优化时间

![]\(https://i-blog.csdnimg.cn/blog_migrate/90bfa372474b955ee68048a38e59325f.png)

我们通过打表可以发现一些性质，当i不断在变大的过程中，出现的答案回变成一个块，然而在这个块里，答案都是一样的，因此我们就可以一起算,通过观察和证明可以得出以下公式，为每个块的右边界![]\(https://i-blog.csdnimg.cn/blog_migrate/c973b246909a621482d5a77cbca0ebb7.png)

### 

#### 

给出正整数 nnn 和 kkk，请计算

G(n,k)=∑i=1nk mod iG(n, k) = \sum_{i = 1}^n k \bmod iG(n,k)=i=1∑n​kmodi

其中 k mod ik\bmod ikmodi 表示 kkk 除以 iii 的余数。

#### 

输入只有一行两个整数，分别表示 nnn 和 kkk。

#### 

输出一行一个整数表示答案。

#### 

##### 

`10 5
`

##### 

`29
`

#### 

###### 

G(10,5)=0+1+2+1+0+5+5+5+5+5=29G(10, 5)=0+1+2+1+0+5+5+5+5+5=29G(10,5)=0+1+2+1+0+5+5+5+5+5=29。

###### 

对于 30%30\%30% 的数据，保证 n,k≤103n , k \leq 10^3n,k≤103。
- 对于 60%60\%60% 的数据，保证 n,k≤106n, k \leq 10^6n,k≤106。
- 对于 100%100\%100% 的数据，保证 1≤n,k≤1091 \leq n, k \leq 10^91≤n,k≤109。

### 

![]\(https://i-blog.csdnimg.cn/blog_migrate/bcf6d50e578508aa6fc1905a35b83620.png)