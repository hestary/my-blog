---
title: "poj 1011 Sticks_输入包含2行的块。第一行包含切割后的木棒零件数,最多64根。第二行包含由空格分隔"
published: 2020-07-31
description: ""
tags: ["剪枝", "算法", "dfs"]
category: "dfs"
draft: false
---

- 

                    **

乔治随机抽取了50根长棍。现在他想把棍子恢复到原来的状态，但是他忘了他原来有多少根棍子和它们原来有多长。请帮助他设计一个程序，计算出这些棍子可能的最小原始长度。所有以单位表示的长度都是大于零的整数。

输入包含2行的块。第一行包含切割后的木棒零件数，最多64根。第二行包含由空格分隔的部分的长度。文件的最后一行包含零。

输出应包含尽可能短的原始棒长度，每行一个。

样本输入

9

5 2 1 5 2 1 5 2 1 5 2 1

4

1 2 3 4

0

样本输出

6

5

## 

暴力**大法师（dfs）**+剪枝

### 

从小到大枚举原始木棍的长度，每次进行相应的check，如果返回为*真*，即可输出答案；

长度为 len  根数 为 cnt=sum/len  dfs 四个参数  已经拼好了几个，当前这个拼了多少长，上一个使用的木条的编号**，暴力想法完成，再想剪枝。

### 

优化搜索顺序：把木棍从大到小进行排序，每次从大到下，递减选。从上一个使用的木条编号开始
- 排除等效冗余（1）：对于当前木棒，记录最新一次拼接的木棒，如果拼接这个木棒达不到原始木棒的长度，那么拼接和这个木棒相同长度的木棒也是达不到目标长度
- 排除等效冗余（2）：对于一个原始木棒，如果第一个木棒都加不进去，那么就无需递归，直接返回FALSE
- 排除等效冗余（3）：如果当前原始木棒中拼入一根木棒后，刚好拼接完整，并且“接下来拼接剩余原始木棒”的递归分支返回失败，那么直接判定当前分支失败，立刻回溯，该剪枝可以用贪心证明，“再用一根木棍拼接成原始木棍”肯定比“再用若干个木棍拼接成原始木棍”更优

`#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <cmath>

using namespace std;
int a[150],v[150],n,len,cnt;//木棍长度  木棍标记 木棍个数 原始木棍长度 原始木棍个数
bool dfs(int stick,int cab,int last)
{    //已经拼接第stick个原始木棍
     //当前拼接原始木棍的长度
     //上一个使用的木棍编号+1
	if(stick>cnt)return true;//能拼接完
	if(cab==len)return dfs(stick+1,0,1);//拼接下一个
	int fail=0;//记录相同长度的木棍（排除等效冗余（1））
	for(int i=last;i<=n;i++)//递减拼接
	{
		if(!v[i]&&cab+a[i]<=len&&fail!=a[i])//没有标记过&&拼接起来小于原始木棍&&不是相同标记
		{
			v[i]=1;//拼接此木棍，标记
			if(dfs(stick,cab+a[i],i+1))return true;//往下递归
			fail=a[i];//记录相同
			v[i]=0;//回溯，还原现场
			if(cab==0||cab+a[i]==len)return false;//剪枝（3）（4）
		}
	}
	return false;//拼接失败
}
bool cmp(int x,int y)//制定快排规则
{
	return x>y;//从大到小
}
int main()
{
	while(cin>>n&&n)//注意有多组测试数据
	{
		int sum=0,val=0;//木棍和 木棍最大的长度
		for(int i=1;i<=n;i++)//输入
		{
			cin>>a[i];//输入
			sum+=a[i];val=max(val,a[i]);//维护两个变量值
		}
		sort(a+1,a+1+n,cmp);//大到小排序
		for(len=val;len<=sum;len++)//枚举原始木棍的len
		{
			if(sum%len==0)//如果可以拼接 len肯定是木棍总和的因数
			{
				cnt=sum/len;//原始木棍个数
			    memset(v,0,sizeof(v));//清空标记
			    if(dfs(1,0,1))//check一下
			    {
			    	cout<<len<<endl;//可以拼接就输出
			    	break;//已经找到答案，退出
				}
			}
		}
	}
	return 0;//完美ＡＣ
}
`