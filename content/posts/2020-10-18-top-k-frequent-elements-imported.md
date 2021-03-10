---
author: "volyx"
title:  "Top K Frequent Elements"
date: "Sun Oct 18 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given a non-empty array of integers, return the k most frequent elements.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:

Input: nums = [1], k = 1
Output: [1]

Note:

- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
- It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
- You can return the answer in any order.

Solution:

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freq = new HashMap<>();
        for (int num : nums) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }

        Queue<Integer> q = new PriorityQueue<>(Comparator.comparingInt(freq::get));

        for (int num : freq.keySet()) {
            q.add(num);
            if (q.size() > k) {
                q.remove();
            }
        }
        int[] result = new int[k];
        int i = q.size() - 1;
        for (int num : q) {
            result[i--] = num;
        }
        return result;
    }
}
