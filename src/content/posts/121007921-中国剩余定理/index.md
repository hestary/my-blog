---
title: "中国剩余定理"
published: 2021-10-28
description: ""
tags: ["中国剩余定理"]
category: "算法进阶—进阶指南"
draft: false
---

## 

令M=∏i=1nmiM= {\textstyle \prod_{i=1}^{n}}m_iM=∏i=1n​mi​,  ，Mi=MmiM_i=\frac{M}{m_i}Mi​=mi​M​ ,ti∗Mi≡1(mod  mi)t_i*M_i \equiv1(mod \ \ m_i )ti​∗Mi​≡1(mod  mi​)

则

ai∗ti∗Mi≡ai(mod  mi)a_i*t_i*M_i \equiv a_i(mod \ \ m_i )ai​∗ti​∗Mi​≡ai​(mod  mi​)

aj∗tj∗Mj≡0(mod  mi)a_j*t_j*M_j \equiv 0(mod \ \ m_i )aj​∗tj​∗Mj​≡0(mod  mi​)

所以可以构造出答案XXX

X=∏i=1nMitiai{\large {\color{Blue} \mathbf{X= {\textstyle \prod_{i=1}^{n}} M_it_ia_i} } } X=∏i=1n​Mi​ti​ai​

`#include<bits/stdc++.h>
#define I inline
#define int long long
#define RI register int 
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch)){res=(res<<1)+(res<<3)+(ch&15);ch=getchar();}
	return res*f;
}
int n,a,b,w[15];int x,y;
I void exgcd(int a,int b){
	if(!b){x=1;y=0;return;}
	exgcd(b,a%b);
	int k=x;x=y;y=k-a/b*y;
}
int M=1, m[150000];
int X;
signed main()
{
	n=read(); 
	for(RI i=1;i<=n;i++){m[i]=read();w[i]=read();M*=m[i];}
	for(RI i=1;i<=n;i++){
		exgcd(M/m[i],m[i]);
		X+=(x<0 ? x+m[i]:x)*(M/m[i])*w[i];
	}
	printf("%lld",X%M);
	return 0;
}
`