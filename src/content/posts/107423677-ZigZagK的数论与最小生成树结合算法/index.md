---
title: "ZigZagK的数论与最小生成树结合算法"
published: 2020-07-18
description: ""
tags: ["c++", "kruskal"]
category: "最小生成树"
draft: false
---

`/*
ZigZagK是个爱思考的孩子。
这天，ZigZaK不想学习，开始思考最小生成树相关问题，他自主思考出了Xor生成树，Or(z)生成树的完美解决方法，
甚至想出了随机生成树的随机做法。他想把数论与最小成树相结合。于是他定义一条连接点 uu 和点 vv 的边的边
权为 gcd(u,v)gcd(u,v)，他想求出这样的定义下的 n 个点的完全图的最大生成树。*/

//用桶排就行了。
//复杂度 O(nlnn)O(nln?n)

#include<bits/stdc++.h>
using namespace std;
long long fa[10000010],ans,n;
long long getfa(int x)
{
	if(fa[x]==x)return x;
	return fa[x]=getfa(fa[x]);
}
int main()
{
	cin>>n;
	for(int i=1;i<=n;i++)fa[i]=i;//krskr，初始化，自己的父亲是自己 
	for(int i=n/2;i>=1;i--)
	for(int j=i*2;j<=n;j+=i)//循环暴力枚举因数 
    if(getfa(i)!=getfa(j))fa[getfa(i)]=getfa(j),ans+=i;//连到因子下面
	// 4 8 不在一个集合 ，8->4 ans+=4; 8连到4下面，价值为4； 
	cout<<ans;
	return 0;
}
`