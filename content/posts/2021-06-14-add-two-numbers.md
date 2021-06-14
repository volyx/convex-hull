---
author: "volyx"
title:  "2. Add Two Numbers"
date: "2021-06-14"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "linked-list"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```txt
Example 1:

Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

![ex1](/images/2021-06-04-ex1.jpg)

```txt
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]

Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

Constraints:

- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

## Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        
        ListNode head = null;
        ListNode curr = null;
        ListNode prev = null;
        int carry = 0;
        while (l1 != null || l2 != null) {
            int value = 0;
            if (l1 != null) value += l1.val;
            if (l2 != null) value +=l2.val;
            if (carry > 0) {
                value+=1;
                carry = 0;
            }
            
            if (value >= 10) {
                carry = 1;
                value = value % 10;
            }
            
            curr = new ListNode();
            curr.val = value;
                
            if (prev == null) {
                prev = curr;
            } else {            
                prev.next = curr;
                prev = curr;
            } 
            
            if (head == null) {
                head = prev;    
            }
            
            l1 = l1 != null? l1.next : null;
            l2 = l2 != null ? l2.next: null;
        }
        
        if (carry > 0) {
            prev.next = new ListNode(1);
        }
        return head;
    }
}
```
