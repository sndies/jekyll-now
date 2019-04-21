---
layout: post
title:  "dp算法- egg dropping问题"
date:   2019-04-21 14:27:43 +0800
categories: jekyll update
---


---

<br/>
<br/>

#### · 要求说明

  输入： n个鸡蛋，k层楼， 考虑最糟糕的情况   
  输出： 找到鸡蛋不摔碎的楼层，最少的尝试数


<br/>

#### · 推算状态转移方程

 1.寻找问题子空间， 假设当前位于x层楼， 扔一个鸡蛋只有两种可能，
    a.蛋碎.....这时只能下一层楼寻找解决空间, 注意子问题空间中鸡蛋少了一个
    b.蛋没碎....这时可能再往上一层楼寻找解决空间

 2.状态转移方程
   eggDrop(n, k) = 1 + min{  max(eggDrop(n - 1,  x - 1),    eggDrop(n,  k - x)) };   
   x in {1, 2, ..., k} 
  
<br/>

#### · 递归解法

```java
public class GFG {  
    static int eggDrop(int n, int k) {  
        if (k == 1 || k == 0)  
            return k;  
      
        if (n == 1)  
            return k;  
      
        int min = Integer.MAX_VALUE;  
        int x, res;  
     
        for (x = 1; x <= k; x++)  {  
            res = Math.max(eggDrop(n-1, x-1), eggDrop(n, k-x));  
            if (res < min)  
                min = res;  
        }  
      
        return min + 1;  
    }  
      
    public static void main(String args[])  {  
        int n = 2, k = 10;  
        System.out.print("Minimum number of " + "trials in worst case with " + n + " eggs and " + k   + " floors is " + eggDrop(n, k));  
    } 

```

<br>

#### · dp解法

```java
class EggDrop { 
    static int eggDrop(int n, int k) { 
      
        int eggFloor[][] = new int[n+1][k+1]; 
        int res; 
        int i, j, x; 
           
        for (i = 1; i <= n; i++) { 
            eggFloor[i][1] = 1; 
            eggFloor[i][0] = 0; 
        } 
          
        for (j = 1; j <= k; j++) 
            eggFloor[1][j] = j; 
            
        for (i = 2; i <= n; i++) 
        { 
            for (j = 2; j <= k; j++) 
            { 
                eggFloor[i][j] = Integer.MAX_VALUE; 
                for (x = 1; x <= j; x++) 
                { 
                     res = 1 + max(eggFloor[i-1][x-1], eggFloor[i][j-x]); 
                     if (res < eggFloor[i][j]) 
                        eggFloor[i][j] = res; 
                } 
            } 
        } 
           
        return eggFloor[n][k]; 
  
    } 
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
