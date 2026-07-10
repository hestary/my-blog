---
title: "树链剖分（树剖）"
published: 2021-08-13
description: ""
tags: ["数据结构", "算法"]
category: "算法进阶—进阶指南"
draft: false
---

- 

## 

### 

树链剖分，指一种对树进行划分的算法，它先通过轻重边剖分将树分为多条链，保证每个点属于且只属于一条链，然后再通过数据结构（树状数组、BST、SPLAY、线段树等）来维护每一条链。

---

### 

LCA[学习资料](https://blog.csdn.net/yhhy666/article/details/118518817)
- 树形DP
- 树的遍历
- 线段树
- 链式前向星

---

### 

- 将树从

         x

        x

     x到y结点最短路径上所有节点的值都加上

         z

        z

     z
- 求树从

         x

        x

     x到

         y

        y

     y结点最短路径上所有节点的值之和(最大值/最小值/…)
- 将以

         x

        x

     x为根节点的子树内所有节点值都加上

         z

        z

     z
- 求以

         x

        x

     x为根节点的子树内所有节点值之和

---

### 

- 重儿子：对于每一个非叶子节点，它的儿子中结点数最多的儿子
- 轻儿子：对于每一个非叶子节点，它的儿子中 非重儿子 的剩下所有儿子即为轻儿子
 **叶子节点没有重儿子也没有轻儿子**
- 重边：一个父亲连接他的重儿子的边称为重边
- 轻边：剩下的即为轻边
- 重链：相邻重边连起来的 连接一条重儿子 的链叫重链
 对于叶子节点，若其为轻儿子，则有一条以自己为起点的长度为1的链
 每一条重链以轻儿子为起点

上面讲的可能有一点抽象
 ![]\(https://i-blog.csdnimg.cn/blog_migrate/f6d1efab1e73fa5aa54e28f626144fd6.png)
 可以通过这张图看清楚定义

### 

将一条路径

        (

        u

        ,

        v

        )

       (u,v)

    (u,v)拆分为若干条重路径的过程,实际上就是.个寻找最近公共祖先的过程。 考
 虑“暴力”的做法,我们会选择u,v中深度较大的点向上走一步,直到

        u

        =

        v

       u=v

    u=v。现在有了重路径，由于
 我们记录了重路径的顶部结点top[x],还记录了每个点在序列中的位置,因此我们不需要一步步
 走。假定

        t

        o

        p

        [

        u

        ]

       top[u]

    top[u]和

        t

        o

        p

        [

        v

        ]

       top[v]

    top[v]不同，那么它们的最近公共祖先可能在其中一条的重路径上，也可能在
 其他的重路径上，因为LCA显然不可能在top深度较大的那条重路径上，所以我们先处理top深度
 较大的。首先我们找出

        u

        ,

        v

       u,v

    u,v中

        t

        o

        p

       top

    top深度较大的点,假设是u,则可以直接跳到

        a

        [

        t

        o

        p

        [

        u

        ]

        ]

       a[ top[u]]

    a[top[u]]处,且跳过
 的这一-段,在线段树中是一段区间，若我们按照深度从小到大来存储点，则这段区间为:

        [

        s

         e

         [

        o

        p

        [

        x

        ]

        ]

        ,

        s

        e

        g

        [

        x

        ]

        ]

       [se_[op [x]],seg[x]]

    [se[​op[x]],seg[x]]。当

        u

        ,

        V

       u,V

    u,V的top相同时，说明它们走到了同一条重路径上，这时它们之间的路径也是
 序列上的一段区间,且u,v中深度较小的那点是原路径的

        L

        C

        A

       LCA

    LCA。
 这样我们就可以将给出的任意路径拆 分成若干条重路径，也就是若干个区间，并用线段树等
 数据结构处理操作。
 当我们要处理任意两点间路径时：

**设所在链顶端的深度更深的那个点为

         x

        x

     x点：**

        a

        n

        s

       ans

    ans加上

        x

       x

    x点到

        x

       x

    x所在链顶端 这一段区间的点权和
 把

        x

       x

    x跳到

        x

       x

    x所在链顶端的那个点的上面一个点
 不停执行这两个步骤，直到两个点处于一条链上，这时再加上此时两个点的区间和即可
 ![]\(https://i-blog.csdnimg.cn/blog_migrate/6163b5e1817ac5818927d9e0d5bc08fa.png)

#### 

在做之前我们可以要维护这7个数组

- 标记每个点的深度 

         d

         e

         p

         [

         i

         ]

        dep[i]

     dep[i]
- 标记每个点的父亲 

         f

         a

         [

         i

         ]

        fa[i]

     fa[i]
- 标记每个非叶子节点的子树大小(含它自己) 

         s

         i

         z

         e

         [

         i

         ]

        size[i]

     size[i]
- 标记每个非叶子节点的重儿子编号 

         s

         o

         n

         [

         i

         ]

        son[i]

     son[i]
- 标记每个点的新编号 

         i

         d

         [

         x

         ]

        id[x]

     id[x]
- 赋值每个点的初始值到新编号上 

         a

         [

         i

         ]

        a[i]

     a[i]
- 处理每个点所在链的顶端 

         t

         o

         p

         [

         i

         ]

        top[i]

     top[i]

#### 

`I void dfs1(int x,int father)
{
	deep[x]=deep[father]+1;//更新深度
	fa[x]=father;
	size[x]=1;
	int maxson=-1;
	for(RI i=head[x];i;i=edge[i].next)
	{
		int to=edge[i].to;
		if(to==father)continue;
		dfs1(to,x);
		size[x]+=size[to];//加上子树的大小
		if(size[to]>maxson)maxson=size[to],son[x]=to;//统计重儿子
	}
}
` 

#### 
 
注意在进行重新编号的时候先访问重链
 这样可以保证重链内的节点编号连续
 然后在最后搞的时候可以方便很多

`I void dfs2(int x,int tp)
{
	top[x]=tp;//重链的顶端
	id[x]=++cnt;//更新新的编号
	a[cnt]=val[x]; //把这个的值映射到线段树里面
	if(!son[x])return;
	dfs2(son[x],tp);//找重儿子
	for(RI i=head[x];i;i=edge[i].next)
	{
		int to=edge[i].to;
		if(to==fa[x]||to==son[x])continue;
		dfs2(to,to);
	}
}
` 

#### 
 
`I LL ask(int x,int y)
{
	LL ans=0;
	while(top[x]!=top[y])//没有在一条链上面
	{
		int fx=top[x],fy=top[y];
		if(deep[fx]<deep[fy])swap(fx,fy),swap(x,y);
		ans=(ans+getsum(id[fx],id[x],1))%mod;//从深度大的开始跳，跳的时候加
		x=fa[fx];
	}
	if(deep[x]>deep[y])swap(x,y);
	ans=(ans+getsum(id[x],id[y],1))%mod;//最后计算两个在同一条链上的值
	return ans;
}
` 

#### 
 
树链剖分修改区间的时候不能直接改，要边跳边改，因为这一段区间是有可能不连在一起的，一定要在跳的时候加上线段树的区间修改（我在这坑了一下午）
 
`I void up(int x,int y,LL k)
{
	while(top[x]!=top[y])
	{
		int fx=top[x],fy=top[y];
		if(deep[fx]<deep[fy])swap(fx,fy),swap(x,y);
		change(id[fx],id[x],k,1);
		x=fa[fx];
	}
	if(deep[x]>deep[y])swap(x,y);
	change(id[x],id[y],k,1);
	return ;
}
` 

### 
 
`#include<bits/stdc++.h>
#define ls(x) x<<1
#define rs(x) x<<1|1
#define maxn 100010
#define I inline
#define LL long long
#define RI register int 
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch)){res=(res<<1)+(res<<3)+(ch&15);ch=getchar();}
	return res*f;
}
struct Tree{
	int l,r;
	LL sum;
}tree[maxn*4];
LL lazy[maxn*4];
int tot,head[maxn];
LL mod;int n,m,root,op;
struct node{
	int to,next;
}edge[maxn*2];
I void add(int x,int y)
{
	edge[++tot].to=y;
	edge[tot].next=head[x];
	head[x]=tot;
}
LL a[maxn],val[maxn];
int cnt,fa[maxn],son[maxn],deep[maxn],top[maxn],id[maxn],size[maxn];
I void build(int l,int r,int id)
{
	tree[id].l=l;tree[id].r=r;
	if(l==r){tree[id].sum=a[l];return;}
	int mid=(l+r)>>1;
	build(l,mid,ls(id));
	build(mid+1,r,rs(id));
	tree[id].sum=(tree[ls(id)].sum+tree[rs(id)].sum)%mod;
	return ;
}
I void pushdown(int id)
{
	if(!lazy[id])return ;
	tree[ls(id)].sum=(tree[ls(id)].sum+(tree[ls(id)].r-tree[ls(id)].l+1)*lazy[id])%mod;
	tree[rs(id)].sum=(tree[rs(id)].sum+(tree[rs(id)].r-tree[rs(id)].l+1)*lazy[id])%mod;
	lazy[ls(id)]=(lazy[ls(id)]+lazy[id])%mod;
	lazy[rs(id)]=(lazy[rs(id)]+lazy[id])%mod;
	lazy[id]=0;
	return ;
}
I void change(int l,int r,LL k,int id)
{
	if(tree[id].l>=l&&tree[id].r<=r)
	{
		lazy[id]=(lazy[id]+k)%mod;
		tree[id].sum=(tree[id].sum+(tree[id].r-tree[id].l+1)*k)%mod;
		return ;
	}
	pushdown(id);
	if(tree[ls(id)].r>=l)change(l,r,k,ls(id));
	if(tree[rs(id)].l<=r)change(l,r,k,rs(id));
	tree[id].sum=(tree[ls(id)].sum+tree[rs(id)].sum)%mod;
	return ;
}
I LL getsum(int l,int r,int id)
{
	if(tree[id].l>=l&&tree[id].r<=r)return tree[id].sum%mod;
	LL ans=0;
	pushdown(id);
	if(tree[ls(id)].r>=l)ans=(ans+getsum(l,r,ls(id)))%mod;
	if(tree[rs(id)].l<=r)ans=(ans+getsum(l,r,rs(id)))%mod;
	return ans;
}
I void dfs1(int x,int father)
{
	deep[x]=deep[father]+1;
	fa[x]=father;
	size[x]=1;
	int maxson=-1;
	for(RI i=head[x];i;i=edge[i].next)
	{
		int to=edge[i].to;
		if(to==father)continue;
		dfs1(to,x);
		size[x]+=size[to];
		if(size[to]>maxson)maxson=size[to],son[x]=to;
	}
}
I void dfs2(int x,int tp)
{
	top[x]=tp;
	id[x]=++cnt;
	a[cnt]=val[x]; 
	if(!son[x])return;
	dfs2(son[x],tp);
	for(RI i=head[x];i;i=edge[i].next)
	{
		int to=edge[i].to;
		if(to==fa[x]||to==son[x])continue;
		dfs2(to,to);
	}
}
I LL ask(int x,int y)
{
	LL ans=0;
	while(top[x]!=top[y])
	{
		int fx=top[x],fy=top[y];
		if(deep[fx]<deep[fy])swap(fx,fy),swap(x,y);
		ans=(ans+getsum(id[fx],id[x],1))%mod;
		x=fa[fx];
	}
	if(deep[x]>deep[y])swap(x,y);
	ans=(ans+getsum(id[x],id[y],1))%mod;
	return ans;
}
I void up(int x,int y,LL k)
{
	while(top[x]!=top[y])
	{
		int fx=top[x],fy=top[y];
		if(deep[fx]<deep[fy])swap(fx,fy),swap(x,y);
		change(id[fx],id[x],k,1);
		x=fa[fx];
	}
	if(deep[x]>deep[y])swap(x,y);
	change(id[x],id[y],k,1);
	return ;
}
int main()
{
    n=read();m=read();root=read();scanf("%lld",&mod);
	for(RI i=1;i<=n;i++)scanf("%lld",&val[i]);
	for(RI i=1;i<n;i++)
	{
		int u,v;u=read();v=read();
		add(u,v);add(v,u);
	}
	dfs1(root,0);
	dfs2(root,root);
	build(1,n,1);
	while(m--)
	{
		op=read();
		if(op==1)
		{
			int x,y;LL z;
		   x=read();y=read();scanf("%lld",&z);
		   z%=mod;
		    up(x,y,z);	
		}
		else
		{
			if(op==2)
			{
				int x,y;
				x=read();y=read();
				printf("%lld\n",ask(x,y));
			}
			else
			{
				if(op==3)
				{
					int x;
					x=read();
					LL z;
					scanf("%lld",&z);
					z%=mod;
					change(id[x],size[x]+id[x]-1,z,1);
				}
				else
				{
					int x;x=read();
					printf("%lld\n",getsum(id[x],id[x]+size[x]-1,1));
				}
			}
		}
	}
	return 0;
}
/*
8 10 2 448348

458 718 447 857 633 264 238 944 

1 2
2 3
3 4
6 2
1 5
5 7
8 6
3 7 611
4 6
3 1 267
3 2 111
1 6 3 153
3 7 673
4 8
2 6 1
4 7
3 4 228
*/

`