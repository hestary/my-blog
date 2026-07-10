---
title: "CF436E Cardboard Box"
published: 2022-10-20
description: ""
tags: ["算法", "贪心算法", "c++"]
category: "比赛"
draft: false
---


对于本题有一个很直接的想法，把花费 yi 看成是花费 xi 得到一个’Y’以后再花费 yi−xi 的金圆券再得到一个’Y’。

如果直接用小根堆 q1 维护最小代价，每次选第一个’Y’后把第二个’Y’插入堆中，得到的答案不一定是最优的。因为假设现在还需 2 个’Y’，贪心的选了 i 的第二个’Y’，再选 j 大一点的第一个’Y’，可能并不比直接选 j 的’YY’的代价小（也就是没有综合考虑选第一个’Y’后再插入的第二个’Y’的代价）。

可以再开一个小根堆 q2 来维护取 ‘YY’ 的代价。每次取出时判断一下是零散地选两个’Y’代价小还是一次性取’YY’代价小。但是需要注意，如果一次性选两个’Y’代价更小，不能直接把两个’Y’都取走，这是因为取了第一个’Y’后，并不保证取第二个’Y’和另一个’Y’的代价就比 q2 此时的最小值更优。只能说这种选法比零散的选法一定更优或者等价，但取出一个后就不一定是最优的了（如果取第二颗星的代价实在太小了，那么也会被再次取出）。

同时由于 q1 和 q2 中维护的是相同元素，于是需要用一个数组记录该星是否被选过，如果当前堆顶的元素已经被使用过了就弹出，直到没有被使用过。

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 1000010
#define LL long long 
#define mod 1000100
using namespace std;
I int read()
{
	int res=0,f=1;char ch=getchar();
	while(!isdigit(ch))ch=getchar();
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
struct node{
	int id;LL val;
	I node make(int x,int y){
		node k;k.id=x;k.val=y;
		return k;
	}
	friend I bool operator <(const node &x,const node &y){
		return x.val>y.val;
	}
};
priority_queue<node>Q1,Q2;
int n,a[N],vis[N];LL ans,m;
int Ans[N];
int main()
{
	n=read();m=read();
	for(RI i=1;i<=n;i++)a[i]=read(),a[i+n]=read(),a[i+n]-=a[i],Q1.push({i,a[i]}),Q2.push({i,a[i+n]+a[i]});
	while(m--){
		while(Q1.size()&&vis[Q1.top().id])Q1.pop();
		while(Q2.size()&&vis[Q2.top().id])Q2.pop();//删除已经做过的点
		int now=Q1.top().id;Q1.pop();
		while(Q1.size()&&vis[Q1.top().id])Q1.pop();
		if(m&&Q2.size()&&Q2.top().val<=a[now]+Q1.top().val){//对于第二种情况的讨论
			Q1.push({now,a[now]});
			now=Q2.top().id;
		}
		
		if(now<=n)Q1.push({n+now,a[n+now]});
		ans+=a[now];vis[now]=1;
	}	
	printf("%lld\n",ans);
	for(RI i=1;i<=n;i++)printf("%d",vis[i]+vis[i+n]);
	return 0;
}

`