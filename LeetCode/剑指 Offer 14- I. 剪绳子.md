---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（`m、n`都是整数，`n > 1`并且`m > 1`），每段绳子的长度记为 `k[0],k[1]...k[m-1]` 。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是`8`时，我们把它剪成长度分别为`2、3、3`的三段，此时得到的最大乘积是`18`。

<!--more-->

**示例1 ：**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

**示例2：**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

**说明:** 你可以假设 `n` 不小于 `2` 且不大于 `58`。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题根据提示，需要用到动态规划，那么我们首先就需要找出状态转移方程。我们用`dp`数组来存储两个数的乘积，这个乘积分为两种情况，第一种情况就是，`i`被拆为`i`和`i-j`，那乘积就是`i`和`i-j`的乘积，另一种情况就是，拆分出`j`后还需要对剩下的`i-j`再次进行拆分，所以乘积就是`j`和`dp[i-j]`的乘积。通过以上分析我们就可以列出状态转移方程：
$$
dp[i] = Math.max(j * (i-j),j * dp[i-j])
$$
我们遍历从`0`到`n`的数，就可以得出结果。

具体代码如下：

```java
class Solution {
    public int integerBreak(int n) {
        if (n == 0)
            return 0;
        int[] dp = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            int curMax = 0;
            for (int j = 1; j < i; j++) {
                curMax = Math.max(curMax, Math.max(j * (i - j), j * dp[i - j]));
            }
            dp[i] = curMax;
        }
        return dp[n];
    }
}
```

本题也可以用数学方法来解决，可以知道，和一定，两个数字相差越小，乘积越大，举个例子，`x + y = 10`，当`x = 2, y = 8`时， `x * y = 16`，当`x = 5, y = 5`时，`x * y = 25`，所以我们取尽量接近的数字连乘，得到的结果最大。我们假设取每段相等，则乘积`y`有：
$$
y  = (\frac{n}{x})^x
$$
对两边取对数：
$$
lny = x \times \frac{n}{x}
$$
两边对`x`求导：
$$
y' \times \frac{1}{y} = ln \frac{n}{x} + x \times \frac{x}{n}(- \frac{n}{x^2}) \\
y' = (ln \frac{x}{n} - 1) \times (\frac{n}{x})^x
$$
令$y' = 0$，可得$x = \frac{n}{e}$，也就是当每段取$e$时，乘积最大，但是因为要取整数，取`3`最合适。

具体代码如下：

```java
class Solution {
    public int cuttingRope(int n) {
        //长度为2或3只有一种情况
        if (n == 2 || n == 3)
            return n - 1;
        //如果是三的倍数，直接就是三的指数
        if (n % 3 == 0) {
            return (int) Math.pow(3, n / 3);
        } else if (n % 3 == 1) { //如果余1就单另出来一个长度为4的绳子
            return (int) (4 * Math.pow(3, (n - 4) / 3));
        } else { //n对3取模余2的情况
            return (int) (2 * Math.pow(3, (n - 2) / 3));
        }
    }
}
```

