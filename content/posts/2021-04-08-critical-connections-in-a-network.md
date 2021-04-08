---
author: "volyx"
title:  "1192. Critical Connections in a Network"
date: "2021-04-08"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "hard", "dfs", "scc", "tarjan"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[1514. Path with Maximum Probability](https://leetcode.com/problems/critical-connections-in-a-network/)

There are n servers numbered from 0 to n-1 connected by undirected server-to-server connections forming a network where connections[i] = [a, b] represents a connection between servers a and b. Any server can reach any other server directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some server unable to reach some other server.

Return all critical connections in the network in any order.

```txt
Example 1:

Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted.
```

![ex1](/images/2021-04-08-ex1.png)

## Solution

```java
class Solution {
    boolean[] visited = new boolean[10_0000];
    public boolean canReach(int[] arr, int start) {
        if (start < 0 || start >= arr.length) return false;
        if (visited[start]) return false;
        visited[start] = true;
        if (arr[start] == 0) return true;
        int right = start + arr[start];
        int left = start - arr[start];
        return canReach(arr, left) || canReach(arr, right);
    }
}
```
