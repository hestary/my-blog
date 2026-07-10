---
title: "P3612 [USACO17JAN]Secret Cow Code S_p3612. [usaco17jan] secret cow code s"
published: 2020-10-18
description: ""
tags: ["字符串", "算法"]
category: "分治"
draft: false
---

**

奶牛正在试验秘密代码，并设计了一种方法来创建一个无限长的字符串作为其代码的一部分使用。

给定一个字符串，让后面的字符旋转一次（每一次正确的旋转，最后一个字符都会成为新的第一个字符）。也就是说，给定一个初始字符串，之后的每一步都会增加当前字符串的长度。

给定初始字符串和索引，请帮助奶牛计算无限字符串中位置N的字符。

cow 8

c

简化一下题目，就是求一个字符串，把最后一个字符串接到最前面，然后从第一个字符复制到倒数第二个字符，最后求解第N个字符的问题。

我们先不管题目所说的转换条件，直接顺序复制，拿样例来看**

cow->cowcow

发现第6个字母是第3个字母复制而来所以可以得出 第i个 是 第 i-len/2个字符推出来再按 样例做

COW-COWWCO

这里要从两个类型讨论

1.如果求得字符小于前面推过来的字符的长度，那么就是没有转换，从前面推过来

2.如果所求的字符大于前面推过来的字符的长度，那么转换了，如果它不是最后一个字符，那么它是从（i-1）-（len/2）推过来，比如

len：=6

i=5;

(i-1)-(len/2)=1

第二个C就是从第一个c推过来

如果这个字符是最后一个那么就是从len/2推过来，因为最后一个放到了第一个

两个人就差了一个字符。

`#include<bits/stdc++.h>
using namespace std;
string s;
unsigned long long len,n;
double q;
long long x;
int main()
{
    cin>>s>>n;
    len=s.size();
    for(int i=len;i>=1;i--)s[i]=s[i-1];
    long long i=n;
    long long num=len;
   while(num*2<=n)num*=2;//求出第n个字符再第次转换出来的字符串
   if(num!=n)num*=2;
   while(1)
    { 	
	    if(i<=len)
    	{
    		cout<<s[i];
    		return 0;
		}
    	if(i==num/2+1)i=num/2;//如果刚好是最后一个字符，从前面一个字符串最后一个转换过来
    	else if(i>(num/2))i=(i-1)-(num/2);//如果不是最后一个字符串，分两种情况进行讨论，看看是不是前面的，还是前面的转换过来
		num/=2;
   
	}
	return 0;
}
`