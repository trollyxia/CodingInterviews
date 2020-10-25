# 52-N皇后II

难度 困难



## 题目描述

*n* 皇后问题研究的是如何将 *n* 个皇后放置在 *n*×*n* 的棋盘上，并且使皇后彼此之间不能相互攻击。

![](C:/Users/ladmin/Desktop/CodingInterviews/Leetcode/images/8-queens.png)

上图为 8 皇后问题的一种解法。

给定一个整数 `n`，返回 `n` 皇后不同的解决方案的数量。

示例:

```
输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```


提示：

- 皇后，是国际象棋中的棋子，意味着国王的妻子。皇后只做一件事，那就是“吃子”。当她遇见可以吃的棋子时，就迅速冲上去吃掉棋子。当然，她横、竖、斜都可走一或 N-1 步，可进可退。（引用自 百度百科 - 皇后 ）



## 思路

见上一题[51-N皇后](51-N皇后.md)的思路。区别在于，第 51题需要得到所有可能的解，这道题只需要得到可能的解的数量。因此这道题可以使用第 51题的做法，只需要将得到所有可能的解改成得到可能的解的数量即可。



## 代码

```c++
class Solution {
public:
    int res;
    void helper(int n, int placed, vector<bool> column, vector<bool> slash, vector<bool> backslash) {
        if (placed == n) { 
            res++;
            return;
        }
        int i, j;
        // try every possible position in the current row
        for (i = 0; i < n; i++) {
            if (column[i] || slash[placed + i] || backslash[placed - i + n]) continue;
            column[i] = true;
            slash[placed + i] = true;
            backslash[placed - i + n] = true;
            // search how to place queen for the next few rows
            helper(n, placed + 1, column, slash, backslash);
            column[i] = false;
            slash[placed + i] = false;
            backslash[placed - i + n] = false;
        }
    }
    int totalNQueens(int n) {
        vector<bool> column(n, false);
        vector<bool> slash(2 * n, false);
        vector<bool> backslash(2 * n, false);
        helper(n, 0, column, slash, backslash);
        return res;
    }
};
```



