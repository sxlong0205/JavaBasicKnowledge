---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

<!--more-->

**示例1：**

```
输入: n = 3
输出: 6
```

**示例 2：**

```
输入: n = 9
输出: 45
```

**限制：**

-   `1 <= n <= 10000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题直观来做很简单，但是加了条条框框的限制，就不太好想。具体来说，我们可以采用递归的思想，先递归到最深处，即 n = 1的情况，然后向回递归，举例来说，比如 1 + 2 + 3 + 4 + 5的和就是先递归到最深处 5 -> 4 -> 3 -> 2 -> 1，然后返回，让返回结果加上当前值，即 1 -> 2 -> 3 -> 4 -> 5。

具体代码如下：

```java
class Solution {
    public int sumNums(int n) {
        boolean flag = n > 0 && (n += sumNums(n - 1)) > 0;
        return n;
    }
}
```

