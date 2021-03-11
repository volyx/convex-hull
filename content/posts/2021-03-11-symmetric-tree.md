---
author: "volyx"
title:  "101. Symmetric Tree"
date: "2021-03-11"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy", "binary-tree"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

![https://leetcode.com/problems/symmetric-tree/]

Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

![ex1](/images/2021-03-11-ex1.jpg)

```txt
Example 1:

Input: root = [1,2,2,3,4,4,3]
Output: true
```

![ex2](/images/2021-03-11-ex2.jpg)

```txt
Example 2:

Input: root = [1,2,2,null,3,null,3]
Output: false
```

Constraints:

- The number of nodes in the tree is in the range [1, 1000].
- -100 <= Node.val <= 100

```java
class Solution {
    int[][] heap;
    int n;
    public String frequencySort(String s) {
        heap = new int[128][];
        Arrays.fill(heap, new int[] {0, 0});
        int[] counts = new int[128];
        for (char c : s.toCharArray()) {
            counts[c]++;
        }
        
        for (int i = 0; i < counts.length; i++) {
            int count = counts[i];
            if (count != 0) {
                heap[++n] = new int[] {i, count};
                swim(n);
            }
        }

        StringBuilder sb = new StringBuilder();
        while (n > 0) {
            int[] val = delMax();
            char c = (char) val[0];
            for (int i = 0; i < val[1]; i++) {
                sb.append(c);
            }
        }
        return sb.toString();
    }
    
    // max heap propery -> parent > child; j > i
    // violates i > j
    void swim(int i) {
        int j = i / 2;
        if (j > 0 && less(j, i)) {
            swap(i, j);
            swim(j);
        }
    }
    
    void sink(int i) {
        int left = 2 * i;
        int right = 2 * i + 1;
        int largest = i;
        if (left < heap.length && !less(left, largest)) {
            largest = left;
        }
        
        if (right < heap.length && !less(right, largest)) {
            largest = right;
        }
        
        if (i != largest) {
            swap(i, largest);
            sink(largest);
        }
    }
    
    boolean less(int i, int j) {
        return heap[i][1] < heap[j][1];
    }
    
    int[] delMax() {
        int[] max = heap[1];
        heap[1] = heap[n--];
        heap[n + 1] = new int[]{0,0};
        sink(1);
        return max;
    }
    
    void swap(int i, int j) {
        int[] temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    } 
    
    public String frequencySort2(String s) {
        Map<Character, Integer> freq = new HashMap<>();
        char[] symbols = s.toCharArray();
        for (char c: symbols) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }
        
        Queue<Map.Entry<Character, Integer>> q 
            = new PriorityQueue<>((e1, e2) -> -Integer.compare(e1.getValue(), e2.getValue()));
        
        q.addAll(freq.entrySet());
        
        StringBuilder sb = new StringBuilder();
        
         while (!q.isEmpty()) {
            var entry = q.poll();
            // System.out.println(entry);
            for (int i = 0; i < entry.getValue(); i++) {
                sb.append(entry.getKey());
            }
        }
        
        return sb.toString();
    }
}
