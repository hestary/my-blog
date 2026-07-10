---
title: "KMP算法详解：字符串匹配的高效实践与应用"
published: 2021-08-24
description: ""
tags: ["算法", "数据结构"]
category: "算法进阶—进阶指南"
draft: false
---

### 

[1](https://www.zhihu.com/question/21923021/answer/1032665486)
 [2](https://www.luogu.com.cn/problem/solution/P3375)

### 
 
** 
 
KMP算法是一种改进的字符串匹配算法，由D.E.Knuth，J.H.Morris和V.R.Pratt提出的，因此人们称它为克努特—莫里斯—普拉特操作（简称KMP算法）。KMP算法的核心是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。具体实现就是通过一个next()函数实现，函数本身包含了模式串的局部匹配信息。KMP算法的时间复杂度O(m+n)

模式串匹配，就是给定一个需要处理的文本串（理论上应该很长）和一个需要在文本串中搜索的模式串（理论上长度应该远小于文本串），查询在该文本串中，给出的模式串的出现有无、次数、位置等。

模式串匹配的意义在于，如果我是一个平台的管理员，我可以针对一篇文章或者一句话，搜索其中某个特定脏字或者不雅词汇的出现次数、位置——次数可以帮助我决定采取何种等级对于该用户的惩罚方式，而位置则可以帮助我给每一个脏词打上“*”的标记来自动屏蔽这些脏词。

### 

[模板题目](https://www.luogu.com.cn/problem/P3375)

### 

所谓字符串匹配，是这样一种问题：“字符串 P 是否为字符串 S 的子串？如果是，它出现在 S 的哪些位置？” 其中 S 称为主串；P 称为模式串。下面的图片展示了一个例子。![]\(https://i-blog.csdnimg.cn/blog_migrate/7fbf71fc1897e99c69b4cd9866077e36.png)

        “

        n

        o

        ”

       “no”

    “no” 这个模式串的匹配结果是“出现了一次，从

        S

        [

        6

        ]

       S[6]

    S[6]开始”；

        “

        o

        b

        ”

       “ob”

    “ob”这个模式串的匹配结果是“出现了两次，分别从

        s

        [

        1

        ]

       s[1]

    s[1]、

        s

        [

        10

        ]

       s[10]

    s[10]开始”。按惯例，主串和模式串都以

        0

       0

    0开始编号。

KMP 的精髓在于，对于每次失配之后，我都不会从头重新开始枚举，而是根据我已经得知的数据，从某个特定的位置开始匹配；而对于模式串的每一位，都有唯一的“特定变化位置”，这个在失配之后的特定变化位置可以帮助我们利用已有的数据不用从头匹配，从而节约时间。

那么现在已经很明了了， KMPKMP 的重头戏就在于用失配数组来确定当某一位失配时，我们可以将前一位跳跃到之前匹配过的某一位。而此处有几个先决条件需要理解：

1、我们的失配数组应当建立在模式串意义下，而不是文本串意义下**。因为显然模式串要更加灵活，在失配后换位时，更灵活简便地处理。

**2、如何确定位置呢？**

首先我们要明白，基于先决条件11而言，我们在预处理时应当考虑当模式串的第 ii 位失配时，应当跳转到哪里.因为在文本串中，之前匹配过的所有字符已经没有用了——都是匹配完成或者已经失配的，所以我们的 

        K

        M

        P

       KMP

    KMP 数组（即是用于确定失配后变化位置的数组，下同）应当记录的是：

在模式串 

        s

        t

        r

        1

       str1

    str1 中，对于每一位 

        s

        t

        r

        1

        (

        i

        )

       str1(i)

    str1(i) ,它的 

        k

        m

        p

       kmp

    kmp 数组应当是记录一个位置 

        j

       j

    j ,

        j

        ≤

        i

       j\leq i

    j≤i 并且满足

        s

        t

        r

        1

        (

        i

        )

        =

        s

        t

        r

        1

        (

        j

        )

       str1(i)=str1(j)

    str1(i)=str1(j) 并且在 

        j

        !

        =

        1

       j!=1

    j!=1 时理应满足$ str1(1)$ 至

        s

        t

        r

        1

        (

        j

        −

        1

        )

       str1(j-1)

    str1(j−1) 分别与 

        s

        t

        r

        (

        i

        −

        j

        +

        1

        )

        s

        t

        r

        1

        (

        i

        −

        1

        )

       str(i−j+1)~str1(i-1)

    str(i−j+1) str1(i−1) 按位相等

### 
 
`#include<bits/stdc++.h>
#define I inline
#define RI register int 
#define maxn 1000100
using namespace std;
string s1,s2;
int kmp[maxn];
int len1,len2;
int main()
{
	cin>>s1>>s2;
	len1=s1.size();len2=s2.size();
	for(RI i=len1;i>=1;i--)s1[i]=s1[i-1];
	for(RI i=len2;i>=1;i--)s2[i]=s2[i-1];
	
	int j=0;
	for(RI i=2;i<=len2;i++)
	{
		while(j&&s2[i]!=s2[j+1])j=kmp[j];
		if(s2[i]==s2[j+1])j++;
		kmp[i]=j;
	}
	j=0;
	for(RI i=1;i<=len1;i++)
	{
		while(j&&s1[i]!=s2[j+1])j=kmp[j];
		if(s1[i]==s2[j+1])j++;
		if(j==len2){
			cout<<i-len2+1<<endl;
			j=kmp[j];
		}
	}
	for(RI i=1;i<=len2;i++)cout<<kmp[i]<<' ';
	return 0;
}
`