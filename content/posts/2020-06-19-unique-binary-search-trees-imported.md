---
author: "volyx"
title:  "Unique Binary Search Trees"
date: "Fri Jun 19 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

Example:
```
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

```

Notes: Catalan's numbers: 
```
C(0) = C(1) = 1
C(2) = C(1) * C(0) + C(0) * C(1)
C(3) = C(2) * C(1) + C(1) * C(1) + C(1) * C(2)
```
![catalans](http://quicklatex.com/cache3/ed/ql_40eefdca02335a56d3ccab2eff2aa3ed_l3.png)

Solution:

```java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= i - 1; j++) {
                dp[i] += dp[j] * dp[i - j - 1];
            }
        }
        System.out.println(Arrays.toString(dp));
        return dp[n];
    }
}
