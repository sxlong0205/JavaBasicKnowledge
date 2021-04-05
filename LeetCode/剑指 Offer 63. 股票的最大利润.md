---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 63. 股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

<!--more-->

**示例1：**

```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2：**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

**限制：**

```
0 <= 数组长度 <= 10^5
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

经典的买股票问题，经典的动态规划。但这次我们换个思路，设置两个变量，一个表示当前获得利润的最大值，一个表示当前获得利润的最小值，我们遍历整个数组，每次判断获取已遍历数组的最小股票价值，然后用当前价格减去最小股票价值，判断能够获取的最大利润是多少。

具体代码如下：

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int minProfit = Integer.MAX_VALUE;
        
        for (int i = 0; i < prices.length; i++) {
            if (minProfit > prices[i]) {
                minProfit = prices[i];
            }
            
            if (prices[i] - minProfit > maxProfit) {
                maxProfit = prices[i] - minProfit;
            }
        }
        
        return maxProfit;
    }
}
```

