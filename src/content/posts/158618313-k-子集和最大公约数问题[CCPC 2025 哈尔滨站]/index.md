---
title: "k-子集和最大公约数问题[CCPC 2025 哈尔滨站]"
published: 2026-03-03
description: ""
tags: ["c++", "c语言", "算法", "数学"]
category: "当前文章被以下社区和专栏收录："
draft: false
---

![]\(https://i-blog.csdnimg.cn/direct/71b6aa21de104cb2b62c5b1d451791c9.png)

![]\(https://i-blog.csdnimg.cn/direct/df205a9335304d22a3729e76a5d9c8ff.jpeg)

`#include<iostream>
#include<queue>
#include<cstdio>
#include<algorithm>
#include<cstring>
#define N 5000100
#define ll long long 
using namespace std;
ll gcd(ll a, ll b) {
    while (b) {
        ll t = a % b;
        a = b;
        b = t;
    }
    return a;
}

int main() { 
    int T;cin >> T;
    while (T--) {
        int n;
        cin >> n;
        vector<ll> a(n);
        for (int i = 0; i < n; ++i) cin >> a[i];
        if (n == 1) {
            cout << "infinite\n";
            continue;
        } 
        bool all_equal = true;
        ll mn = a[0], mx = a[0];
        for (ll x : a) {
            if (x != a[0]) all_equal = false;
            if (x < mn) mn = x;
            if (x > mx) mx = x;
        }
        if (all_equal) {
            cout << "infinite\n";
            continue;
        } 
        ll G = a[0];
        for (int i = 1; i < n; ++i) G = gcd(G, a[i]); 
        vector<ll> b(n);
        for (int i = 0; i < n; ++i) b[i] = a[i] / G;
        sort(b.begin(), b.end()); 
        ll D = 0;
        for (int i = 1; i < n; ++i) {
            ll diff = b[i] - b[i-1];
            if (diff != 0) {
                D = gcd(D, diff);
            }
        } 
        ll ans = G * D;
        cout << ans << " " << D << "\n";
    }
    return 0;
}
`