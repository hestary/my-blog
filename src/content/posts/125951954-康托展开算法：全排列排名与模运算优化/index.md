---
title: "康托展开算法：全排列排名与模运算优化"
published: 2022-07-23
description: ""
tags: ["学习", "算法", "c++"]
category: "算法进阶—进阶指南"
draft: false
---


求 1∼N1\sim N1∼N 的一个给定全排列在所有 1∼N1\sim N1∼N 全排列中的排名。结果对 998244353998244353998244353 取模。


第一行一个正整数 NNN。

第二行 NNN 个正整数，表示 1∼N1\sim N1∼N 的一种全排列。


一行一个非负整数，表示答案对 998244353998244353998244353 取模的值。


`3
2 1 3
`


`3
`


`4
1 2 4 3
`


`2
`


对于10%10\%10%数据，1≤N≤101\le N\le 101≤N≤10。

对于50%50\%50%数据，1≤N≤50001\le N\le 50001≤N≤5000。

对于100%100\%100%数据，1≤N≤10000001\le N\le 10000001≤N≤1000000。


考虑每一个位置上对答案的影响。

就拿样例当解释

2 1 3

对于第一个位置只有当1，在第一个位置上面的时候，才会对答案造成影响，而让1到第一个位置上面的时候，后面的数字就可以随便排列了，所有我们可以推出排名的式子了

Ans=∑i=1nsumi∗(n−i)!Ans=\sum_{i=1}^{n} sum_i*(n-i)!Ans=i=1∑n​sumi​∗(n−i)!

sumisum_isumi​表示后缀比aia_iai​小的数有几个，然后这个数提前剩下的数随便排就好了。

我们考虑怎么去维护这个东西，对于阶乘直接O(n)O(n)O(n)预处理出来就好了，对于sumisum_isumi​就可以轻松地打一个值域树状数组来维护，然后就a了

`#include<bits/stdc++.h>
#define I inline
#define LL long long
#define inf 0x3f3f3f3f
#define RI register int
#define N 1000100
#define mod 998244353 
#define debug puts("debug");
using namespace std;
I LL  read()
{
	LL res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
LL ans=0,n,a[N],sum[N],inv[N];
I int lowbit(int x){return x&(-x);}
I int add(int x,int k){for(;x<=N-100;x+=lowbit(x))sum[x]+=k;}
I int ask(int x){int Ans=0;for(;x;x-=lowbit(x))Ans+=sum[x];return Ans;}
I void init(int x){inv[1]=1;for(RI i=2;i<=x;i++)inv[i]=(inv[i-1]*i)%mod;}
int main()
{
	n=read();init(n);for(RI i=1;i<=n;i++)a[i]=read();
	for(RI i=n;i>=1;i--)ans=(ans+ask(a[i])*inv[n-i])%mod,add(a[i],1);
	printf("%lld",ans+1);
	return 0;
}
`