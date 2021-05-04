# 171-Excel表列序号

难度 简单



## 题目描述

给定一个Excel表格中的列名称，返回其相应的列序号。

例如，

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
示例 1:
```
输入: "A"
输出: 1
```
示例 2:
```
输入: "AB"
输出: 28
```
示例 3:
```
输入: "ZY"
输出: 701
```



## 思路

将字符转换成数字再求和即可。



## 代码

```c++
class Solution {
public:
    int titleToNumber(string columnTitle) {
        long long res = 0;
        for (char c: columnTitle) {
            res = res * 26 + c - 'A' + 1;   
        }
        return res;
    }
};
```

