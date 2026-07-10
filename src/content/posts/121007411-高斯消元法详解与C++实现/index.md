---
title: "高斯消元法详解与C++实现"
published: 2021-10-28
description: ""
tags: ["线性代数", "矩阵"]
category: "算法进阶—进阶指南"
draft: false
---

- 


高斯消元法(Gaussian elimination)是求解线性方阵组的一种算法，它也可用来求矩阵的秩，以及求可逆方阵的逆矩阵。它通过逐步消除未知数来将原始线性系统转化为另一个更简单的等价的系统。它的实质是通过初等行变化(Elementary row operations)，将线性方程组的增广矩阵转化为行阶梯矩阵(row echelon form).

---


求解形如

(a1x1+b1x2+c1x3=W1a2x1+b2x2+c2x3=W2a2x1+b2x2+c2x3=W2)\begin{pmatrix}
  & a_1x_1+b_1x_2+c_1x_3=W_1\\
  & a_2x_1+b_2x_2+c_2x_3=W_2\\
  &a_2x_1+b_2x_2+c_2x_3=W_2
\end{pmatrix}⎝⎛​​a1​x1​+b1​x2​+c1​x3​=W1​a2​x1​+b2​x2​+c2​x3​=W2​a2​x1​+b2​x2​+c2​x3​=W2​​⎠⎞​

方程组


先发现几个性质只要把方程组转化为：

(x1+b1x2+c1x3=W10x1+x2+c2x3=W20x1+0x2+c2x3=W2)\begin{pmatrix}
  & x_1+b_1x_2+c_1x_3=W_1\\
  & 0x_1+x_2+c_2x_3=W_2\\
  &0x_1+0x_2+c_2x_3=W_2
\end{pmatrix}⎝⎛​​x1​+b1​x2​+c1​x3​=W1​0x1​+x2​+c2​x3​=W2​0x1​+0x2​+c2​x3​=W2​​⎠⎞​

就可以求方程的答案了，所以我们选择一排一排地消除，就是消除n此

对于每次操作

找到第i列绝对值最小的系数，把它和第一列做交换
- 将这次操作的一列的系数化为1，更新一行的所有值（div 这一列的系数）
- 将其他行的这一列的系数全部化为0（-它自己的系数）
- 倒序三角形求答案


`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define D double
#define N 1500
using namespace std;

D a[N][N];
int n,c;
I void print(){
		for(RI i=1;i<=n;i++){
		printf("%.2f ",a[i][n+1]);
		printf("\n");
	}
}
int main()
{
	scanf("%d",&n);
	for(RI i=1;i<=n;i++)for(RI j=1;j<=n+1;j++)scanf("%lf",&a[i][j]);
	
	for(RI i=1;i<=n;i++){
		int t=i;
		for(RI j=i+1;j<=n;j++)
		if(fabs(a[j][i])>fabs(a[t][i]))t=j;	

		for(RI j=1;j<=n+1;j++)swap(a[t][j],a[i][j]);
		 
		if(!a[i][i]){puts("No Solution");return 0;}
		for(RI j=n+1;j>=i;j--)a[i][j]=a[i][j]/a[i][i];
		for(RI j=i+1;j<=n;j++)
		for(RI k=n+1;k>=i;k--){
			if(a[j][k]){
				a[j][k]-=a[j][i]*a[i][k];
			}
		}
	}
	a[n][n+1]/=a[n][n];
    for(RI i=n;i>=1;i--){
    	for(RI j=i+1;j<=n;j++)
        a[i][n+1]-=a[i][j]*a[j][n+1];
	}
	print();
	return 0;
}
`