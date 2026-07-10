---
title: "你有一个环。在环上随机挑选 n 个点，求存在一个大小为 2π/k 的弧能覆盖所有点的概率。"
published: 2022-11-14
description: ""
tags: ["c++", "c语言", "算法"]
category: "比赛"
draft: false
---

你有一个环。在环上随机挑选 n 个点，求存在一个大小为 2π/k 的弧能覆盖所有点的概率。

`#include<bits/stdc++.h>
#define I inline
#define LL long long 
#define RI register int
#define N 1000100
#define mod 998244353
using namespace std;
I LL qpow(LL ds,LL zs){
	LL ans=1;while(zs){
		if(zs&1)ans=(ans*ds)%mod;
		ds=(ds*ds)%mod;zs>>=1;
	}return ans;
}
I LL read()
{
	LL res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
LL n,k;
int main()
{  
   
	n=read();k=read();
	printf("%lld\n",(n*qpow(qpow(k,n-1),mod-2))%mod);return 0;
}
`