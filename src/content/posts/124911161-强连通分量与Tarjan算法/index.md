---
title: "强连通分量与Tarjan算法"
published: 2022-05-28
description: ""
tags: ["图论", "算法", "数据结构"]
category: "算法进阶—进阶指南"
draft: false
---

- 


时间戳

在图的深度优先遍历过程中，按照每个节点第一次被访问的时间顺序，依次给子NNN

个节点1 N1~N1 N的整数标记，该标记就被称为“时间戳”，记为dfn[x]dfn[x]dfn[x]。

搜索树

在无向连通图中任选一个节点出发进行深度优先遍历，每个点只访问一次。所有发

生递归的边(x,y)(x,y)(x,y) (换言之，从xxx到yyy是对yyy的第一次访问)构成一棵树， 我们把

它称为“无向连通图的搜索树”。当然，一般无向图(不一定连通)的各个连通块的搜

索树构成无向图的“搜索森林”。

下图左侧展示了一张无向连通图，灰色节点是深度优先遍历的起点，加粗的边是

“发生递归”的边(假设我们在遇到多个分支时，总是优先访问最靠左的一条)。右侧

展示了深度优先遍历的搜索树，并标注了节点的时间戳。

![]\(https://i-blog.csdnimg.cn/blog_migrate/2441d6b776ef2cc4498f585dc391b625.png)

追溯值

除了时间戳之外，TarianTarianTarian 算法还引入了一个“追溯值”low[x]low[x]low[x]。 设subtree(x)subtree(x)subtree(x) 表

示搜索树中以xxx为根的子树。low[x]low[x]low[x] 定义为以下节点的时间戳的最小值:

subtree(x)subtree(x)subtree(x)中的节点。
- 通过111条不在搜索树上的边，能够到达subtree(x)subtree(x)subtree(x) 的节点。

以上图为例。为了叙述简便,我们用时间戳代替节点编号。subtree(2)=2,3,4,5subtree(2) = {2,3,4,5}subtree(2)=2,3,4,5。

另外，节点1通过不在搜索树上的边(1,5)边(1,5)边(1,5)能够到达subtree(2)subtree(2)subtree(2)。 所以low[2]=1low[2] = 1low[2]=1。

根据定义，为了计算low[x]low[x]low[x]， 应该先令low[x]=dfn[x]low[x] = dfn[x]low[x]=dfn[x],然后考虑从x出发的

每条边(x,y):(x,y):(x,y):

若在搜索树上x是y的父节点，则令low[x]=min(low[x],low[y])。low[x] = min(low[x], low[y])。low[x]=min(low[x],low[y])。

若无向边(x,y) 不是搜索树上的边，则令low[x]=min(low[x],dfn[y])。low[x] = min(low[x],dfn[y])。low[x]=min(low[x],dfn[y])。

下页图的中括号0里的数值标注了每个节点的“ 追溯值”lowlowlow。


割点判定法则

若xxx不是搜索树的根节点(深度优先遍历的起点)，则x是割点当且仅当搜索树

上存在x的一个子节点y，满足:

dfn[x]≤low[y]dfn[x]≤low[y]dfn[x]≤low[y]

特别地，若x是搜索树的根节点，则xxx是割点当且仅当搜索树.上存在至少两个

子节点y1y1y1,y2y2y2满足上述条件。

证明方法与割边的情形类似，这里就不再赘述。在“割边判定法则”画出的例子

中，共有222个割点，分别是时间戳为111和666的两个点。

下面的程序求出一张无向图中所有的割点。因为割点判定法则是小于等于号，所以

在求割点时，不必考虑父节点和重边的问题，从x出发能访问到的所有点的时间戳都

可以用来更新low[x]low[x]low[x]。


给定一个 nnn 个点 mmm 条边有向图，每个点有一个权值，求一条路径，使路径经过的点权值之和最大。你只需要求出这个权值和。

允许多次经过一条边或者一个点，但是，重复经过的点，权值只计算一次。


第一行两个正整数 n,mn,mn,m

第二行 nnn 个整数，其中第 iii 个数 aia_iai​ 表示点 iii 的点权。

第三至 m+2m+2m+2 行，每行两个整数 u,vu,vu,v，表示一条 u→vu\rightarrow vu→v 的有向边。


共一行，最大的点权之和。


`2 2
1 1
1 2
2 1
`


`2
`


对于 100%100\%100% 的数据，1≤n≤1041\le n \le 10^41≤n≤104，1≤m≤1051\le m \le 10^51≤m≤105，0≤ai≤1030\le a_i\le 10^30≤ai​≤103。

缩点之后DAG上跑topu

`#include<bits/stdc++.h>   
#define mod 998244353
#define LL long long    
#define I inline
#define RI register int 
#define debug cout << "debug"<<endl
#define O(x) cout<< #x <<' '<<x<<endl
#define o(x) cout<< #x <<' '<<x<<' '; 
#define inf 1e15
#define N 10010
#define M 200010
using namespace std;
I int read()
{
	int res=0,f=1;char ch=getchar();
	while(!isdigit(ch))if(ch=='-')f=-f,ch=getchar();else ch=getchar();
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int n,m;
int head[N],tot,tot2,h[N];
struct node{
	int to,next;
}edge[M],e[M];
I void add(int x,int y){
	edge[++tot].to=y;
	edge[tot].next=head[x];
	head[x]=tot;
}
I void Add(int x,int y){
	e[++tot2].to=y;
	e[tot2].next=h[x];
	h[x]=tot2;
}
int low[N],dfn[N],intime,val[N];
int stacker[N],top,vis[N];
int id[N],type,tval[N],du[N],Ans[N];
I void Tarjan(int x){
	low[x]=dfn[x]=++intime;
	stacker[++top]=x;vis[x]=1;
	for(RI i=head[x];i;i=edge[i].next){
		int to=edge[i].to;
		if(!dfn[to]){
			Tarjan(to);
			low[x]=min(low[x],low[to]);
		}else low[x]=min(low[x],dfn[to]);//important
	}
	if(dfn[x]==low[x]){
		int k=0;type++;
		while(k!=x){
			k=stacker[top--];
			id[k]=type;vis[k]=0;
			tval[type]+=val[k];
		}
	}
}
queue<int>Q;
I void topu()
{
    for(RI i=1;i<=type;i++)Ans[i]=tval[i];
	for(RI i=1;i<=type;i++)if(!du[i])Q.push(i);
	while(!Q.empty()){
		int k=Q.front();Q.pop();
		for(RI i=h[k];i;i=e[i].next){
			int to=e[i].to;du[to]--;
		    Ans[to]=max(Ans[to],tval[to]+Ans[k]);
			if(!du[to])Q.push(to);
		}
	}
}
int main()
{
	n=read();m=read();
	for(RI i=1;i<=n;i++)val[i]=read();
	for(RI i=1;i<=m;i++){
		RI u,v;u=read();v=read();
		add(u,v);
	}
	for(RI i=1;i<=n;i++)if(!dfn[i])Tarjan(i);
	for(RI i=1;i<=n;i++){
		for(RI j=head[i];j;j=edge[j].next){
			int to=edge[j].to;
			int a=id[i],b=id[to];
			if(a==b)continue;
			Add(a,b);du[b]++;
		}
	}
	topu();int ans=0;for(RI i=1;i<=type;i++)ans=max(ans,Ans[i]);
	printf("%d",ans);return 0;
}
`