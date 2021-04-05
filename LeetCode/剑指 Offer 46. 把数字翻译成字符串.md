---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

<!--more-->

**示例1：**

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

由于一共二十六个字母，所以最大可翻译的字母就是`a~z`，最大可翻译位数为两位，所以最多需要考虑的就是两位，也就是说，我们当前位置能翻译的字符串个数，最多只和前两个位置的数有关系。由这点，就可以想到动态规划的方法，一共有两种情况，当前数字自己可以翻译成一种字母；以及当前数字和前一个数字组合起来可以翻译成一种字母，就是说，当前位置能翻译字母的组合个数为两种情况之和。需要注意的是，一共只有二十六个字母，所以数字能翻译的范围是`0~25`，超过这个范围将不能被视为是一种翻译。

具体代码如下：

```java
class Solution {
    public int translateNum(int num) {
        String n = String.valueOf(num);
        int[] dp = new int[n.length()];
        dp[0] = 1;
        for (int i = 1; i < n.length(); i++) {

            int temp = (n.charAt(i - 1) - '0') * 10 + (n.charAt(i) - '0');

            if (temp >= 10 && temp <= 25) {
                if (i == 1)
                    //开始特殊值处理
                    dp[i] = 2;
                else
                    dp[i] = dp[i - 1] + dp[i - 2];
            } else {
                dp[i] = dp[i - 1];
            }
        }
        return dp[n.length() - 1];
    }

}
```

因为当前位置只和前两个位置有关，所以可以压缩空间。

具体代码如下：

```java
class Solution {
    public int translateNum(int num) {
        String n = String.valueOf(num);
        int curr = 1;
        int pre = 1;
        for (int i = 2; i <= n.length(); i++) {

            int temp = (n.charAt(i - 2) - '0') * 10 + (n.charAt(i - 1) - '0');

            if (temp >= 10 && temp <= 25) {
                int t = curr;
                curr += pre;
                pre = t;
            } else {
                pre = curr;
            }
        }
        return curr;
    }
}
```

还有大佬想出了递归的方法，具体来说，因为最多只和两位数字有关，我们可以一次递归两个分支，一个分支只考虑一个位置的情况，另一个分支考虑两个位置的情况。

具体代码如下：

```java
class Solution {
    public int translateNum(int num) {
        //结束条件
        if (num < 10)
            return 1;

        //取出两位数字，如果在翻译范围内，分别递归一位和两位的情况，如果不在只需要递归一位
        int temp = num % 100;
        if (temp < 10 || temp > 25)
            return translateNum(num / 10);
        else
            return translateNum(num / 10) + translateNum(num / 100);
    }
}
```



