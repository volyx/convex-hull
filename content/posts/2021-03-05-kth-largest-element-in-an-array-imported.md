---
author: "volyx"
title:  "215. Kth Largest Element in an Array"
date: "2021-03-05"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "heap"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

![https://leetcode.com/problems/kth-largest-element-in-an-array/]

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

```txt
Example 1:

Input: [3,2,1,5,6,4] and k = 2
Output: 5

Example 2:

Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4

Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
```

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        MinPQ pq = new MinPQ(k);
        
        for (int a: nums) {
            pq.add(a);
        }
        
        return pq.min();
    }
    
    
    static class MinPQ {
        final int[] pq;
        int n = 0;
        
        MinPQ(int size) {
            this.pq = new int[size + 1];
        }
        
        int min() {
            return pq[1];
        }
        
        void add(int i) {
            if (n < pq.length - 1) {
                pq[++n] = i;
                swim(n);
            } else {
                if (i > pq[1]) {
                    pq[1] = i;
                    sink(1);
                }
            }
        }
        
        void sink(int i) {
            int left = 2 * i;
            int right = 2 * i + 1;
            
            int smallest = i;
            
            if (left < pq.length && pq[left] < pq[i]) {
                smallest = left;
            }
            
            if (right < pq.length && pq[right] < pq[smallest]) {
                smallest = right;
            }
            if (smallest != i) {
                swap(i, smallest);
                sink(smallest);
            }
        }
        
        void swim(int i) {
            int j = i / 2;
            if (j > 0 && pq[i] < pq[j]) {
                swap(i, j);
                swim(j);
            }
        }
        
        void swap(int i, int j) {
            int t = pq[i];
            pq[i] = pq[j];
            pq[j] = t;
        }
    }
}
