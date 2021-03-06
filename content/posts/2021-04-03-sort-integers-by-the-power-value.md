---
author: "volyx"
title:  "1387. Sort Integers by The Power Value"
date: "2021-04-03"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "easy", "tree", "dfs"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[1387. Sort Integers by The Power Value](https://leetcode.com/problems/sort-integers-by-the-power-value/)

The power of an integer x is defined as the number of steps needed to transform x into 1 using the following steps:

- if x is even then x = x / 2
- if x is odd then x = 3 * x + 1

For example, the power of x = 3 is 7 because 3 needs 7 steps to become 1 (3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1).

Given three integers lo, hi and k. The task is to sort all integers in the interval [lo, hi] by the power value in ascending order, if two or more integers have the same power value sort them by ascending order.

Return the k-th integer in the range [lo, hi] sorted by the power value.

Notice that for any integer x (lo <= x <= hi) it is guaranteed that x will transform into 1 using these steps and that the power of x is will fit in 32 bit signed integer.

```txt
Example 1:

Input: lo = 12, hi = 15, k = 2
Output: 13
Explanation: The power of 12 is 9 (12 --> 6 --> 3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1)
The power of 13 is 9
The power of 14 is 17
The power of 15 is 17
The interval sorted by the power value [12,13,14,15]. For k = 2 answer is the second element which is 13.
Notice that 12 and 13 have the same power value and we sorted them in ascending order. Same for 14 and 15.
```

```txt
Example 2:

Input: lo = 1, hi = 1, k = 1
Output: 1
```

```txt
Example 3:

Input: lo = 7, hi = 11, k = 4
Output: 7
Explanation: The power array corresponding to the interval [7, 8, 9, 10, 11] is [16, 3, 19, 6, 14].
The interval sorted by power is [8, 10, 11, 7, 9].
The fourth number in the sorted array is 7.
```

```txt
Example 4:

Input: lo = 10, hi = 20, k = 5
Output: 13
```

```txt
Example 5:

Input: lo = 1, hi = 1000, k = 777
Output: 570
```

Constraints:

- 1 <= lo <= hi <= 1000
- 1 <= k <= hi - lo + 1

## Solution

```java
class Solution {
    Map<Integer, Integer> cache = new HashMap<>();
    public int getKth(int lo, int hi, int k) {
        var powIndex = new PriorityQueue<int[]>((a, b) -> {
            int c = Integer.compare(a[0], b[0]);
            if (c != 0) return c;
            return Integer.compare(a[1], b[1]);
        });
        cache.put(0, 0);
        cache.put(1, 0);
        for (int i = lo; i <= hi; i++) {
            int steps = power(i);
            powIndex.add(new int[] {steps, i});
        }
        while (--k > 0) {
            powIndex.poll();
        }
        return powIndex.poll()[1];
    }
    
    int power(int x) {
        if (x == 1) return 0;
        if (cache.containsKey(x)) {
             return cache.get(x);
        }
        int power = 1 + ((x % 2 == 0) ? power(x / 2) : power( 3 * x + 1));
        cache.put(x, power);
        return power;
    } 
}
```
