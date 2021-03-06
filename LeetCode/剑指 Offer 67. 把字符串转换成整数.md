---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

写一个函数 StrToInt，实现把字符串转换成整数这个功能。不能使用 atoi 或者其他类似的库函数。

<!--more-->

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

说明：

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 `[−231,  231 − 1]`。如果数值超过这个范围，请返回  `INT_MAX (231 − 1)` 或 `INT_MIN (−231) `。

**示例1：**

```
输入: "42"
输出: 42
```

**示例 2:**

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```


**示例 3:**

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```


**示例 4:**

```
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```


**示例 5:**

```
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题思路比较简单，就直接怎么想的怎么写代码。大体思路就是不断读取每个数字，用一个`result`变量存储结果就行。本题需要注意几个细节：

- 第一个问题就是正负号的问题，因为我们遍历的顺序是从左往右，所以遇到的第一个正负号就是结果的正负，用一个变量来存储，正为`1`，负为`-1`；
- 第二个问题就是越界问题，我们知道`Integer.MAX_VALUE`值为`2147483647`，对这个数除以`10`，然后每次循环判断当前`result`是否大于这个除以`10`后的数字，如果大于直接返回`Integer.MIN_VALUE`，另一种情况就是当前`result`等于这个数除以`10`，那么最后一位就需要判断当前数字是否大于`7`（因为`Integer.MAX_VALUE`最后一位为`7`），如果大于证明越界；
- 第三个问题就是如果当前字符串开始就是字母，那么本题的规则是直接返回0，就是无法构成数字，事实上是减小了题目的难度。

具体代码如下：

```java
class Solution {
    public int strToInt(String str) {
        str = str.trim();
        if (str.length() == 0) return 0;
        char[] chars = str.toCharArray();
        if (chars[0] != '-' && chars[0] != '+' && chars[0] < '0' && chars[0] > '9')
            return 0;
        int negtive = 1;
        int result = 0;
        int boundry = Integer.MAX_VALUE / 10;

        int index = 0;
        while (chars[index] != '-' && chars[index] != '+' && chars[index] > '9' && chars[index] < '0')
            index++;

        if (chars[index] == '-') {
            negtive = -1;
            index++;
        } else if (chars[index] == '+') {
            index++;
        }

        while (index < chars.length && chars[index] >= '0' && chars[index] <= '9') {
            if (result > boundry || (result == boundry && (chars[index] - '0' > 7)))
                return negtive == -1 ? Integer.MIN_VALUE : Integer.MAX_VALUE;
            result *= 10;
            result += chars[index++] - '0';
        }

        return negtive == 1 ? result : -result;
    }
}
```

