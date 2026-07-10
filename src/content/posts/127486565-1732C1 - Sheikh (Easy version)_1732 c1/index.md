---
title: "1732C1 - Sheikh (Easy version)_1732 c1. sheikh (easy version)"
published: 2022-10-24
description: ""
tags: ["1024程序员节"]
category: "比赛"
draft: false
---

Note that f(l,r)≤f(l,r+1). To prove this fact, let’s see how the sum and xor change when the element x is added. The sum will increase by x, but xor cannot increase by more than x.

Then it was possible to use two pointers or binary search to solve the problem. If you solve the problem in the second way, then you iterate over the right boundary of the answer and look for the optimal left boundary for it by binary search. You will need O(1) to find the sum on the segment and xor on the segment. To do this, you can use prefix sums and prefix xor.