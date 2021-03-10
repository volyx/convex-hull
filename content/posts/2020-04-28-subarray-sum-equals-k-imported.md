---
author: "volyx"
title:  "Subarray Sum Equals K"
date: "Tue Apr 28 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:

Input:nums = [1,1,1], k = 2
Output: 2

Note:
```
    The length of the array is in range [1, 20,000].
    The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].
```

Hints
```
Hide Hint #1  
    Will Brute force work here? Try to optimize it.
Hide Hint #2  
    Can we optimize it by using some extra space?
Hide Hint #3  
    What about storing sum frequencies in a hash table? Will it be useful?
Hide Hint #4  
    sum(i,j)=sum(0,j)-sum(0,i), where sum(i,j) represents the sum of all the elements from index i to j-1. Can we use this property to optimize it.
```

Solution:

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> freq = new HashMap<>();
        int sum = 0;
        int counter = 0;
        freq.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum = sum + nums[i];

            if (freq.containsKey(sum - k)) {
                counter+= freq.get(sum -k);
            }
            freq.put(sum, freq.getOrDefault(sum, 0) + 1);
        }
        return counter;
    }
}
