---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

<!--more-->

**示例1：**

```
输入：n = 3
输出：3
```

**示例2：**

```
输入：n = 11
输出：0
```

**限制：**

-   `0 <= n < 2^31`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题要是面试的话临场还真不一定能找出规律，不过鉴于本题规律还算比较简单，可以参考训练自己的思维。通过找规律可以发现，数值为一位的数字一共有9个(1～9)，数值为二位的数字一共有180个(从10～99)，以此类推，最终可以发现规律即为`起始位 * 位数 * 9`，通过该规律，首先可以判断出n是几位数，从而定位到一个区间内。然后通过起始的位置可以计算出n位数对应的数字是多少，最后可以通过计算定位n对应该数字中的第几位，就可以得到结果。

具体代码如下：

```java
class Solution {
    public int findNthDigit(int n) {
        int start = 1;
        long digit = 1;
        long count = 9;
        while (n > count) {
            n -= count;
            digit++;
            start *= 10;
            count = 9 * digit * start;
        }

      	//定位n所指向的数字是多少
        long num = start + (n - 1) / digit;
      	//定位n所指向的数字是第几位
        long reminder = (n - 1) % digit;
        return Long.toString(num).charAt((int)reminder) - '0';

    }
}
```

