---
title: Triangle[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Triangle[M]

------

# 题目

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
[
				[2],
			[3,4],
			   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

# 思路

如图分析：
$d(0,1) = Path[0,1] + min(d(1,1)，d(1,2))$</br>
$d(1,1) = Path[1,1] + min(d(2,1),d(2,2))$</br>
$d(1,2) = Path[1,2] + min(d(2,2),d(2,3))$</br>
$……$</br>
$d(3,1) = 4$</br>
$d(3,2) = 1$</br>
$d(3,3) = 8$</br>
$d(3,4) = 3$</br>
我们从底层往上走，每走一层，都是到这一层的最短路径距离。所以，我们每次只用保存到这一层每个元素的最短路径距离即可。也就是说，对于n层，我们最多只需要n个额外空间。

- 最底层: $[4,1,8,3]$</br>
- 向上走:$[6+1,5+1,7+3] = [7,6,10]$</br>
- 继续:$[3+6,4+6] = [9,10]$</br>
- 最后:$[2+9] = [11]$</br>

# 代码

```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector <int> min_path(triangle.back());
        for(int i = triangle.size()-2;i>=0; i--)
        {
            for(int j = 0;j < triangle[i].size();j++)
            {
                min_path[j] = min(min_path[j],min_path[j+1]) + triangle[i][j];
            }
        }
        return min_path[0];
    }
};
```

