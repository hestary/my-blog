---
title: "矩阵乘法与优化"
published: 2021-08-01
description: ""
tags: ["矩阵", "矩阵乘法", "动态规划"]
category: "dp"
draft: false
---

- 

## 

### 

矩阵相乘最重要的方法是一般矩阵乘积。它只有在第一个矩阵的列数（column）和第二个矩阵的行数（row）相同时才有意义 。一般单指矩阵乘积时，指的便是一般矩阵乘积。一个m×n的矩阵就是m×n个数排成m行n列的一个数阵。由于它把许多数据紧凑地集中到了一起，所以有时候可以简便地表示一些复杂的模型

### 

设AAA为  n∗mn*mn∗m 的矩阵，BBB为 m∗qm*qm∗q 的矩阵，那么称  的矩阵C=n∗qC=n*qC=n∗q

,并且必须满足矩阵A矩阵A矩阵A的列和矩阵B的行数矩阵B的行数矩阵B的行数一样才可以做矩阵乘法

假设此时A=3∗3B=3∗2C=3∗2\\A=3*3 \\ B=3*2  \\ C=3*2A=3∗3B=3∗2C=3∗2

A={a1,1a1,2a1,3a2,1a2,2a2,3a3,1a3,2a3,3}
 A=\left\{
 \begin{matrix}
   a_{1,1}&  a_{1,2} &  a_{1,3} \\
    a_{2,1} &  a_{2,2} &  a_{2,3} \\
    a_{3,1} &  a_{3,2}&  a_{3,3}
  \end{matrix}
  \right\} 
A=⎩⎨⎧​a1,1​a2,1​a3,1​​a1,2​a2,2​a3,2​​a1,3​a2,3​a3,3​​⎭⎬⎫​

B={b1,1b1,2b2,1b2,2b3,1b3,2}
 B=\left\{
 \begin{matrix}
   b_{1,1}  &b_{1,2} \\
    b_{2,1} &  b_{2,2} \\
    b_{3,1} &  b_{3,2}
  \end{matrix}
  \right\} 
B=⎩⎨⎧​b1,1​b2,1​b3,1​​b1,2​b2,2​b3,2​​⎭⎬⎫​

C={a1,1∗b1,1+a1,2∗b2,1+a1,3∗b3,1a1,1∗b1,2+a1,2∗b2,2+a1,2∗b3,2............}
 C=\left\{
 \begin{matrix}
    a_{1,1}*b_{1,1}+a_{1,2}*b_{2,1}+a_{1,3}*b_{3,1}&  a_{1,1}*b_{1,2}+a_{1,2}*b_{2,2}+a_{1,2}*b_{3,2} \\
   ... & ...  \\
  ...  &  ... 
  \end{matrix}
  \right\} 
C=⎩⎨⎧​a1,1​∗b1,1​+a1,2​∗b2,1​+a1,3​∗b3,1​......​a1,1​∗b1,2​+a1,2​∗b2,2​+a1,2​∗b3,2​......​⎭⎬⎫​

C[i][j]=∑a[i][k]∗a[k][j](k€[1,m])//意思就是把A的第i行和B的第j列分别相乘之后相加C[i][j]=∑a[i][k]*a[k][j]  (k€[1,m]) //意思就是把A的第i行和B的第j列分别相乘之后相加C[i][j]=∑a[i][k]∗a[k][j](k€[1,m])//意思就是把A的第i行和B的第j列分别相乘之后相加

`矩阵乘法的具体实现
I matrix operator *(const matrix &x ,const matrix &y)
{
	matrix z;memset(z.a,0,sizeof(z.a));
	z.n=x.n;z.m=y.m;
	for(RI i=1;i<=z.n;i++)
	 for(RI k=1;k<=x.m;k++)
	  for(RI j=1;j<=z.m;j++)
	   z.a[i][j]=z.a[i][j]+x.a[i][k]*y.a[k][j];
	   
	return z;
}
`

### 

矩阵的快速幂和数的快速幂是一个道理！

并且矩阵乘法不一定任何时候都有交换律。因为交换后甚至不能保证第一个矩阵的列数等于第二个矩阵的行数。

但是，矩阵乘法有结合律。A∗B∗C=A∗(B∗C)A*B*C=A*(B*C)A∗B∗C=A∗(B∗C)

这是一个最常用的运算律，使之可以用矩阵快速幂。

`#include<bits/stdc++.h>
#define LL long long 
#define RI  register int 
#define RL register long long
#define maxn 150
#define I inline 
#define mod 1000000007

using namespace std;

I LL read()
{
     RL res=0,f=1;char ch=getchar();
     while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
     while(isdigit(ch)){res=(res<<1)+(res<<3)+(ch&15);ch=getchar();}
     return res*f;
} 
LL n,k;

struct matrix{
	LL a[maxn][maxn];
}m1,m2;

I matrix operator *(const matrix &x ,const matrix &y)
{
	matrix z;memset(z.a,0,sizeof(z.a));
	for(RI i=1;i<=n;i++)
	 for(RI k=1;k<=n;k++)
	  for(RI j=1;j<=n;j++)
	   z.a[i][j]=(z.a[i][j]+x.a[i][k]*y.a[k][j]%mod)%mod;
	   
	return z;
}

I void init()
{
     n=read();k=read();
     for(RI i=1;i<=n;i++)
     {
     	m2.a[i][i]=1;
		for(RI j=1;j<=n;j++)
		m1.a[i][j]=read();	
	 }
} 
I void print()
{
	for(RI i=1;i<=n;i++)
	{
		for(RI j=1;j<=n;j++)cout<<m2.a[i][j]<<' ';
		putchar('\n');
	}
}
I void fastpow()
{
	while(k)
	{
		if(k&1)m2=m2*m1;//把其乘到答案矩阵
		m1=m1*m1;//快速幂
		k>>=1;
	}
	return ;
}
int main()
{
	init();
	fastpow();
	print();
	return 0;
}
`

## 

### 

#### 

我们都知道斐波那契数列的递推式子是

f(n)={1x≤2f(n−1)+f(n−2)x≥3f(n)=
\begin{cases}
1& {x\le2}\\
f(n-1)+f(n-2)& {x\ge3}
\end{cases}f(n)={1f(n−1)+f(n−2)​x≤2x≥3​

但是当题目让我们求斐波那契数列的第10910^9109项怎么办？数组没法存，并且O(n)O(n)O(n)还要超时，那么有没有一种方法可以缩短时间呢?

答案是能！就是运用到了我们上面的矩阵乘法

假设刚开始：

A={f1f2}
 A=\left\{
 \begin{matrix}
  f1&  f2
  \end{matrix}
  \right\} 
A={f1​f2​}

我们要推出下一步

C={f2f3}
 C=\left\{
 \begin{matrix}
  f2&  f3
  \end{matrix}
  \right\} 
C={f2​f3​}

我们构造一个B矩阵

B={0111}
B=\left\{
 \begin{matrix}
  0&  1\\
  1 & 1
  \end{matrix}
  \right\} 
B={01​11​}

发现只需要让C=A∗BC=A*BC=A∗B

我们解决了一个问题就是：通过矩阵乘法也可以推出斐波那契数列的后面一项，但是好像每次乘矩阵B的复杂度也是O(n)O(n)O(n)

A∗B∗B....∗B=f(n)A*B*B....*B=f(n)A∗B∗B....∗B=f(n)

于是我们可以把中间的好多个乘矩阵B给简化成为矩阵快速幂

A∗Bn−2=f(n)A*B^{n-2}=f(n)A∗Bn−2=f(n)

这样就可以在O(logn)O(logn)O(logn)的情况下fast解决这道题目

`#include<bits/stdc++.h>
#define LL long long 
#define RI  register int 
#define RL register long long
#define maxn 150
#define I inline 
#define mod 1000000007

using namespace std;

I LL read()
{
     RL res=0,f=1;char ch=getchar();
     while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
     while(isdigit(ch)){res=(res<<1)+(res<<3)+(ch&15);ch=getchar();}
     return res*f;
} 
LL n,k;

struct matrix{
	int n,m; 
	LL a[maxn][maxn];
}m1,m2;

I matrix operator *(const matrix &x ,const matrix &y)//矩阵乘法
{
	matrix z;memset(z.a,0,sizeof(z.a));
	z.n=x.n;z.m=y.m;
	for(RI i=1;i<=z.n;i++)
	 for(RI k=1;k<=x.m;k++)
	  for(RI j=1;j<=z.m;j++)
	   z.a[i][j]=(z.a[i][j]+x.a[i][k]*y.a[k][j]%mod)%mod;
	   
	return z;
}

I void init()
{
     n=read();
     if(n<=2){putchar('1');exit(0);}//初始化矩阵
     n-=2;
     m1.n=1;m1.m=2;
     m1.a[1][1]=1;m1.a[1][2]=1;
     m2.n=2;m2.m=2;
     m2.a[1][1]=0;m2.a[1][2]=1;
     m2.a[2][1]=1;m2.a[2][2]=1;
} 
I void fastpow()
{
	while(n)
	{
		if(n&1)m1=m1*m2;
		m2=m2*m2;
		n>>=1;
	}
	return ;
}
int main()
{
	init();
	fastpow();
	cout<<m1.a[1][2];
	return 0;
}
`

#### 

题目大意就是

f(n)={1x≤3f(n−1)+f(n−3)x≥4f(n)=
\begin{cases}
1& {x\le3}\\
f(n-1)+f(n-3)& {x\ge4}
\end{cases}f(n)={1f(n−1)+f(n−3)​x≤3x≥4​

我们和上面一样的做法

A={f1f2f3}
 A=\left\{
 \begin{matrix}
  f1&  f2 & f3
  \end{matrix}
  \right\} 
A={f1​f2​f3​}

我们要推出下一步

C={f2f3f4}
 C=\left\{
 \begin{matrix}
  f2&  f3 & f4
  \end{matrix}
  \right\} 
C={f2​f3​f4​}

我们构造一个B矩阵

B={001100011}
B=\left\{
 \begin{matrix}
  0&  0& 1\\
  1 & 0&0\\
  0&1&1
  \end{matrix}
  \right\} 
B=⎩⎨⎧​010​001​101​⎭⎬⎫​

就解决了

`#include<bits/stdc++.h>
#define LL long long 
#define RI  register int 
#define RL register long long
#define maxn 150
#define I inline 
#define mod 1000000007

using namespace std;

I LL read()
{
     RL res=0,f=1;char ch=getchar();
     while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
     while(isdigit(ch)){res=(res<<1)+(res<<3)+(ch&15);ch=getchar();}
     return res*f;
} 
LL n,k;

struct matrix{
	int n,m; 
	LL a[maxn][maxn];
}m1,m2;

I matrix operator *(const matrix &x ,const matrix &y)
{
	matrix z;memset(z.a,0,sizeof(z.a));
	z.n=x.n;z.m=y.m;
	for(RI i=1;i<=z.n;i++)
	 for(RI k=1;k<=x.m;k++)
	  for(RI j=1;j<=z.m;j++)
	   z.a[i][j]=(z.a[i][j]+x.a[i][k]*y.a[k][j]%mod)%mod;
	   
	return z;
}

I void init()
{
     n-=3;
     m1.n=1;m1.m=3;
     m1.a[1][1]=1;m1.a[1][2]=1;m1.a[1][3]=1;
     m2.n=3;m2.m=3;
     m2.a[1][1]=0;m2.a[1][2]=0;m2.a[1][3]=1;
     m2.a[2][1]=1;m2.a[2][2]=0;m2.a[2][3]=0;
     m2.a[3][1]=0;m2.a[3][2]=1;m2.a[3][3]=1;
} 
I void fastpow()
{
	while(n)
	{
		if(n&1)m1=m1*m2;
		m2=m2*m2;
		n>>=1;
	}
	return ;
}
int T;
int main() 
{
	T=read();
	while(T--)
	{ 
	 n=read();if(n<=3){puts("1");continue;}
	init();
    
	fastpow();
	cout<<m1.a[1][3]<<endl;
	}
	return 0;
}
`

### 

![]\(https://i-blog.csdnimg.cn/blog_migrate/96b76658eb6c45b9f69d41b4e1a42c00.png)

优化要满足一下四个条件

是二维的f[i][j]f[i][j]f[i][j]
- 从i−1i-1i−1转移到iii
- 是Σ求和Σ求和Σ求和
- 转移系数也就是上图中的z[k][j]z[k][j]z[k][j]和iii无关