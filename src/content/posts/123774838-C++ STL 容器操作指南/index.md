---
title: "C++ STL 容器操作指南"
published: 2022-03-27
description: ""
tags: ["STL"]
category: "算法进阶—进阶指南"
draft: false
---

### 

` #include<algorithm>
 //对a中的从a.begin()（包括它）到a.end()（不包括它）的元素进行从小到大排列
 sort(a.begin(),a.end());
 //对a中的从a.begin()（包括它）到a.end()（不包括它）的元素倒置，但不排列，如a中元素为1,3,2,4,倒置后为4,2,3,1
 reverse(a.begin(),a.end());
  //把a中的从a.begin()（包括它）到a.end()（不包括它）的元素复制到b中，从b.begin()+1的位置（包括它）开始复制，覆盖掉原有元素
 copy(a.begin(),a.end(),b.begin()+1);
 //在a中的从a.begin()（包括它）到a.end()（不包括它）的元素中查找10，若存在返回其在向量中的位置
  find(a.begin(),a.end(),10);

`
`#include<vector>
vector<int> a,b;
//b为向量，将b的0-2个元素赋值给向量a
a.assign(b.begin(),b.begin()+3);
//a含有4个值为2的元素
a.assign(4,2);
//返回a的最后一个元素
a.back();
//返回a的第一个元素
a.front();
//返回a的第i元素,当且仅当a存在
a[i];
//清空a中的元素
a.clear();
//判断a是否为空，空则返回true，非空则返回false
a.empty();
//删除a向量的最后一个元素
a.pop_back();
//删除a中第一个（从第0个算起）到第二个元素，也就是说删除的元素从a.begin()+1算起（包括它）一直到a.begin()+3（不包括它）结束
a.erase(a.begin()+1,a.begin()+3);
//在a的最后一个向量后插入一个元素，其值为5
a.push_back(5);
//在a的第一个元素（从第0个算起）位置插入数值5,
a.insert(a.begin()+1,5);
//在a的第一个元素（从第0个算起）位置插入3个数，其值都为5
a.insert(a.begin()+1,3,5);
//b为数组，在a的第一个元素（从第0个元素算起）的位置插入b的第三个元素到第5个元素（不包括b+6）
a.insert(a.begin()+1,b+3,b+6);
//返回a中元素的个数
a.size();
//返回a在内存中总共可以容纳的元素个数
a.capacity();
//将a的现有元素个数调整至10个，多则删，少则补，其值随机
a.resize(10);
//将a的现有元素个数调整至10个，多则删，少则补，其值为2
a.resize(10,2);
//将a的容量扩充至100，
a.reserve(100);
//b为向量，将a中的元素和b中的元素整体交换
a.swap(b);
//b为向量，向量的比较操作还有 != >= > <= <
a==b;

`
`void update(vector<int> &oldVec,  vector<int> &newVec) {
    sort(oldVec.begin(), oldVec.end());
    sort(newVec.begin(), newVec.end());
    if (oldVec == newVec) return;
    vector<int> bingji, jiaoji, VecDel, VecAdd; // 并集 . 交集， oldvec -> newvec 需要删除的 和 需要增加的
    set_intersection(oldVec.begin(), oldVec.end(), newVec.begin(), newVec.end(), inserter(jiaoji, jiaoji.begin()));
    set_union(oldVec.begin(), oldVec.end(), newVec.begin(), newVec.end(), inserter(bingji, bingji.begin()));
    set_difference(oldVec.begin(), oldVec.end(), jiaoji.begin(), jiaoji.end(), inserter(VecDel, VecDel.begin()));
    set_difference(newVec.begin(), newVec.end(), jiaoji.begin(), jiaoji.end(), inserter(VecAdd, VecAdd.begin()));
}

`

### 

*

````cpp
void update(set<int> &oldVec,  set<int> &newVec) {
    sort(oldVec.begin(), oldVec.end());
    sort(newVec.begin(), newVec.end());
    if (oldVec == newVec) return;
    set<int> bingji, jiaoji, VecDel, VecAdd; // 并集 . 交集， oldvec -> newvec 需要删除的 和 需要增加的
    set_intersection(oldVec.begin(), oldVec.end(), newVec.begin(), newVec.end(), inserter(jiaoji, jiaoji.begin()));
    set_union(oldVec.begin(), oldVec.end(), newVec.begin(), newVec.end(), inserter(bingji, bingji.begin()));
    set_difference(oldVec.begin(), oldVec.end(), jiaoji.begin(), jiaoji.end(), inserter(VecDel, VecDel.begin()));
    set_difference(newVec.begin(), newVec.end(), jiaoji.begin(), jiaoji.end(), inserter(VecAdd, VecAdd.begin()));
}

`
`begin();            // 返回指向第一个元素的迭代器
end();              // 返回指向迭代器的最末尾处（即最后一个元素的下一个位置）
clear();            // 清除所有元素
count();            // 返回某个值元素的个数
 
empty();            // 如果集合为空，返回true
 
equal_range();      //返回集合中与给定值相等的上下限的两个迭代器
 
erase()–删除集合中的元素
 
find()–返回一个指向被查找到元素的迭代器
 
get_allocator()–返回集合的分配器
 
insert()–在集合中插入元素
 
lower_bound()–返回指向大于（或等于）某值的第一个元素的迭代器
 
key_comp()–返回一个用于元素间值比较的函数
 
max_size()–返回集合能容纳的元素的最大限值
 
rbegin()–返回指向集合中最后一个元素的反向迭代器
 
rend()–返回指向集合中第一个元素的反向迭代器
 
size()–集合中元素的数目
 
swap()–交换两个集合变量
 
upper_bound()–返回大于某个值元素的迭代器
 
value_comp()–返回一个用于比较元素间的值的函数
`

## 

#include

bitset可以看看作一个多位二进制数，每8位占用一个字节，相当于采用了状态压缩的二进制数组，并支持基本的位运算，在估算程序的运行的时间时，我们一般以32位正数的运算次数为基准，因此n位bitset执行一次位运算的复杂度可视为n/32，效率较高。

声明

bitset<10000> s ;  表示一个10000位二进制数，< >中填写位数。

下面把位数记为 n ;

位运算操作符：

~s : 返回对bitset按位取反的结果。

&，|，^ : 返回对两个位数相同的bitset执行按位与，或，异或运算的结果。

，!= : 比较两个bitset代表的二进制数是否相等。

[ ] 操作符

s[ k ] 表示s的第k位，既可以取值，也可以赋值。

在10000位二进制数中，最低位为 s [ 0 ] , 最高位是 s [ 9999 ] 。

count

s.count ( )  返回有多少位为1；

any/none

若s的每一位都为0， 则s.any( ) 返回false，s.none( )返回true.

若s的至少有一位为1， 则s.any( ) 返回true，s.none( )返回flase.

set/reset/flip

s.set( ）：把s所有位变为1.

s.set( k , v ) ：把s的第k位改为v , 即 s[ k ] = v；

s.reset( )：把s所有位变为0.

s.reset( k )：把s的第k位改为0 , 即 s[ k ] = 0；

s.flip( )：把s所有的位取反，即s=~s;

s.flip( k ):把s的第k位取反，s [ k ]^=1；

原文链接：https://blog.csdn.net/sodacoco/article/details/82905864*