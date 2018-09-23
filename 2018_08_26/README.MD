# Algorithm

[892. Surface Area of 3D Shapes](https://leetcode.com/contest/weekly-contest-99/problems/surface-area-of-3d-shapes/)

题目描述：

英文：
On a `N  * N`  grid, we place some `1 * 1 * 1` cubes.

Each value `v = grid[i][j]` represents a tower of v cubes placed on top of grid cell `(i, j)`.

Return the total surface area of the resulting shapes.

中文：
给定一个整数数组 A，对于每个整数 A[i]，我们可以选择任意 x 满足 -K <= x <= K，并将 x 加到 A[i] 中。

在此过程之后，我们得到一些数组 B。

返回 B 的最大值和 B 的最小值之间可能存在的最小差值。

**Example 1:**

>Input: [[2]]

>Output: 10

**Example 2:**

>Input: [[1,2],[3,4]]

>Output: 34


**Example 3:**

>Input: [[1,0],[0,2]]

>Output: 16

**Example 4:**

>Input: [[1,1,1],[1,0,1],[1,1,1]]

>Output: 32

**Example 5:**

>Input: [[2,2,2],[2,1,2],[2,2,2]]

>Output: 46


```c++

class Solution {
    public int surfaceArea(int[][] grid) {
        int[] dr = new int[]{0, 1, 0, -1};
        int[] dc = new int[]{1, 0, -1, 0};

        int N = grid.length;
        int ans = 0;

        for (int r = 0; r < N; ++r)
            for (int c = 0; c < N; ++c)
                if (grid[r][c] > 0) {
                    ans += 2;
                    for (int k = 0; k < 4; ++k) {
                        int nr = r + dr[k];
                        int nc = c + dc[k];
                        int nv = 0;
                        if (0 <= nr && nr < N && 0 <= nc && nc < N)
                            nv = grid[nr][nc];

                        ans += Math.max(grid[r][c] - nv, 0);
                    }
                }

        return ans;
    }
}
```

# Review
[Python for data science : Part 4](https://towardsdatascience.com/python-for-data-science-part-4-6087cb811a29)

![](https://cdn-images-1.medium.com/max/1600/1*aNMBIivJppLy2fMRVUSgHA.gif)

本文简单介绍了python这门语言在数据科学中的使用，难度偏向入门,本文章和上周分享的 Review 属于同一系列，属于第四部分

本篇文章终于脱离了之前枯燥乏味的基础普及开始有干货了↓↓↓↓
1. Descriptive statistics of numerical columns
2. Create column based on conditions
3. Unique values of column
4. Cross tab (similar to pivot table in Excel)
5. Sorting values
6. Check column datatypes
7. Binning numerical columns


如果大家之前没有经过系统的学习，那么看这四篇文章是是会让自己对数据分析的认识提高一个台阶的，这样也会为之后的kaggle竞赛做好铺垫。



## Technique
[这样一步一步推导支持向量机，谁还看不懂？](https://mp.weixin.qq.com/s/wLWIFegIwlndx-n2yWywuA)

经过上周的铺垫后相信大家已经了解如何理解SVM的目标函数和约束是怎么得来的思路。（作者在文末表示会在接下来的文章中推导KKT求解全过程，我们拭目以待）

今天这篇文章就带领大家进行了简单的推导，但是个人觉得过程有些简略并且逻辑不够严谨，今后如果有合适的机会希望自己写出一篇系统的讲解来和大家一起进步。

# Share
最近遇到了一个问题，关于谷歌浏览器（chrome）
就是在win端使用浏览器的时候，可以用固定标签页的方式让用户在下次打开浏览器时也自动打开这些固定标签页。但是在mac端并不可以，今天就遇到了这个问题导致很多标签页丢失了，查了一下发现这个的解决方案 
https://www.v2ex.com/t/269601

那就是在mac端的时候可以采用 command+Q 的方式来关闭浏览器，这样下次就可以打开之前并没有关闭的标签页（非固定的也是一样），这里的机制也许就像上文中所说的一样，如果直接点击红色关闭按钮，默认是把所有的标签页删除（而且这里的关闭记录并不会被保存在历史记录中，只有这点和专门关闭标签页是不一样的）。
