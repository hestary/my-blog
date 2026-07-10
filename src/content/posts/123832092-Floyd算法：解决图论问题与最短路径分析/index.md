---
title: "Floyd算法：解决图论问题与最短路径分析"
published: 2022-04-26
description: ""
tags: ["c++", "dp"]
category: "算法进阶—进阶指南"
draft: false
---


`//#include<bits/stdc++.h>   
//#define mod 998244353
//#define LL long long 
//#define I inline
//#define RI register int
//#define debug cout << "debug"<<endl
//#define O(x) cout<< #x <<' '<<x<<endl
//#define o(x) cout<< #x <<' '<<x<<' '; 
//#define inf 0x3f3f3f3f
//#define N 35
//#define M 650
//using namespace std;
//I int read()
//{
//	RI res=0,f=1;char ch=getchar();
//	while(!isdigit(ch))if(ch=='-')f=-f,ch=getchar();else ch=getchar();
//	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
//	return res*f;
//}
//int n,m;
//int a[N][N];
//char u,v,wh;
//I int gtc(char x){return x-'A'+1;}
//int du[N],ans[N],vis[N];
//queue<int >Q;
//I void topu(int x){
//	memset(du,0,sizeof du);memset(vis,0,sizeof vis);
//	for(RI i=1;i<=n;i++){
//		for(RI j=1;j<=n;j++){
//			if(a[i][j])du[j]++;
//		}
//	}while(!Q.empty())Q.pop();
//	int first=0;
//	for(RI i=1;i<=n;i++)if(!du[i]){first=i;break;}
//	int tep=0;vis[first]=1;
//	Q.push(first);while(!Q.empty()){
//		int k=Q.front();Q.pop();int anss=0;
//		ans[++tep]=k;for(RI i=1;i<=n;i++){
//			if(a[k][i]==1&&!vis[i]){
//				du[i]--;if(!du[i])Q.push(i),vis[i]=1,anss++;
//			}
//		}
//		if(anss>=2)return ;
//	}
//	if(tep==n){
//		printf("Sorted sequence determined after %d relations: ",x);
//		for(RI i=1;i<=n;i++)printf("%c",(char)(ans[i]+'A'-1));
//		printf(".");exit(0);
//	}
//}
//I void Floyd(int x){
//	for(RI k=1;k<=n;k++){
//		for(RI i=1;i<=n;i++){
//			for(RI j=1;j<=n;j++){
//				if(a[i][k]&&a[k][j])a[i][j]=1;
//			}
//		}
//	}
//	for(RI i=1;i<=n;i++){
//		for(RI j=1;j<=n;j++){
//			if(a[i][j]&&a[j][i]){
//				printf("Inconsistency found after %d relations.",x);
//				exit(0);
//			}
//		}
//	}
//	topu(x);return;
//}
//int main()
//{
//	n=read();m=read();for(RI i=1;i<=m;i++){
////		scanf("%c%c%c",&u,&wh,&v);
//        cin>>u>>wh>>v; 
//		if(wh=='<')a[gtc(u)][gtc(v)]=1;
//		else a[gtc(v)][gtc(u)]=1;
//		Floyd(i);
//	}puts("Sorted sequence cannot be determined.");
//	return 0;
//}
#include<bits/stdc++.h>
#define qw first
#define er second
using namespace std;
const int N=200;
int n,c[N];
double x[N],y[N],w[N][N],d[N][N],mxd[N],cz[N],mx=1e9;
bool a[N][N],v[N];
vector<int>c2[N];
priority_queue<pair<double,int> >q;
pair<double,int>e;
void dfs(int x,int col){
	if(v[x]) return;
	v[x]=1;c[x]=col;
	c2[col].push_back(x);
	for(int i=1;i<=n;i++)
		if(a[x][i])
			dfs(i,col);
}
void Dijkstra(int s){
	memset(v,0,sizeof(v));
	d[s][s]=e.qw=0;e.er=s;
	q.push(e);
	while(q.size()){
		int x=q.top().er;
		q.pop();
		if(v[x])
			continue;
		v[x]=1;
		for(int i=1;i<=n;i++){
			if(!a[x][i])
				continue;
			if(d[s][i]>d[s][x]+w[x][i]){
				d[s][i]=d[s][x]+w[x][i];
				e.qw=-d[s][i];e.er=i;
				q.push(e);
			}
		}
	}
}
int main()
{
    cin>>n;
    for(int i=1;i<=n;i++)
    	for(int j=1;j<=n;j++)
    		d[i][j]=1e7;
    for(int i=1;i<=n;i++)
    	cin>>x[i]>>y[i];
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			scanf("%1d",&a[i][j]);
			w[i][j]=sqrt((x[i]-x[j])*(x[i]-x[j])+(y[i]-y[j])*(y[i]-y[j]));
		}
	}
	for(int i=1;i<=n;i++)
		Dijkstra(i);
	memset(v,0,sizeof(v));
	for(int i=1,col=1;i<=n;i++){
		if(v[i]) continue;
		dfs(i,col);
		for(int j=0;j<c2[col].size();j++){
			for(int k=0;k<c2[col].size();k++){
				if(j==k||d[c2[col][j]][c2[col][k]]==1e7) continue;
				mxd[c2[col][j]]=max(mxd[c2[col][j]],d[c2[col][j]][c2[col][k]]);
			}
			cz[col]=max(cz[col],mxd[c2[col][j]]);
		}
		col++;
	}
	for(int i=1;i<=n;i++)
		for(int j=1;j<=n;j++){
			if(c[i]==c[j]) continue;
			mx=min(mx,max(cz[c[i]],max(cz[c[j]],mxd[i]+w[i][j]+mxd[j])));
		}
	printf("%.6lf",mx);
	return 0;
}
`


`#include<bits/stdc++.h>   
#define mod 998244353
#define LL long long 
#define I inline
#define RI register int
#define debug cout << "debug"<<endl
#define O(x) cout<< #x <<' '<<x<<endl
#define o(x) cout<< #x <<' '<<x<<' '; 
#define inf 0x3f3f3f3f
#define N 35
#define M 650
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch))if(ch=='-')f=-f,ch=getchar();else ch=getchar();
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
int n,m;
int a[N][N];
char u,v,wh;
I int gtc(char x){return x-'A'+1;}
int du[N],ans[N],vis[N];
queue<int >Q;
I void topu(int x){
	memset(du,0,sizeof du);memset(vis,0,sizeof vis);
	for(RI i=1;i<=n;i++){
		for(RI j=1;j<=n;j++){
			if(a[i][j])du[j]++;
		}
	}while(!Q.empty())Q.pop();
	int first=0;
	for(RI i=1;i<=n;i++)if(!du[i]){first=i;break;}
	int tep=0;vis[first]=1;
	Q.push(first);while(!Q.empty()){
		int k=Q.front();Q.pop();int anss=0;
		ans[++tep]=k;for(RI i=1;i<=n;i++){
			if(a[k][i]==1&&!vis[i]){
				du[i]--;if(!du[i])Q.push(i),vis[i]=1,anss++;
			}
		}
		if(anss>=2)return ;
	}
	if(tep==n){
		printf("Sorted sequence determined after %d relations: ",x);
		for(RI i=1;i<=n;i++)printf("%c",(char)(ans[i]+'A'-1));
		printf(".");exit(0);
	}
}
I void Floyd(int x){
	for(RI k=1;k<=n;k++){
		for(RI i=1;i<=n;i++){
			for(RI j=1;j<=n;j++){
				if(a[i][k]&&a[k][j])a[i][j]=1;
			}
		}
	}
	for(RI i=1;i<=n;i++){
		for(RI j=1;j<=n;j++){
			if(a[i][j]&&a[j][i]){
				printf("Inconsistency found after %d relations.",x);
				exit(0);
			}
		}
	}
	topu(x);return;
}
int main()
{
	n=read();m=read();for(RI i=1;i<=m;i++){
//		scanf("%c%c%c",&u,&wh,&v);
        cin>>u>>wh>>v; 
		if(wh=='<')a[gtc(u)][gtc(v)]=1;
		else a[gtc(v)][gtc(u)]=1;
		Floyd(i);
	}puts("Sorted sequence cannot be determined.");
	return 0;
}
`


求从起点 S 到终点 E 恰好经过 N 条边（可以重复经过）的最短路。

![]\(https://i-blog.csdnimg.cn/blog_migrate/4393f701505551f1a3fdb014b55696ee.png)