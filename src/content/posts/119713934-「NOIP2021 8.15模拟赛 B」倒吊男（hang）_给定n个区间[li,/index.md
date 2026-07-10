---
title: "「NOIP2021 8.15模拟赛 B」倒吊男（hang）_给定n个区间[li,ri],你需要把它们划分成两部分a,b。 求|∩i∈a[li,ri]|+|∩i∈"
published: 2021-08-15
description: ""
tags: ["算法", "数据结构"]
category: "比赛"
draft: false
---

- 


给定n个区间[li,ri][li,ri][li,ri]，你需要把它们划分成两部分A,B。

求∣∩i∈A[li,ri]∣+∣∩i∈B[li,ri]∣|∩i∈A[li,ri]|+|∩i∈B[li,ri]|∣∩i∈A[li,ri]∣+∣∩i∈B[li,ri]∣（即两部分区间交集大小之和）的最大值。

---

显然，对于一些区间 [l,r][l,r][l,r]，它们的交集大小是 max(0,min(r[i])−max(l[i])+1)max(0,min(r[i])-max(l[i])+1)max(0,min(r[i])−max(l[i])+1)。

因此，可以先将区间按左端点排序，然后枚举其中一个区间左端点最大值为 lil_ili​，则另一个区间左端点最大值为lnl_nln​ 。

而对于右端点，有两种可能性。

设第1 − i1 \ - \ i1 − i 条线段中最小rrr的 为rminr_{min}rmin​ ，最大的为 rmaxr_{max}rmax​，第i+1−ni+1-ni+1−n 中最小rrr 为MnMnMn 。

那么最优情况下，两个集合的rminr_{min}rmin​为：

1−i1-i1−i为一个区间，i+1−−ni+1--ni+1−−n为一个
- j−−ij--ij−−i为一个  1−j and i+1−n1-j  \ and \ i+1-n1−j and i+1−n为一个(jjj为rmaxr_{max}rmax​的下标)

（注意，这里的可能不会取到当前区间而是先前某个区间，但这样相当于把左端点取得比实际情况偏大了，肯定不优）

确定了左端点和右端点，就可以据此更新答案了。

`#include<bits/stdc++.h>
#define N 5000010
using namespace std;
struct node{
	int x,y;
}A[N];
bool cmp(node x,node y){
	return x.x<y.x;
}
int n,ans,P[N];
int main()
{
	cin>>n;
	for(int i=1;i<=n;i++)cin>>A[i].x>>A[i].y,ans=max(ans,A[i].y-A[i].x+1);
	sort(A+1,A+1+n,cmp);
	P[n]=A[n].y;
	for(int i=n-1;i;i--) P[i]=min(A[i].y,P[i+1]);
	int Mx=A[1].y,Mn=A[1].y;
	for(int i=1;i<n;i++)
	{
		Mx=max(Mx,A[i].y),Mn=min(Mn,A[i].y);
		ans=max(ans,max(Mn-A[i].x+1,0)+max(P[i+1]-A[n].x+1,0));
		ans=max(ans,max(Mx-A[i].x+1,0)+max(min(P[i+1],Mn)-A[n].x+1,0));
	}
	cout<<ans;
	return 0;
}
`