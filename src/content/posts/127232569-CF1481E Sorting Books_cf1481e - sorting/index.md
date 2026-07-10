---
title: "CF1481E Sorting Books_cf1481e - sorting books"
published: 2022-10-09
description: ""
tags: ["算法", "c++", "动态规划"]
category: "比赛"
draft: false
---

## 

你现在要整理书架上的 nnn 本书，每本书有一个颜色 aia_iai​，当每种颜色的书都摆在一起时书架上便整齐了，你每次可以将一本书放到序列最右端，问使书架上整齐的最小操作数。

## 

容易得到，答案最大是nnn次，因为我们可以随意地操作序列nnn次，使序列从小到大就可以了，然后对于答案，我们就只需要求最多可以剩下几个书动，这样子ansansans就是nnn减去不移动的最大值。

我们可以设立状态fif_ifi​表示[i,n][i,n][i,n]最大的不用动数量，因为每次操作可以放到最后面，因此，我们很容易想打这种状态。然后考虑转移发现除了最右边留下来的一种值，每类元素必须要连成一块且完全保留。必须完全保留，也就意味着原本在这种值之间的所有元素都必须右移。于是我们记录每种值最左边的元素、最右边的元素、元素的数量，就可以把每类元素看成一个区间。那么对于不在最右边的值，就是要满足选出权值总和尽可能大的完整区间，这种东西直接把所有区间按右端点排个序就可以 DP 了。

然后对于最右边的值，假设我们已经选出的所有区间最大的右端点为 R，那么我们显然会选取 [R+1,n] 中出现次数最多的元素保留，这直接从后往前扫一遍，开桶维护预处理即可。可以做到 O(n)O(n)O(n)。

fi=max{fi+1if i∈[1,n)cntiif i=l[a[i]];cnti+fr[a[i]]+1if i!=l[a[i]]
f_i = max\begin{cases}f_{i+1}\quad \text {if \textcolor{orange}{i∈[1,n)}}  \\
cnt_i\quad \text{if \textcolor{orange}{i=l[a[i]]};}\\
cnt_i+f_{r[a[i]]+1} \quad\text{if \textcolor{orange}{i!=l[a[i]]}}
\end{cases} 
fi​=max⎩⎨⎧​fi+1​if i∈[1,n)cnti​if i=l[a[i]];cnti​+fr[a[i]]+1​if i!=l[a[i]]​

## 

`#include<bits/stdc++.h>
#define I inline
#define LL long long
#define inf 0x3f3f3f3f
#define LB long double
#define RI register int
#define N 1000100
#define debug puts("debug");
using namespace std;
I int read()
{
	int res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int n,a[N],ans,l[N],r[N],cnt[N],f[N];
int main()
{ 
    memset(l,inf,sizeof l);
	n=read();for(RI x,i=1;i<=n;i++)a[i]=read(),l[a[i]]=min(l[a[i]],i),r[a[i]]=max(r[a[i]],i);
	for(RI i=n;i>=1;i--){
		cnt[a[i]]++;f[i]=f[i+1];
		if(i==l[a[i]])f[i]=max(f[i],f[r[a[i]]+1]+cnt[a[i]]);
		else f[i]=max(f[i],cnt[a[i]]);
	}printf("%d",n-f[1]);return 0;
}
`