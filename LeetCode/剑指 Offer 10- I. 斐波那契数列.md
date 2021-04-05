---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项。斐波那契数列的定义如下：

<!--more-->

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```


斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 `1e9+7（1000000007）`，如计算初始结果为：`1000000008`，请返回 `1`。

**示例 1：**

```
输入：n = 2
输出：1
```

**示例 2：**

```
输入：n = 5
输出：5
```

**提示：**

-   `0 <= n <= 100`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

经典问题斐波那契数列，解法分为递归和动态规划的方式，递归没什么意思，直接写即可。动态规划和[509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)思路一样，只不过这里加了一个取模的操作，新瓶装旧酒，万变不离其宗，这里直接给出压缩后的动态规划。

具体代码如下：

```java
class Solution {
    public int fib(int n) {
        if (n < 2) {
            return n;
        }
        int[] dp = new int[]{0, 0, 0};
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[2] = (dp[0] + dp[1]) % 1000000007;
            dp[0] = dp[1];
            dp[1] = dp[2];
        }
        return dp[2];
    }
}
```

