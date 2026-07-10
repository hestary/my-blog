---
title: "斐波那契数列的奇妙性质与证明：深入解析"
published: 2022-07-25
description: ""
tags: ["Conda", "Python", "算法"]
category: "算法进阶—进阶指南"
draft: false
---


[参考](https://blog.csdn.net/weixin_44851176/article/details/104662539?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165873306616780366532994%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165873306616780366532994&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-104662539-null-null.142%5Ev33%5Enew_blog_pos_by_title,185%5Ev2%5Etag_show&utm_term=%E5%B8%B8%E7%94%A8Fibonacci%E6%95%B0%E6%80%A7%E8%B4%A8&spm=1018.2226.3001.4187)


         F

         n

         −

         1

         +

         F

         n

         −

         2

         =

         F

         n

        Fn−1+Fn−2=Fn

     Fn−1+Fn−2=Fn

         F

         0

         =

         1

         ,

         F

         1

         =

         1

        F0=1,F1=1

     F0=1,F1=1
 上述式子为定义式


         F

         (

         0

         )

         +

         F

         (

         1

         )

         +

         …

         +

         F

         (

         n

         )

         =

         F

         (

         n

         +

         2

         )

         −

         1

        F(0) + F(1)+ … + F(n) = F(n+2) − 1

     F(0)+F(1)+…+F(n)=F(n+2)−1

证明：

         F

         0

         +

         F

         1

         =

         F

         2

        F0+F1=F2

     F0+F1=F2

         F

         1

         +

         F

         2

         =

         F

         3

        F1+F2=F3

     F1+F2=F3

         F

         2

         +

         F

         3

         =

         F

         4

        F2+F3=F4

     F2+F3=F4

⋮

        F

        n

        +

        F

        n

        +

        1

        =

        F

        n

        +

        2

       Fn+Fn+1=Fn+2

    Fn+Fn+1=Fn+2

        F

        0

        +

        2

        F

        1

        +

        2

        F

        2

        +

        …

        +

        2

        F

        n

        +

        F

        n

        +

        1

        =

        F

        1

        +

        F

        2

        +

        …

        +

        F

        n

        +

        2

       F0+2F1+2F2+…+2Fn+Fn+1=F1+F2+…+Fn+2

    F0+2F1+2F2+…+2Fn+Fn+1=F1+F2+…+Fn+2

        F

        0

        +

        F

        1

        +

        F

        2

        +

        …

        +

        F

        n

        +

        F

        n

        +

        1

        =

        F

        n

        +

        2

        −

        F

        1

        =

        F

        n

        +

        2

        −

        1

       F0+F1+F2+…+Fn+Fn+1=Fn+2−F1=Fn+2−1

    F0+F1+F2+…+Fn+Fn+1=Fn+2−F1=Fn+2−1

2.

        F

        (

        1

        )

        +

        F

        (

        3

        )

        +

        …

        +

        F

        (

        2

        n

        −

        1

        )

        =

        F

        (

        2

        n

        )

       F(1) + F(3) + … + F(2n−1) = F(2n)

    F(1)+F(3)+…+F(2n−1)=F(2n)

证明：

        F

        1

        =

        F

        0

        +

        1

       F1=F0+1

    F1=F0+1

        F

        3

        =

        F

        2

        +

        F

        1

       F3=F2+F1

    F3=F2+F1

         ⋮

       ⋮

    ⋮

        F

        2

        n

        −

        1

        =

        F

        2

        n

        −

        2

        +

        F

        2

        n

        −

        3

       F2n−1=F2n−2+F2n−3

    F2n−1=F2n−2+F2n−3

        F

        1

        +

        F

        3

        +

        …

        +

        F

        2

        n

        −

        1

        =

        1

        +

        F

        0

        +

        F

        1

        +

        F

        2

        +

        …

        +

        F

        2

        n

        −

        3

        +

        F

        2

        n

        −

        2

        =

        1

        +

        F

        2

        n

        −

        1

        =

        F

        2

        n

       F1+F3+…+F2n−1=1+F0+F1+F2+…+F2n−3+F2n−2=1+F2n−1=F2n

    F1+F3+…+F2n−1=1+F0+F1+F2+…+F2n−3+F2n−2=1+F2n−1=F2n


        F

        (

        0

        )

        +

        F

        (

        2

        )

        +

        …

        +

        F

        (

        2

        n

        )

        =

        F

        (

        2

        n

        +

        1

        )

        −

        1

       F(0) + F(2) + … + F(2n) = F(2n+1) − 1

    F(0)+F(2)+…+F(2n)=F(2n+1)−1
 证明：

有 

        F

        0

        +

        F

        1

        +

        …

        +

        F

        n

        =

        F

        n

        +

        2

        −

        1

        和

        F

        1

        +

        F

        3

        +

        …

        +

        F

        2

        n

        −

        1

        =

        F

        2

        n

       F0+F1+…+Fn=Fn+2−1 和 F1+F3+…+F2n−1=F2n

    F0+F1+…+Fn=Fn+2−1和F1+F3+…+F2n−1=F2n

        F

        0

        +

        F

        2

        …

        +

        F

        2

        n

        =

        F

        2

        n

        +

        2

        −

        F

        2

        n

        −

        1

        =

        F

        2

        n

        +

        1

        −

        1

       F0+F2…+F2n=F2n+2−F2n−1=F2n+1−1

    F0+F2…+F2n=F2n+2−F2n−1=F2n+1−1


        F

        (

        0

         )

         2

        +

        F

        (

        1

         )

         2

        +

        F

        (

        2

         )

         2

        +

        …

        +

        F

        (

        n

         )

         2

        =

        F

        (

        n

        )

        F

        (

        n

        +

        1

        )

       F(0)^2 + F(1)^2 + F(2)^2 + … + F(n)^2 = F(n)F(n+1)

    F(0)2+F(1)2+F(2)2+…+F(n)2=F(n)F(n+1)

证明：

有 

        F

        20

        =

        F

        0

        ∗

        F

        1

       F20=F0∗F1

    F20=F0∗F1 ，假设有 

        F

        20

        +

        F

        21

        +

        F

        22

        +

        …

        +

        F

        2

        n

        −

        1

        =

        F

        n

        −

        1

        F

        n

       F20+F21+F22+…+F2n−1=Fn−1Fn

    F20+F21+F22+…+F2n−1=Fn−1Fn

那么

        F

        20

        +

        F

        21

        +

        …

        +

        F

        2

        n

        −

        1

        +

        F

        2

        n

        =

        F

        n

        −

        1

        F

        n

        +

        F

        2

        n

        =

        F

        n

        F

        n

        +

        1

       F20+F21+…+F2n−1+F2n=Fn−1Fn+F2n=FnFn+1

    F20+F21+…+F2n−1+F2n=Fn−1Fn+F2n=FnFn+1


从第二项开始，每个偶数项的平方都比前后两项之积多1，每个奇数项的平方都比前后两项之积少1。


.

        F

        (

        n

        +

        2

        )

        +

        F

        (

        n

        −

        2

        )

        =

        3

        ×

        F

        (

        n

        )

       F(n+2) + F(n−2) = 3 × F(n)

    F(n+2)+F(n−2)=3×F(n)
 证明：

        F

        n

        +

        2

        =

        F

        n

        +

        1

        +

        F

        n

        =

        (

        F

        n

        +

        F

        n

        −

        1

        )

        +

        F

        n

        =

        (

        F

        n

        +

        (

        F

        n

        −

        F

        n

        −

        2

        )

        )

        +

        F

        n

        =

        3

        ×

        F

        n

        −

        F

        n

        −

        2

       Fn+2=Fn+1+Fn=(Fn+Fn−1)+Fn=(Fn+(Fn−Fn−2))+Fn=3×Fn−Fn−2

    Fn+2=Fn+1+Fn=(Fn+Fn−1)+Fn=(Fn+(Fn−Fn−2))+Fn=3×Fn−Fn−2


        g

        c

        d

        (

        F

        (

        n

        +

        1

        )

        ,

        F

        (

        n

        )

        )

        =

        1

       gcd( F(n+1) , F(n) ) = 1

    gcd(F(n+1),F(n))=1
 证明：
 根据辗转相减法则

        g

        c

        d

        (

        F

        n

        +

        1

        ,

        F

        n

        )

        =

        g

        c

        d

        (

        F

        n

        +

        1

        −

        F

        n

        ,

        F

        n

        )

        =

        g

        c

        d

        (

        F

        n

        ,

        F

        n

        −

        1

        )

        =

        g

        c

        d

        (

        F

        2

        ,

        F

        1

        )

        =

        1

       gcd(Fn+1,Fn)=gcd(Fn+1−Fn,Fn)=gcd(Fn,Fn−1)=gcd(F2,F1)=1

    gcd(Fn+1,Fn)=gcd(Fn+1−Fn,Fn)=gcd(Fn,Fn−1)=gcd(F2,F1)=1


        F

        (

        m

        +

        n

        )

        =

        F

        (

        m

        −

        1

        )

        F

        (

        n

        )

        +

        F

        (

        m

        )

        F

        (

        n

        +

        1

        )

       F(m+n) = F(m−1)F(n) + F(m)F(n+1)

    F(m+n)=F(m−1)F(n)+F(m)F(n+1)
 把

        F

        n

       Fn

    Fn看做斐波那契的第1项，那么到第

        F

        n

        +

        m

       Fn+m

    Fn+m项时，系数为

        F

        m

        −

        1

       Fm−1

    Fm−1

把

        F

        n

        +

        1

       Fn+1

    Fn+1看做斐波那契的第2项，那么到第

        F

        n

        +

        m

       Fn+m

    Fn+m项时，系数为

        F

        m

       Fm

    Fm


        g

        c

        d

        (

        F

        (

        n

        +

        m

        )

        ,

        F

        (

        n

        )

        )

        =

        g

        c

        d

        (

        F

        (

        n

        )

        ,

        F

        (

        m

        )

        )

       gcd( F(n+m) , F(n) ) = gcd( F(n) , F(m) )

    gcd(F(n+m),F(n))=gcd(F(n),F(m))
 证明：

        g

        c

        d

        (

        F

        n

        +

        m

        ,

        F

        n

        )

        =

        g

        c

        d

        (

        F

        n

        +

        1

        F

        m

        +

        F

        n

        F

        m

        −

        1

        ,

        F

        n

        )

        =

        g

        c

        d

        (

        F

        n

        +

        1

        F

        m

        ,

        F

        n

        )

        =

        g

        c

        d

        (

        F

        m

        ,

        F

        n

        )

       gcd(Fn+m,Fn)=gcd(Fn+1Fm+FnFm−1,Fn)=gcd(Fn+1Fm,Fn)=gcd(Fm,Fn)

    gcd(Fn+m,Fn)=gcd(Fn+1Fm+FnFm−1,Fn)=gcd(Fn+1Fm,Fn)=gcd(Fm,Fn)


        g

        c

        d

        (

        F

        (

        n

        )

        ,

        F

        (

        m

        )

        )

        =

        F

        (

        g

        c

        d

        (

        n

        ,

        m

        )

        )

       gcd( F(n) , F(m) ) = F( gcd(n,m) )

    gcd(F(n),F(m))=F(gcd(n,m))
 由8式得，Fibonacci数满足下标的辗转相减

        g

        c

        d

        (

        F

        n

        ,

        F

        m

        )

        =

        g

        c

        d

        (

        F

        g

        c

        d

        (

        n

        ,

        m

        )

        ，

        F

        g

        c

        d

        (

        n

        ,

        m

        )

        )

        =

        F

        g

        c

        d

        (

        n

        ,

        m

        )

       gcd(Fn,Fm)=gcd(Fgcd(n,m)，Fgcd(n,m))=Fgcd(n,m)

    gcd(Fn,Fm)=gcd(Fgcd(n,m)，Fgcd(n,m))=Fgcd(n,m)