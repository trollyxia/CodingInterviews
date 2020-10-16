# 28-实现strStr()

难度 简单



## 题目描述

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

示例 2:

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```


说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。



## 思路

- （代码思路）从前向后遍历`haystack`，如果其中的字符与`needle`的首个字符相同，则进一步扫描其后面的字符判断是否能跟`needle`完全匹配。如果匹配不成功，则从`haystack`当前位置的下一个位置开始重新匹配。

  这种方法对于很长的字符串会超时，为了优化，在完全扫描`needle`判断其能否与`haystack`当前位置开始的字符串匹配之前，先对`haystack`剩余的字符串长度进行判断，如果其剩余的字符串长度不足则直接返回`-1`。（经过这个优化后就不会超时）

- KMP算法

  

## 代码

```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if (needle.length() == 0) return 0;
        if (needle.length() > haystack.length()) return -1;
        int i, j;
        for (i = 0; i < haystack.length(); i++) {
            if (haystack[i] != needle[0]) continue;
            for (j = 0; j < needle.length(); j++) {
                if (haystack.length() - i < needle.length()) 
                    return -1;
                if (haystack[i + j] != needle[j])
                    break;
            }
            if (j == needle.length()) return i;
        }
        return -1;
    }
};
```

