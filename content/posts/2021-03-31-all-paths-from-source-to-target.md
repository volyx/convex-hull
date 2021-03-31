---
author: "volyx"
title:  "797. All Paths From Source to Target"
date: "2021-03-31"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "graph", "dfs"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)

Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1, and return them in any order.

The graph is given as follows: graph[i] is a list of all nodes you can visit from node i (i.e., there is a directed edge from node i to node graph[i][j]).

```txt
Example 1:

Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

![ex1](/images/2021-03-31-dfs-ex1.jpg)

```txt
Example 2:

Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
```

![ex2](/images/2021-03-31-dfs-ex2.jpg)

```txt
Example 3:

Input: graph = [[1],[]]
Output: [[0,1]]
```

```txt
Example 4:

Input: graph = [[1,2,3],[2],[3],[]]
Output: [[0,1,2,3],[0,2,3],[0,3]]
```

```txt
Example 5:

Input: graph = [[1,3],[2],[3],[]]
Output: [[0,1,2,3],[0,3]]
```

Constraints:

- n == graph.length
- 2 <= n <= 15
- 0 <= graph[i][j] < n
- graph[i][j] != i (i.e., there will be no self-loops).
- The input graph is guaranteed to be a DAG.

## Solution

```java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<Integer> paths = new ArrayList<>();
        List<List<Integer>> res = new ArrayList<>();
        build(0, graph, paths, res);
        return res;
    }
    
    void build(int s, int[][] g, List<Integer> paths, List<List<Integer>> res) {
        paths.add(s);
        if (s == g.length - 1) {
            res.add(new ArrayList<>(paths));
        } else {
            for (int v : g[s]) {
                 build(v, g, paths, res);
            }
        }
        paths.remove(paths.size() - 1);
    }
}
```
