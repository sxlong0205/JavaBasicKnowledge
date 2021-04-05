---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [[剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)](https://leetcode-cn.com/problems/qiu-12n-lcof/)

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

<!--more-->

**示例：**

```
输入: a = 1, b = 1
输出: 2
```

**提示：**

-   `a`, `b` 均可能是负数或 0
-   结果不会溢出 32 位整数

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

这个其实就是位运算，如果计算机组成原理的话，我们可以在大脑里模拟加法器的工作流程，需要考虑进位情况。通过真值表可以发现，两个二进制数相加时，如果不出现进位情况，那么结果应该是两个数的异或运算，如果有进位时，是两个数的与运算，但是进位需要进行特殊处理，也就是需要左移一位。

具体代码如下：

```java
class Solution {
    public int add(int a, int b) {
        while (b != 0) {
            int temp = (a & b) << 1;
            a ^= b;
            b = temp;
        }
        return a;
    }
}
```

