---
title: "笛卡尔树(Cartesian Tree)"
published: 2021-11-16
description: ""
tags: ["算法", "c++", "线性代数"]
category: "算法进阶—进阶指南"
draft: false
---

- 

#### 

[性质](#_2)
- [建树](#_9)
- [Code](#Code_17)

## 

- 有两个关键字

         (

         x

         ,

         y

         )

        (x,y)

     (x,y)组成
- 如果只看第一个关键字x的时候它满足二叉搜索树（二叉查找树的性质）即：中序遍历为原来的序列，并且

         i

          d

           l

           s

         <

         i

          d

          x

         <

         i

          d

           r

           s

        id_{ls}<id_x<id_{rs}

     idls​<idx​<idrs​
- 如果看第二个关键字的话它满足小根堆的性质。即：节点的权值

         v

         a

         l

        val

     val，大于两个儿子的
- 任意两个点的LCA的权值就是它们之间的RMQ

## 

对于我们要满足二叉搜索树的性质的时候，我们肯定按顺序加入数字，并且每次加入的时候往最右边加入，这样肯定能实现对二叉搜索树的条件

然后再进行分类讨论
 1.再右边找不到比这个点更大的权值，那么就把这个点作为根，原来的根节点作为这个点的左边节点
 ![]\(https://i-blog.csdnimg.cn/blog_migrate/18fd128563181984d09d9a9416bcdb8a.png)
 2.找到了这个点，那么就把这个点的右儿子移到新加入的这个点的左儿子上
 ![]\(https://i-blog.csdnimg.cn/blog_migrate/d174a1e76a28febef12373462d707458.png)

## 
 
`I void build(){
	Stack[++top]=1;
	for(RI i=2;i<=n;i++){
		while(top&&A[Stack[top]]>A[i])top--;
		if(!top)L[i]=Stack[top+1];
		else L[i]=R[Stack[top]],R[Stack[top]]=i;
		Stack[++top]=i;
	} 
}
`