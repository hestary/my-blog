---
title: "Tarjan算法与无向图的连通性_无向图tarjan"
published: 2022-10-17
description: ""
tags: ["算法", "图论", "深度优先"]
category: "比赛"
draft: false
---

- 

### 

`给定无向连通图G=(V，E)：
若对于x∈V，从图中删去节点x以及所有与x关联的边之后，G分裂成两个
`
或两个以上不相连的子图，则称x为G的割点.

若对于e∈E，从图中删去边e之后，G分裂成两个不相连的子图，则称e为

G的桥或割边.

一般无向图(不一定连通)的“割点”和“桥”就是它的各个连通块的“割点”和

“桥”

根据著名计算机科学家RobertTarjan的名字命名的Tarjan算法能够在线性时间内

(求出无向图的割点与桥，进一步可求出无向图的双连通分量(本节后半部分将会介绍)。

在有向图方面，Tarjan算法能够求出有向图的强连通分量、必经点与必经边(下一节将

(会介绍)。罗伯特·塔尔健在数据结构方面也做出了很多卓有成效的工作，包括证明并查集的时间复杂度，提出斐波那契堆、Splay Tree和Lint-Cut Tree等.

#### 

在图的深度优先遍历过程中，按照每个节点第一次被访间的时间顺序，依次给予N

个节点1~N的整数标记，该标记就被称为“时间戳”，记为dfn[x]。

#### 

在无向连通图中任选一个节点出发进行深度优先遍历，每个点只访问- -次。 所有发

生递归的边(x,y) (换言之，从x到y是对y的第一次访问)构成- - 棵树，我们把

它称为“无向连通图的搜索树”。当然，一般无向图 (不- - 定连通)的各个连通块的搜

索树构成无向图的“搜索森林”。

下图左侧展示了一张无向连通图，灰色节点是深度优先遍历的起点，加粗的边是

“发生递归”的边(假没我们在遇到多个分支时，总是优先访问最靠左的一一条)。右侧

展示了深度优先遍历的搜索树，并标注了节点的时间戳。

#### 

除了时间戳之外，Tarjan 算法还引入了一个“追溯值”low[x]。设subree(x) 表

示搜索树中以x为根的子树。low[x] 定义为以下节点的时间戳的最小值:

subtree(x)中的节点。

2.通过1条不在搜索树上的边，能够到达subtree(x) 的节点。

以上图为例。为了叙述简便，我们用时间戳代替节点编号。subtree(2) = {2.3.4.5}。

另外，节点1通过不在搜索树上的边(1,5) 能够到达subtree(2)。 所以low|2]= 1。

根据定义，为了计算low[x], 应该先令low[x] = dfn[x]，然后考虑从x出发的

每条边(x,y):

若在搜索树上x是y的父节点，则令low[x] = min(low[x], low[y])。

若无向边(x,y) 不是搜索树上的边，则令low[x] = min(low[x], dfn[y]).

下页图的中括号0里的数值标注了每个节点的“追溯值”low。

#### 

dfn[x]<low[y]dfn[x]<low[y]dfn[x]<low[y]

y属于x的一个子节点

感性理解一下就是，没有其他的路径可比这个点x 更早地走到y点，因此删掉这个点之后整张图就断裂开了，所以说这条边必然是桥，但是桥必然是在搜索树上面的，因此当输入的图有重边的时候，就无法判断，因为其他的重边不在dfs树里面，因此搜索的时候，dfs的传参为那一条边，而且连接自己父节点的边都是成对出现的，因此可以用异或1来实现成对变换

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 1000100
#define LL long long 
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int dfn[N],low[N],bridge[N],tot,head[N];
struct node{
	int to,next;
}edge[N<<1];
I void add(int x,int y){
	edge[++tot].next=head[x];
	edge[tot].to=y;
	head[x]=tot;
}
int n,m,num;
I void Tarjan(int x,int ineg){
	dfn[x]=low[x]=++num;
	for(RI i=head[x];i;i=edge[i].next){
		int to=edge[i].to;
		if(!dfn[to]){
			Tarjan(to,i);
			low[x]=min(low[x],low[to]);
			if(low[to]>dfn[x])
				bridge[i]=bridge[i^1]=1;
		}else if(i!=(ineg^1))low[x]=min(low[x],dfn[to]);
	}
}
int main()
{
	n=read();m=read();tot=1;
	for(RI u,v,i=1;i<=m;i++){
		u=read();v=read();
		add(u,v);add(v,u);
	}for(RI i=1;i<=n;i++)if(!dfn[i])Tarjan(i,0);
	for(RI i=2;i<tot;i+=2)if(bridge[i])printf("%d %d\n",edge[i].to,edge[i+1].to);
	return 0;
}
`

#### 

若x不是搜索树的根节点(深度优先遍历的起点)，则x是割点当且仅当搜索树

上存在x的一个子节点y,满足:

dfn[x]≤low[y]dfn[x]≤low[y]dfn[x]≤low[y]

特别地，若x是搜索树的根节点，则x是割点当且仅当搜索树上存在至少两个

子节点y1.Y2满足上述条件。

证明方法与割边的情形类似，这里就不再赘述。在“割边判定法则”画出的例子

中，共有2个割点，分别是时间戳为1和6的两个点。

**下面的程序求出一张无向图中所有的割点。因为割点判定法则是小于等于号，所以

在求割点时，不必考虑父节点和重边的问题**，从x出发能访问到的所有点的时间戳都

可以用来更新low[x]。

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 6000100
#define LL long long 
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int dfn[N],low[N],bridge[N],tot,head[N];
struct node{
	int to,next;
}edge[N<<1];
I void add(int x,int y){
	edge[++tot].next=head[x];
	edge[tot].to=y;
	head[x]=tot;
}
int n,m,num,root,vis[N],d;
I void Tarjan(int x){
	dfn[x]=low[x]=++num;int flag=0;
	for(RI i=head[x];i;i=edge[i].next){
		int to=edge[i].to;
		if(!dfn[to]){
			Tarjan(to);
			low[x]=min(low[x],low[to]);
			if(low[to]>=dfn[x]){
				flag++;
				if(flag>1||x!=root)vis[x]=1;
			}
				
		}else low[x]=min(low[x],dfn[to]);
	}
}
int main()
{
//	freopen("P3388_4.in","r",stdin);
//	freopen("1.txt","w",stdout);
	n=read();m=read();
	for(RI u,v,i=1;i<=m;i++){
		u=read();v=read();if(u==v)continue;
		add(u,v);add(v,u);
	}for(RI i=1;i<=n;i++)if(!dfn[i])root=i,Tarjan(i);
	for(RI i=1;i<=n;i++)if(vis[i])d++;
	cout<<d<<endl;
	for(RI i=1;i<=n;i++)if(vis[i])printf("%d ",i);
	return 0;
}
`

#### 

若一张无向连通图不存在割点，则称它为“点双连通图”。若-张无向连通图不存

在桥，则称它为“边双连通图”。

无向图的极大点双连通子图被称为“点双连通分量”。简记为“v-DCC"中。无向

连通图的极大边双连通子图被称为“边双连通分量”，简记为“e-DCC".二者统称

为“双连通分量”，简记为“DCC"。

E"SE并且G"也是双连通子图。

定理

-张无向连通團是“点双连通图”，当且仅当满足下列两个条件之一 :

1.图的项点数不超过2。

2.图中任意两点都同时包含在至少一个简单环中。其中“简单环”指的是不自交

的环，也就是我们通常画出的环。

一张无向连通图是“边双连通图”，当且仅当任意-条边都包含在至少一个简单

环中。

##### 

该定理给出了无向连通图是“点双连通图”或“边双连通图”的充要条件。我们

以“点双连通图”为例进行证明，对于“边双连通图"的证明，请读者自己完成。

对于顶点数不超过2的情况，定理显然成立，下 面假设图中顶点数不小于3.

先证充分性。若任意两点x,y都同时包含在至少一个简单环中，则x,y之间至

少有两条不相交的路径。无论从图中删除哪个节点。xy均能通过两条路径之一相连。

故图中不存在割点，是点双连通图。

再证必要性。反证法，假设- -张无向连通图是“点双连通图" ,并且存在两点x,y. .

它们不同时处于任何一个简单环中。

如果x,y之间仅存在1条简单路径,那么路径上至少有一个割点,与“点双连通”

矛盾。

如果x,y之间存在2条或2条以上的简单路径，那么容易发现，任意两条都至少

有一个除x,y之外的交点:进-一步可推导出，x,y 之间的所有路径必定同时交于除

x,y之外的某- -点p(不然就会存在两条没有交点的路径，形成- -个简单环,如下图所

示)。

根据定义，p是一个割点。与“点双连通”矛盾。故假设不成立。

证毕。

#### 

边双连通分量的计算非常容易。只需求出无向图中所有的桥，把桥都删除后，无向

图论

图会分成若干个连通块，每一个连通块就是一个“边双连通分量”。

下面的无向图共有2条“桥”边。3个“边双连通分量" :

在具体的程序实现中，- -般先用Tarjan算法标记出所有的桥边。然后，再对整个

无向图执行-次深度优先遍历(遍历的过程中不访问桥边)。划分出每个连通块。下面

的代码在Taran求桥的参考程序基础上,计算出数组e, c[x]表示节点x所属的“边

双连通分量”的编号。

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 6000100
#define LL long long 
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int dfn[N],low[N],bridge[N],tot,head[N];
struct node{
	int to,next;
}edge[N<<1];
I void add(int x,int y){
	edge[++tot].next=head[x];
	edge[tot].to=y;
	head[x]=tot;
}
int n,m,num;
I void Tarjan(int x,int ineg){
	dfn[x]=low[x]=++num;
	for(RI i=head[x];i;i=edge[i].next){
		int to=edge[i].to;
		if(!dfn[to]){
			Tarjan(to,i);
			low[x]=min(low[x],low[to]);
			if(low[to]>dfn[x])
				bridge[i]=bridge[i^1]=1;
		}else if(i!=(ineg^1))low[x]=min(low[x],dfn[to]);
	}
}
vector<int>G[N];
int vis[N],cnt;
I void dfs(int x){
	vis[x]=cnt;G[cnt].push_back(x);
	for(RI i=head[x];i;i=edge[i].next){
		int to=edge[i].to;
		if(vis[to]||bridge[i])continue;
		dfs(to);
	}
} 
int main()
{
	n=read();m=read();tot=1;
	for(RI u,v,i=1;i<=m;i++){
		u=read();v=read();
		add(u,v);add(v,u);
	}for(RI i=1;i<=n;i++)if(!dfn[i])Tarjan(i,0);
	for(RI i=1;i<=n;i++)if(!vis[i])++cnt,dfs(i); 
	printf("%d \n",cnt);
	for(RI i=1;i<=cnt;i++){printf("%d ",G[i].size());
		for(RI j=0;j<G[i].size();j++)
		printf("%d ",G[i][j]);putchar('\n'); 
	}
//	for(RI i=2;i<tot;i+=2)if(bridge[i])printf("%d %d\n",edge[i].to,edge[i+1].to);
	return 0;
}
`

#### 

“点双连通分量”是一个极其容易误解的概念。它与前面的例题“BLO"中“删除

割点后图中剩余的连通块”是不一样的， 请读者格外留意。

若某个节点为孤立点，则它自己单独构成一个v-DCC.除了孤立点之外。点双连通

分量的大小至少为2。根据v-DCC定义中的“极大”性，虽然桥不属于任何e-DCC,但

是制点可能属于多个v-DCC.还是来看本节- - 直使用的例子，下面的无向图共有2个

割点，4个“点双连通分量”.。

为了求出“点双连通分量”，需要在Tarlan算法的过程中维护一个栈，并按照如

下方法维护栈中的元素: .

1.当一个节点第一次被访问时，把该节点入栈。

2.当割点判定法则中的条件dfn[x] s low[y]成立时，无论x是否为根，都要:

(1)从栈顶不断弹出节点，直至节点y被弹出。

(2)刚才弹出的所有节点与节点x -起构成一-个v-DCC.

下面的程序在求出割点的同时。计算出vector数组dcc. dee[i] 保存编号为i的

v-DCC中的所有节点。

`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define N 6000100
#define LL long long 
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int dfn[N],low[N],bridge[N],tot,head[N];
struct node{
	int to,next;
}edge[N<<1];
I void add(int x,int y){
	edge[++tot].next=head[x];
	edge[tot].to=y;
	head[x]=tot;
}
int stk[N];
int n,m,num,root,vis[N],top,cnt;
vector<int>G[N];
//int root;
I void Tarjan(int x){
	if(head[x]==0&&x==root){G[++cnt].push_back(x);return;}
	stk[++top]=x;dfn[x]=low[x]=++num;int flag=0;
	for(RI i=head[x];i;i=edge[i].next){
		int to=edge[i].to;
		if(!dfn[to]){
			Tarjan(to);
			low[x]=min(low[x],low[to]);
			if(low[to]>=dfn[x]){
				flag++;
				if(flag>1||x!=root)vis[x]=1;RI z;
				cnt++;do{ z=stk[top--];G[cnt].push_back(z);}while(z!=to);
				G[cnt].push_back(x);
			}
				
		}else low[x]=min(low[x],dfn[to]);
	}
}
int main()
{
	n=read();m=read();
	for(RI u,v,i=1;i<=m;i++){
		u=read();v=read();if(u==v)continue;
		add(u,v);add(v,u);
	}for(RI i=1;i<=n;i++)if(!dfn[i])root=i,Tarjan(i);cout<<cnt<<endl;
//	for(RI i=1;i<=n;i++)if(vis[i])printf("%d ",i);
	for(RI i=1;i<=cnt;i++){cout<<G[i].size()<<' ';if(!G[i].size())continue;
		for(RI j=0;j<G[i].size();j++)cout<<G[i][j]<<' ';cout<<endl;
	}
	return 0;
}
`