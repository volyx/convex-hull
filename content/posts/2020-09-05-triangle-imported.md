---
author: "volyx"
title:  "Triangle"
date: "Sat Sep 05 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```txt
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

Solution:

```java
class Solution {
    public int minimumTotal(List<List<Integer>> tree) {
        if (tree.size() == 0) {
            return 0;
        }
        for (int level = tree.size() - 2; level >= 0; level--) {
                                    // [1]
            List<Integer> currentLevel = tree.get(level); // [1 2]
            List<Integer> nextLevel = tree.get(level+1); // [1 4 5]

            for (int col = 0; col < currentLevel.size(); col++) {
                int minSum = Math.min(
                    currentLevel.get(col) + nextLevel.get(col),
                    currentLevel.get(col) + nextLevel.get(col + 1)
                );
                currentLevel.set(col, minSum);
            }
        }
        return tree.get(0).get(0);
    }
}
