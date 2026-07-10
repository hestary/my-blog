---
title: "汉诺塔问题解析"
published: 2022-10-10
description: ""
tags: ["汉诺塔", "震惊", "没有想到"]
category: "dp"
draft: false
---

汉诺塔（Tower of Hanoi），又称河内塔，是一个源于印度古老传说的益智玩具。大梵天创造世界的时候做了三根金刚石柱子，在一根柱子上从下往上按照大小顺序摞着64片黄金圆盘。大梵天命令婆罗门把圆盘从下面开始按大小顺序重新摆放在另一根柱子上。并且规定，在小圆盘上不能放大圆盘，在三根柱子之间一次只能移动一个圆盘

fi=fi−1∗2+1f_i=f_{i-1}*2+1fi​=fi−1​∗2+1

通项公式2n−12^{n}-12n−1


汉诺塔（Tower of Hanoi）是一个数学游戏：有三根柱子，其中一根柱子自底向上串着尺寸渐小的多个圆盘，遵循以下规则：

1、一次只能移动一个圆盘；

2、大圆盘不能放在小圆盘上面。

请问最少需要移动多少步，才能将所有圆盘移到另一根柱子上？

推广： 如果有四根或者更多柱子，所需的最少移动步数又是多少？


设fijf_{ij}fij​表示i个盘子，j个柱子最小步数

考虑现在有N个盘子要移动，可以先设立一个M，对于M盘子先移动到非目标柱子上，然后再把剩下的N-M个盘子移动到目标柱子上面，最后再把剩下的M个盘子移动到目标柱子，故有状态转移方程fi,j=fk,j∗2+fi−k,j−1,k∈[1,n)f_{i,j}=f_{k,j}*2+f_{i-k,j-1},k∈[1,n)fi,j​=fk,j​∗2+fi−k,j−1​,k∈[1,n)

`#include<bits/stdc++.h>
#define I inline
#define LL long long
#define inf 0x3f3f3f3f
#define LB long double
#define RI register int
#define N 50
#define debug puts("debug");
using namespace std;
I LL read()
{
	LL res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int f[N][N],n;
int main()
{
	memset(f,inf,sizeof f);
	n=12;for(RI i=1;i<=4;i++)f[1][i]=1;
	for(RI i=2;i<=n;i++)f[i][3]=f[i-1][3]*2+1;
	
	for(RI i=1;i<=n;i++){
		for(RI k=1;k<i;k++){
			f[i][4]=min(f[i][4],f[k][4]*2+f[i-k][3]);
		}
		cout<<f[i][4]<<endl;
	}
}
`