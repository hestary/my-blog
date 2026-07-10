---
title: "算法竞赛题解精选"
published: 2020-08-27
description: ""
tags: ["图论", "dfs"]
category: "比赛"
draft: false
---

### 

在这里插入图片描述![]\(https://i-blog.csdnimg.cn/blog_migrate/3ef92eeebe20400e92dc9ba1a96339b2.png#pic_center)![]\(https://i-blog.csdnimg.cn/blog_migrate/2fdf942aa1ae3e279d1cf4cca2b57934.png#pic_center)![]\(https://i-blog.csdnimg.cn/blog_migrate/7878a1e087cb8e533638833f7eefa3dc.png#pic_center)

**这一题只需要判断一下，倍数是2的个数，倍数是4的个数。两个倍数是二的可以带两个数，一个倍数是`在这里插入代码片`四的，可以带两数走**

`#include<bits/stdc++.h>
#define maxn 15000
using namespace std;
int ans1,ans2,ans3;
int T,n,a[maxn];
int main()
{
    cin>>T;
    while(T--)
    {
        cin>>n;
        ans1=ans2=ans3=0;
        for(int i=1;i<=n;i++)
        {
            cin>>a[i];
            if(a[i]%4==0)ans2++;
            else if(a[i]%2==0)ans1++;
            else ans3++;
        }
        if((ans1/2+ans2*2>=n-1)||(ans2-ans3>=0)||(ans3==ans2+1&&!ans1))cout<<"AWaDa!"<<endl;
        else cout<<"AKTang!"<<endl;
    }
    return 0;
}

`

---

### 

![]\(https://i-blog.csdnimg.cn/blog_migrate/ac92868634b5820a4af05fce181d549a.png#pic_center)

`#include<bits/stdc++.h>
#define maxn 150000
using namespace std;
int a[maxn],n,m,tep;
int main()
{
    cin>>n;tep=n;
    for(int i=1;i<=n;i++)cin>>a[i];
    cin>>m;
    for(int i=1;i<=m;i++)
    {
        int x;cin>>x;
        if(x==1)
        {
            int k;cin>>k;
            int j=a[1];
            for(int i=2;i<=tep+1;i++)//前面
            {
            int q=a[i];
            a[i]=j;
            j=q;
            }
            tep++;
            a[1]=k;
        }
        else if(x==2)后面
        {
            int k;cin>>k;
            a[++tep]=k;
        }
        else for(int i=1;i<=tep/2;i++)swap(a[i],a[tep-i+1]);turn
    }
    for(int i=1;i<=tep;i++)cout<<a[i]<<' ';
    return 0;
}

`

---

### 

![]\(https://i-blog.csdnimg.cn/blog_migrate/79631f00d1b51992881e5b32bfbda9e9.png#pic_center)

**先对数据进行预处理，计算出每个老虎到第一个老虎的距离，然后再枚举起点，分两类讨论向左还是向右，发现老虎加的攻击值=起点走到上一个老虎的距离，所以打这个老虎就是两个点的距离**

`#include<bits/stdc++.h>
#define maxn 150
using namespace std;
int dp[maxn][maxn];
int n,ans,a[maxn],dis[maxn],k=1e6;
int main()
{
    cin>>n;
    for(int i=1;i<=n;i++)cin>>a[i],ans+=a[i];
    dis[1]=0;
    for(int i=1;i<n;i++)cin>>a[i],dis[i+1]+=a[i]+dis[i];
    for(int i=1;i<=n;i++)
    {
        int neww=0;
        for(int j=i-1;j>=1;j--)neww+=dis[i]-dis[j];//往左先
        for(int j=i+1;j<=n;j++)neww+=dis[i]+dis[j];
        k=min(k,neww);
         
        neww=0;
        for(int j=i+1;j<=n;j++)neww+=dis[j]-dis[i];//往右先
        for(int j=i-1;j>=1;j--)neww+=2*dis[n]-dis[i]-dis[j];
        k=min(k,neww);
    }
    cout<<ans+k;
    return 0;
}

`

---

### 

**暴力dfs开始的人，在dfs下个人，方案数每次++**

`#include<bits/stdc++.h>
#define maxn 150000
#define mo   998244353
using namespace std;
int a[maxn],tot,head[maxn],vis[maxn];
map<int,int>q[maxn];
int n,m,ans;
struct node
{
    int next;
    int to;
}edge[maxn];
void add(int u,int v)
{
    ++tot;
    edge[tot].next=head[u];
    edge[tot].to=v;
    head[u]=tot;
}
void dfs(int x,int tep)
{
    ans++;ans%=mo;//方案数加加
    for(int i=head[x];i;i=edge[i].next)dfs(edge[i].to,tep+1);//下个人
}
int main()
{
    cin>>n>>m;
    for(int i=1;i<=m;i++)
    {
        int x,y;cin>>x>>y;
        if(!q[x][y])
        {
            q[x][y]=1;
            add(x,y);
        }
         
    }
    for(int i=1;i<=n;i++)dfs(i,1);
    cout<<ans;
    return 0;
}

`