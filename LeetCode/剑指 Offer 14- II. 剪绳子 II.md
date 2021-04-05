---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 `m `段（`m`、`n`都是整数，`n>1`并且`m>1`），每段绳子的长度记为 `k[0],k[1]...k[m - 1]` 。请问 `k[0]k[1]...*k[m - 1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为`2、3、3`的三段，此时得到的最大乘积是`18`。

答案需要取模` 1e9+7（1000000007）`，如计算初始结果为：`1000000008`，请返回 `1`。

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

**提示：**

- `2 <= n <= 1000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题和[剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)大同小异，唯一的区别就是防止越界，在每次计算时对结果取模即可。

具体代码如下：

```java
class Solution {
    public int cuttingRope(int n) {
        if (n == 2 || n == 3)
            return n - 1;

        long result = 1;
        while (n > 4) {
            n = n - 3;
            result = (result * 3) % 1000000007;
        }
        return (int) (n * result % 1000000007);
    }
}
```

