---
author: "volyx"
title:  "1637. Widest Vertical Area Between Two Points Containing No Points"
date: "Fri Feb 26 00:00:00 MSK 2021"
# description: "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
tags:  ["leetcode", "medium", "quick-sort"]
categories: ["leetcode"]
# series: ["Themes Guide"]
# aliases: ["migrate-from-jekyl"]
# ShowToc: true
# TocOpen: true
# weight: 2
---

**/
class Solution {
    private static final Random RANDOM = new Random();
    public int[][] kClosest(int[][] points, int K) {
        int lo = 0;
        int hi = points.length - 1; 
        
        shuffle(points);
        while (lo < hi) {
            int j = partition(points, lo, hi);
            
            if (j < K) {
                lo = j + 1;
            } else if (j > K) {
                hi = j - 1;
            } else {
                return copyOf(points,K);
            }
        }
        
        return copyOf(points, K);
    }
    
    int partition(int[][] a, int lo, int hi) {
        int i = lo;
        int j = hi + 1;
        while (true) {
            
            while (less(a[++i], a[lo])) {
                if (i == hi) break;
            }
            
            while (less(a[lo], a[--j])) {
                if (j == lo) break;
            }
            
            if (i >= j) break;
            swap(a, i, j);
        }
        swap(a, lo, j);
        return j;
    }
    
    static boolean less(int[] a, int[] b) {
         int diff = b[0] * b[0] + b[1]*b[1] - a[0]* a[0] - a[1] * a[1];
         return diff > 0;
    }
    
    void swap(int[][] a, int i, int j) {
        int[] temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    
    static int[][] copyOf(int[][] points, int k) {
        int[][] a = new int[k][];
        
        for (int i = 0; i < k; i++) {
            a[i] = points[i];
        }
        
        return a;
    }
    
       
    void shuffle(int[][] a) {
        for (int i = 0; i < a.length; i++) {
            swap(a, i, RANDOM.nextInt(a.length));
        }
    }
    
    public int[][] kClosest2(int[][] points, int K) {
        List<Point> sortedPoints = new ArrayList<>();
        for (int i = 0 ; i < points.length; i++) {
            sortedPoints.add(new Point(points[i][0], points[i][1]));
        }
        
        Collections.sort(sortedPoints);
        
        int[][] res = new int[K][2];
        
        for (int i = 0; i < Math.min(points.length, K); i++) {
            res[i] = new int []{sortedPoints.get(i).x, sortedPoints.get(i).y};
        }
        
        return res;
    }
    
    class Point implements Comparable<Point> {
        int x;
        int y;
        
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
        
        public int compareTo(Point that) {
            return 
                (this.x * this.x + this.y * this.y) - 
                (that.x * that.x + that.y * that.y)
                ;
        }
        
        public String toString() {
            return String.format("[%d,%d]", this.x, this.y);
        }
    }
}
