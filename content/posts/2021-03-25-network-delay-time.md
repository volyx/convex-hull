---
author: "volyx"
title:  "743. Network Delay Time"
date: "2021-03-25"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "grpah", "dijkstra", "bellman-ford"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)

You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

```txt
Example 1:

Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```

![ex1](/images/2021-03-25-ex1.png)

```txt
Example 2:

Input: times = [[1,2,1]], n = 2, k = 1
Output: 1
```

```txt
Example 3:

Input: times = [[1,2,1]], n = 2, k = 2
Output: -1
```

Constraints:

- 1 <= k <= n <= 100
- 1 <= times.length <= 6000
- times[i].length == 3
- 1 <= ui, vi <= n
- ui != vi
- 0 <= wi <= 100
- All the pairs (ui, vi) are unique. (i.e., no multiple edges.)

## Solution

```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        int[] costs = new int[n + 1];
        Arrays.fill(costs, -1);
        costs[k] = 0;
        Queue<int[]> q = new PriorityQueue<int[]>((a, b) -> a[1] - b[1]);
        q.add(new int[]{k, 0});
        
        List<Integer>[] visited = new List[n + 1];
        
        while (!q.isEmpty()) {
            int[] x = q.poll();
            for (int[] time: times) {
                if (x[0] == time[0]) {
                    
                    if (visited[x[0]] == null) {
                        visited[x[0]] = new ArrayList<>();
                        visited[x[0]].add(x[0]);
                    }
                    
                    if (visited[x[0]].contains(time[1])) {
                        continue;
                    }
                    
                    visited[x[0]].add(time[1]);
                    
                    int newTime = x[1] + time[2];
                    
                    int prevTime = costs[time[1]];
                    
                    if (prevTime == -1 || newTime < prevTime) {
                        costs[time[1]] = newTime;
                    }
                    q.add(new int[]{time[1], costs[time[1]]});
                }
            }
        }
        int maxTime = 0;
        for (int i = 1; i < costs.length; i++) {
            if (costs[i] == -1) {
                return -1;
            }
            maxTime = Math.max(maxTime, costs[i]);
        }
        return maxTime;
    }
}

class Solution {
    // Belman-Ford
    public int networkDelayTime(int[][] times, int n, int s) {
       int[] d = new int[n + 1];
       Arrays.fill(d, Integer.MAX_VALUE);
       d[s] = 0;
       for (int i = 1; i < n + 1; i++) {
           for (int j = 0; j < times.length; j++) {
               int[] e = times[j];
               int a = e[0];
               int b = e[1];
               int w = e[2];
               if (d[a] != Integer.MAX_VALUE) {
                   d[b] = Math.min(d[b], d[a] + w);
               }
               
           }
       } 
        
       int max = 0; 
       for (int i = 1; i < d.length; i++) {
           int t = d[i];
           if (t == Integer.MAX_VALUE) return -1;
           max = Math.max(max, t);
       }  
       return max;
    }
}
```
