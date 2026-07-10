---
title: "特别行动队_特别行动队 c++"
published: 2022-07-21
description: ""
tags: ["c语言", "动态规划", "图论"]
category: "dp"
draft: false
---

dpi=dpj+sumti∗(sumfi−sumfj)+s∗(sumfn−sumfj)dp_i =dp_j+sumt_i*(sumf_i-sumf_j)+s*(sumf_n-sumf_j)dpi​=dpj​+sumti​∗(sumfi​−sumfj​)+s∗(sumfn​−sumfj​)

dpi=dpj+sumti∗sumfi−sumti∗sumfj+s∗sumfn−s∗sumfjdp_i =dp_j+sumt_i*sumf_i-sumt_i*sumf_j+s*sumf_n-s*sumf_jdpi​=dpj​+sumti​∗sumfi​−sumti​∗sumfj​+s∗sumfn​−s∗sumfj​

dpi−sumti∗sumfi−s∗sumfn+sumti∗sumfj+s∗sumfj=dpjdp_i -sumt_i*sumf_i-s*sumf_n+sumt_i*sumf_j+s*sumf_j=dp_jdpi​−sumti​∗sumfi​−s∗sumfn​+sumti​∗sumfj​+s∗sumfj​=dpj​

dpi−sumti∗sumfi−s∗sumfn+(sumti+s)∗sumfj=dpjdp_i -sumt_i*sumf_i-s*sumf_n+(sumt_i+s)*sumf_j=dp_jdpi​−sumti​∗sumfi​−s∗sumfn​+(sumti​+s)∗sumfj​=dpj​

dpi−sumti∗sumfi−s∗sumfn=bdp_i -sumt_i*sumf_i-s*sumf_n =bdpi​−sumti​∗sumfi​−s∗sumfn​=b

(sumti+s)=k(sumt_i+s)=k(sumti​+s)=k

sumfj=xsumf_j=xsumfj​=x

dpj=ydp_j=ydpj​=y

(sum[i],dp[i])(sum[i],dp[i])(sum[i],dp[i])

k=dpj−dpisumfj−sumfi{\color{Purple} {\Huge \mathbf{k=\frac{dp_j-dp_i}{sumf_j-sumf_i} {\LARGE } } } }k=sumfj​−sumfi​dpj​−dpi​​

维护前面的是不是需要,直接单调队列维护凸包就好了

`#include<bits/stdc++.h>
#define I inline 
#define LL long long 
#define RI register int 
#define inf 0x3f3f3f3f
#define debug puts("debug")
#define o(x) cout<<x<<' '
#define O(x) cout<<x<<endl
#define ls(x) x<<1
#define rs(x) x<<1|1
#define N 1000100
#define Mod 998244353
using namespace std;
I int read()
{
	RI res=0,f=1;char ch=getchar();
	while(!isdigit(ch)){if(ch=='-')f=-f;ch=getchar();}
	while(isdigit(ch))res=(res<<1)+(res<<3)+(ch&15),ch=getchar();
	return res*f;
}
LL n,sum[N],a,b,c,x[N],f[N],q[N];
LL num[N]; 
int head=1,tail=1;
int main()
{
	n=read();a=read();b=read();c=read();
	for(RI i=1;i<=n;i++)x[i]=read(),sum[i]=sum[i-1]+x[i],num[i]=a*sum[i]*sum[i]-b*sum[i];
	for(RI i=1;i<=n;i++){
		while(head < tail && 
		( f[q[head+1]]-
		f[q[head]] + 
		num[q[head+1]] - 
		num[q[head]]) 
		>= 
		((sum[q[head+1]]-
		sum[q[head]])*2*a*sum[i]) 
		)head++;

	f[i]=
		f[q[head]]+
		num[q[head]]-
		2*a*sum[i]*
		sum[q[head]]+
		a*sum[i]*sum[i]+
		b*sum[i]+c;
		
		while(head < tail &&  (f[i] - f[q[tail]] + num[i] - num[q[tail]])*(sum[q[tail]]-sum[q[tail-1]]) 
		>= (f[q[tail]] - f[q[tail-1]] + num[q[tail]] - num[q[tail-1]])*(sum[i]-sum[q[tail]]) )

		tail--;q[++tail]=i; 
	
	}
	printf("%lld",f[n]);return 0;
}
`