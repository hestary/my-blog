---
title: "P7961 [NOIP2021] 数列"
published: 2022-11-16
description: ""
tags: ["算法"]
category: "比赛"
draft: false
---


给定整数 n,m,kn, m, kn,m,k，和一个长度为 m+1m + 1m+1 的正整数数组 v0,v1,…,vmv_0, v_1, \ldots, v_mv0​,v1​,…,vm​。

对于一个长度为 nnn，下标从 111 开始且每个元素均不超过 mmm 的非负整数序列 {ai}\{a_i\}{ai​}，我们定义它的权值为 va1×va2×⋯×vanv_{a_1} \times v_{a_2} \times \cdots \times v_{a_n}va1​​×va2​​×⋯×van​​。

当这样的序列 {ai}\{a_i\}{ai​} 满足整数 S=2a1+2a2+⋯+2anS = 2^{a_1} + 2^{a_2} + \cdots + 2^{a_n}S=2a1​+2a2​+⋯+2an​ 的二进制表示中 111 的个数不超过 kkk 时，我们认为 {ai}\{a_i\}{ai​} 是一个合法序列。

计算所有合法序列 {ai}\{a_i\}{ai​} 的权值和对 998244353998244353998244353 取模的结果。


输入第一行是三个整数 n,m,kn, m, kn,m,k。

第二行 m+1m + 1m+1 个整数，分别是 v0,v1,…,vmv_0, v_1, \ldots, v_mv0​,v1​,…,vm​。


仅一行一个整数，表示所有合法序列的权值和对 998244353998244353998244353 取模的结果。


`5 1 1
2 1
`


`40
`


`见附件中的 sequence/sequence2.in
`


`见附件中的 sequence/sequence2.ans
`


**【样例解释 #1】**

由于 k=1k = 1k=1，而且由 n≤S≤n×2mn \leq S \leq n \times 2^mn≤S≤n×2m 知道 5≤S≤105 \leq S \leq 105≤S≤10，合法的 SSS 只有一种可能：S=8S = 8S=8，这要求 aaa 中必须有 222 个 000 和 333 个 111，于是有 (52)=10\binom{5}{2} = 10(25​)=10 种可能的序列，每种序列的贡献都是 v02v13=4v_0^2 v_1^3 = 4v02​v13​=4，权值和为 10×4=4010 \times 4 = 4010×4=40。

**【数据范围】**

对所有测试点保证 1≤k≤n≤301 \leq k \leq n \leq 301≤k≤n≤30，0≤m≤1000 \leq m \leq 1000≤m≤100，1≤vi<9982443531 \leq v_i < 9982443531≤vi​<998244353。

测试点nnnkkkmmm1∼41 \sim 41∼4=8=8=8≤n\leq n≤n=9=9=95∼75 \sim 75∼7=30=30=30≤n\leq n≤n=7=7=78∼108 \sim 108∼10=30=30=30≤n\leq n≤n=12=12=1211∼1311 \sim 1311∼13=30=30=30=1=1=1=100=100=10014∼1514 \sim 1514∼15=5=5=5≤n\leq n≤n=50=50=50161616=15=15=15≤n\leq n≤n=100=100=10017∼1817 \sim 1817∼18=30=30=30≤n\leq n≤n=30=30=3019∼2019 \sim 2019∼20=30=30=30≤n\leq n≤n=100=100=100

表示当前考虑到第i位，已经放了j个数，当前已经有了k个1，并且这一位还存储的1的个数p

考虑从这一个位置开始向下转移，考虑枚举这一个位置该放置1的个数，然后向下转移

f [i+1][j+t][k+(t+p)%2][(t+p)/2]+= f[i][j][k][p]*C[n-j][t]*pow(a[i],t)%mod

考虑答案在什么时候出现，显然就是,f[m+1][n][0~k][p] 并且满足 p向上进位之后加上k还是小于输入的k

`#include<bits/stdc++.h>
#define I inline
#define LL long long
#define inf 0x3f3f3f3f
#define LB long double
#define RI register int
#define N 32
#define debug puts("debug");
#define M 150
#define mod 998244353
#define memeory cout<<abs(&me2-&me1)/1024./1024<<"MB"<<endl;
using namespace std;
I LL read()
{
	LL res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
LL C[M][M],n,m,K,a[M],f[M][N][N][N];
//表示当前考虑到第i位，已经放了j个数，当前已经有了k个1，并且这一位还存储的1的个数p 
//考虑从这一个位置开始向下转移，考虑枚举这一个位置该放置1的个数，然后向下转移
//f [i+1][j+t][k+(t+p)%2][(t+p)/2]+= f[i][j][k][p]*C[n-j][t]*pow(a[i],t)%mod
//考虑答案在什么时候出现，显然就是,f[m+1][n][0~k][p] 并且满足 p向上进位之后加上k还是小于输入的k
I void getC(){
	for(RI i=0;i<=n;i++)C[i][0]=1;
	for(RI i=1;i<=n;i++)
	for(RI j=1;j<=i;j++)
	C[i][j]=(C[i-1][j]+C[i-1][j-1])%mod;
	
} 
I int pop(int x){
	int ans=0;while(x)ans+=(x&1),x>>=1;
	return ans;
}
I LL qpow(LL ds,LL zs){
	LL ans=1;while(zs){
		if(zs&1)ans=(ans*ds)%mod;
		ds=(ds*ds)%mod;zs>>=1;
	}return ans;
}
int main()
{
	n=read();m=read();K=read();getC();
	for(RI i=0;i<=m;i++)a[i]=read();f[0][0][0][0]=1;
	for(RI i=0;i<=m;i++){
		for(RI j=0;j<=n;j++){
			for(RI k=0;k<=K;k++){
				for(RI p=0;p<=n;p++){
					for(RI t=0;t+j<=n;t++){
						f[i+1][j+t][k+(t+p)%2][(t+p)/2]
						+=f[i][j][k][p]*C[n-j][t]%mod*qpow(a[i],t)%mod;
						f[i+1][j+t][k+(t+p)%2][(t+p)/2]%=mod;
					}
				}
			}
		}
	}
	LL num=0;for(RI k=0;k<=K;k++)for(RI p=0;p<=n;p++)if(k+pop(p)<=K)num+=f[m+1][n][k][p],num%=mod;
	printf("%lld\n",num%mod);return 0;
}

`