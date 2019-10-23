---
title: Minimum Path Sum[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Minimum Path Sum[M]

------

## 题目

> Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.
> Note: You can only move either down or right at any point in time.



## 思路

### DP

这应该是很容易想到的，因为每次只能往下或右走，所以对于每个格，就两种可能：

- 从上面走下来
- 从左边走过来
  那么很容易写出表达式：dp(i,j) = min(dp(i-1,j) , dp(i,j-1)) + path(i,j)
  然后要做一个处理，就是对于第0行，和第0列只能从左边或上面走。这样判断很麻烦，其实有一个很简单的办法：
  增加一行和一列，让这一行和这一列都为一个很大的值，这样，不管是第0行还是0列，都可以用统一的算法。
  （这里有个小注意点，就是我对minpath[0][1]赋值为0，这是为了更改原来minpath[0][0]位置的值）

```java
public class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        if(0 == m)
            return 0;
        int n = grid[0].length;
        int [][] minpath = new int[m+1][n+1];
        //init 0th row and 0th column to Max
        for(int i = 0;i <= m;i ++)
            minpath[i][0] = Integer.MAX_VALUE;
        for(int j = 0;j <= n;j ++)
            minpath[0][j] = Integer.MAX_VALUE;
            
        minpath[0][1] = 0;
        
        for(int i = 1;i <= m;i ++)
            for(int j = 1;j <= n;j++)
                    minpath[i][j] = Math.min(minpath[i-1][j],minpath[i][j-1]) + grid[i-1][j-1];

        return minpath[m][n];
        
    }
}
```

### 一维数组

当然，上面的算法还可以改进，就是把二维数组换成一维数组，因为我们实际运行的时候发现，我们每次计算只和当前行的grid和之前行的minpath有关。
这个一维数组一直会更新，而更新条件就是 : dp[j] = min(dp(j),dp(j-1)) + grid(i,j) 
这里同样为了避免第0列出问题（j-1越界），加入了1格，实际j从1开始  

```java
public class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        if(0 == m)
            return 0;
        int n = grid[0].length;
        int [] minpath = new int[n+1];
        for(int i = 0;i <= n;i ++)
            minpath[i] = Integer.MAX_VALUE;

        minpath[1] = 0;

        for(int i = 0;i < m;i ++)
            for(int j = 1;j <= n;j++)
                minpath[j] = Math.min(minpath[j-1],minpath[j]) + grid[i][j-1];

        return minpath[n];

    }
}

```