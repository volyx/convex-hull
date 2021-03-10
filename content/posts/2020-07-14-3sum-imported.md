---
author: "volyx"
title:  "3Sum"
date: "Tue Jul 14 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:
```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

Solution:

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        
        if (nums.length < 3) {
            return Collections.emptyList();
        }
        
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        Set<String> uniq = new HashSet<>();
        Map<Integer, Integer> valueToIndex = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            valueToIndex.put(nums[i], i);
        }
        
        int i = 0;
        
        while (i < nums.length - 1) {
            for (int j = i + 1; j < nums.length; j++) {
                Integer sum = -(nums[i] + nums[j]);
                Integer sumIndex = valueToIndex.get(sum);
                if (sumIndex != null 
                    && sumIndex != i 
                    && sumIndex != j
                    && sumIndex > j
                    && uniq.contains("" + nums[i] + nums[j] + sumIndex) == false) {
                    result.add(List.of(nums[i], nums[j], sum));
                    uniq.add("" + nums[i] + nums[j] + sumIndex);
                }
            }  
            i++;
        }
        return result;
    }
}
