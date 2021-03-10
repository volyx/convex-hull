---
author: "volyx"
title:  "Group Anagrams"
date: "Thu May 14 00:00:00 MSK 2020"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

Given an array of strings, group anagrams together.

Example:

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

Note:
```
    All inputs will be in lowercase.
    The order of your output does not matter.
```
Solution 

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        
        int[] c = new int[26];
        for (String s : strs) {
            Arrays.fill(c, 0);
            for (int i = 0 ; i < s.length(); i++) {
                c[s.charAt(i) - 'a']++;
            }
            
            String code = Arrays.toString(c);
            
            List<String> list = map.get(code);
            if (list == null) {
                list = new ArrayList<>();
            } 
            list.add(s);
            map.put(code, list);
        }
        return new ArrayList<>(map.values());
    }
}
