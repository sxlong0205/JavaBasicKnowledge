---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

一只青蛙一次可以跳上`1`级台阶，也可以跳上`2`级台阶。求该青蛙跳上一个` n` 级的台阶总共有多少种跳法。

答案需要取模 `1e9+7（1000000007）`，如计算初始结果为：`1000000008`，请返回` 1`。

<!--more-->

**示例1 ：**

```
输入：n = 2
输出：2
```

**示例2：**

```
输入：n = 7
输出：21
```

**示例3：**

```
输入：n = 0
输出：1
```

**提示：**

- `0 <= n <= 100`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题思路和[剑指 Offer 10- I. 斐波那契数列](https://zhuanlan.zhihu.com/p/201474492)如出一辙，都是斐波那契数列的应用，与[剑指 Offer 10- I. 斐波那契数列](https://zhuanlan.zhihu.com/p/201474492)不同的是，本题是从斐波那契数列第三个索引上的值开始的，我们依旧利用动态规划进行计算。

具体代码如下：

```java
class Solution {
    public int numWays(int n) {
        if (n == 0)
            return 1;
        if (n <= 2)
            return n;

        int[] dp = new int[]{0, 0, 0};
        dp[0] = 1;
        dp[1] = 2;
        for (int i = 2; i < n; i++) {
            dp[2] = (dp[0] + dp[1]) % 1000000007;
            dp[0] = dp[1];
            dp[1] = dp[2];
        }
        return dp[2];
    }
}
```

