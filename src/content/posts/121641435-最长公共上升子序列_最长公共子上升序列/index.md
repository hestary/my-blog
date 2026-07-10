---
title: "最长公共上升子序列_最长公共子上升序列"
published: 2021-11-30
description: ""
tags: ["c++", "线性代数", "矩阵"]
category: "dp"
draft: false
---

算法

(DP,线性DP,前缀和) O(n2)O(n2)

这道题目是AcWing 895. 最长上升子序列和AcWing 897. 最长公共子序列的结合版，在状态表示和状态计算上都是融合了这两道题目的方法。

状态表示：

f[i][j]代表所有a[1 ~ i]和b[1 ~ j]中以b[j]结尾的公共上升子序列的集合；

f[i][j]的值等于该集合的子序列中长度的最大值；

状态计算（对应集合划分）：

首先依据公共子序列中是否包含a[i]a[i]a[i]，将f[i][j]f[i][j]f[i][j]所代表的集合划分成两个不重不漏的子集：

不包含a[i]的子集，最大值是f[i−1][j]a[i]的子集，最大值是f[i - 1][j]a[i]的子集，最大值是f[i−1][j]；

包含a[i]的子集，将这个子集继续划分，依据是子序列的倒数第二个元素在b[]中是哪个数：

子序列只包含b[j]一个数，长度是1；

子序列的倒数第二个数是b[1]的集合，最大长度是f[i−1][1]+1b[1]的集合，最大长度是f[i - 1][1] + 1b[1]的集合，最大长度是f[i−1][1]+1；

…

子序列的倒数第二个数是b[j−1]的集合，最大长度是f[i−1][j−1]+1b[j - 1]的集合，最大长度是f[i - 1][j - 1] + 1b[j−1]的集合，最大长度是f[i−1][j−1]+1；

如果直接按上述思路实现，需要三重循环

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 5500
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch))if(ch=='-')f=-f,ch=getchar();else ch=getchar();
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int f[N][N],n,a[N],b[N],num[N][N];
int main()
{
	n=read();for(RI i=1;i<=n;i++)a[i]=read();
	for(RI i=1;i<=n;i++)b[i]=read();
	for(RI i=1;i<=n;i++)
	{
		for(RI j=1;j<=n;j++)
		{
	      f[i][j]=f[i-1][j];
	      if(a[i]==b[j])
		  {
	      	int Max=1;for(RI k=1;k<j;k++)
			if(a[i]>b[k])Max=max(Max,f[i-1][k]+1);
			f[i][j]=max(f[i][j],Max);
		  }
		}
	}
    int res = 0;
    for (int i = 1; i <= n; i ++ ) res = max(res, f[n][i]);
    printf("%d\n", res);
	return 0;
}

`
然后我们发现每次循环求得的maxv是满足a[i]>b[k]的f[i−1][k]+1a[i] > b[k]的f[i - 1][k] + 1a[i]>b[k]的f[i−1][k]+1的前缀最大值。

因此可以直接将maxv提到第一层循环外面，减少重复计算，此时只剩下两重循环。

最终答案枚举子序列结尾取最大值即可。

时间复杂度

代码中一共两重循环，因此时间复杂度是 O(n2)O(n^2)O(n2)。

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 3500
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch))if(ch=='-')f=-f,ch=getchar();else ch=getchar();
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int f[N][N],n,a[N],b[N];
int main()
{
	n=read();for(RI i=1;i<=n;i++)a[i]=read();
	for(RI i=1;i<=n;i++)b[i]=read();int Max=1;
	for(RI i=1;i<=n;i++)
	{
		Max=1;
		for(RI j=1;j<=n;j++)
		{
	      f[i][j]=f[i-1][j];
	      if(a[i]==b[j])f[i][j]=max(f[i][j],Max);
		  if(a[i]>b[j])Max=max(Max,f[i-1][j]+1);
		}
	}
    int res=0;for(int i=1;i<=n;i++)res=max(res,f[n][i]);
    printf("%d\n", res);
	return 0;
}

`