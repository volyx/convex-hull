---
author: "volyx"
title:  "921. Minimum Add to Make Parentheses Valid"
date: "Fri Feb 19 00:00:00 MSK 2021"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "stack"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

![https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/]

Given a string S of '(' and ')' parentheses, we add the minimum number of parentheses ( '(' or ')', and in any positions ) so that the resulting parentheses string is valid.

Formally, a parentheses string is valid if and only if:

- It is the empty string, or
- It can be written as AB (A concatenated with B), where A and B are valid strings, or
- It can be written as (A), where A is a valid string.

Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.

```txt
Example 1:

Input: "())"
Output: 1

Example 2:

Input: "((("
Output: 3

Example 3:

Input: "()"
Output: 0

Example 4:

Input: "()))(("
Output: 4
```

Note:

- S.length <= 1000
- S only consists of '(' and ')' characters.


```java
class Solution {
    public int calPoints(String[] ops) {
        
        var stack = new ArrayList<Integer>();
        
        for (var op: ops) {
            switch (op) {
                case "+":
                    stack.add(stack.get(stack.size() - 1) + stack.get(stack.size() - 2));
                    break;
                case "D":
                    stack.add(stack.get((stack.size() - 1)) * 2);
                    break;
                case "C": 
                    stack.remove(stack.size() - 1);
                    break;
                default:
                    stack.add(Integer.valueOf(op));
            }
        }
        Integer sum =  0;
        for (Integer val: stack) {
            sum += val;
        }
        return sum;
    }
}
