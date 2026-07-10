---
title: "[NOI2001] 食物链"
published: 2026-01-21
description: ""
tags: ["算法", "c++", "c语言"]
category: "当前文章被以下社区和专栏收录："
draft: false
---

- 


动物王国中有三类动物 A,B,CA,B,CA,B,C，这三类动物的食物链构成了有趣的环形。AAA 吃 BBB，BBB 吃 CCC，CCC 吃 AAA。

现有 NNN 个动物，以 1∼N1 \sim N1∼N 编号。每个动物都是 A,B,CA,B,CA,B,C 中的一种，但是我们并不知道它到底是哪一种。

有人用两种说法对这 NNN 个动物所构成的食物链关系进行描述：

第一种说法是 `1 X Y`，表示 XXX 和 YYY 是同类。
- 第二种说法是 `2 X Y`，表示 XXX 吃 YYY。

此人对 NNN 个动物，用上述两种说法，一句接一句地说出 KKK 句话，这 KKK 句话有的是真的，有的是假的。当一句话满足下列三条之一时，这句话就是假话，否则就是真话。

- 当前的话与前面的某些真的话冲突，就是假话；
- 当前的话中 XXX 或 YYY 比 NNN 大，就是假话；
- 当前的话表示 XXX 吃 XXX，就是假话。

你的任务是根据给定的 NNN 和 KKK 句话，输出假话的总数。


第一行两个整数，N,KN,KN,K，表示有 NNN 个动物，KKK 句话。

第二行开始每行一句话。格式见题目描述与样例。


一行，一个整数，表示假话的总数。


`100 7
1 101 1
2 1 2
2 2 3
2 3 3
1 1 3
2 3 1
1 5 5

`


`3

`


对于全部数据，1≤N≤5×1041\le N\le 5 \times 10^41≤N≤5×104，1≤K≤1051\le K \le 10^51≤K≤105。

![]\(https://i-blog.csdnimg.cn/direct/ffdab4ee181d4a398175342670522ed6.jpeg)

`#include<iostream>
#include<cstdio> 
#define N 50010
using namespace std;

int fa[N*3],n,m;
int ans;
int getfa(int x){
	if(fa[x]==x)return x;
	return fa[x]=getfa(fa[x]);
}
 
int main()
{
	scanf("%d%d",&n,&m);
	for(int i=1;i<=n*3;i++)fa[i]=i;
	while(m--)
	{
		int op,a,b;
		scanf("%d%d%d",&op,&a,&b);
		if(a>n||b>n){ans++;continue;}
		if(op==1)
		{
			if(getfa(a)!=getfa(b+n)&&getfa(a)!=getfa(b+2*n))
			{
				fa[getfa(a)]=getfa(b);
				fa[getfa(a+2*n)]=getfa(b+2*n);
				fa[getfa(a+n)]=getfa(b+n);
			}
			else ans++;
		}
		else
		{
			if(getfa(a)!=getfa(b)&&getfa(a)!=getfa(b+2*n))
			{
				fa[getfa(a)]=getfa(b+n);
				fa[getfa(a+2*n)]=getfa(b);
				fa[getfa(a+n)]=getfa(b+n*2);
			}
			else ans++;
		}
	}
	printf("%d",ans);return 0;
}
`
![]\(https://i-blog.csdnimg.cn/direct/a70b2b928f3442929e74b4893cabc2cd.jpeg)

`#include<bits/stdc++.h>
using namespace std;
const int maxn = 5e4 + 233;
int fa[maxn], d[maxn];
int ff(int x)
{
    if(fa[x] == x) return x;
    int r = ff(fa[x]);
    d[x] += d[fa[x]];
    return fa[x] = r;
}
int main()
{
    int n,k; cin >> n >> k;
    for(int i = 0; i <= n; i++) fa[i] = i;
    int ans = 0;
    for(int i = 1; i <= k; i++)
    {
        int t, a, b;
        scanf("%d%d%d", &t, &a, &b);
        if(a > n || b > n) {ans ++; continue;}
        else if(t == 2 && a == b) {ans++; continue;}
        else
        {
            int rel;
            if(t == 2) rel = 1;
            else rel = 0;
            int x = ff(a), y = ff(b);
            if(x == y) 
            {
                if((((d[a] - d[b]) % 3) + 3) % 3 != rel)
                ans++;
            }
            else
            {
                fa[x] = y;
                d[x] = d[b] - (d[a] - rel);
            }
        }
    }
    cout<< ans;
}
 
`