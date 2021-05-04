# 168-Excel表列名称

难度 简单



## 题目描述

给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
示例 1:
```
输入: 1
输出: "A"
```
示例 2:
```
输入: 28
输出: "AB"
```
示例 3:
```
输入: 701
输出: "ZY"
```


## 思路

10进制转26进制，但有所不同的是正常转换成26进制的余数是0-25，
而本题的余数是1-26（对应A-Z），为了消除差距的这个`1`, 在columnNumber为26的倍数的时候进行单独处理。



## 代码

```c++
class Solution {
public:
    string convertToTitle(int columnNumber) {
        string columns = "0ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        string res;
        while (columnNumber > 0) {
            int name = columnNumber % 26;
            if (name == 0) {
                name = 26;
                columnNumber -= 26;
            }
            res = columns[name] + res;
            columnNumber = columnNumber / 26;
        }
        return res;
    }
};
```

