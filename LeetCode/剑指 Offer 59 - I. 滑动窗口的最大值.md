---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

<!--more-->

**示例：**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**提示：**

你可以假设 *k* 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题因为暴力解法会在[239. 滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)中超时，所以只讲解单调栈策略。一看题目，每次都需要返回一个区间内的最大值，我们自然而然会想到大顶堆，但是大顶堆有个问题就是不能反映窗口滑动的过程，即窗口向右移动，无法删除窗口左边划出的元素。

所以本题要用一种特殊的数据结构——双端队列，我们每次向队列右端添加数字，需要满足以下条件：当前`nums[i]`小于队列中最右端的元素，如果`nums[i]`大于队列中最右端的元素，则需要将队列中右端元素从右边出队，即要保证队列中元素是一个递减序列。然后取出队头元素，即队列中最左端的元素加入结果数组中。最后，需要判断划出窗口的元素是否是当前队列的队头，即是否是当前队列中的最大元素，如果是，需要将队头元素从队列左端出队。一开始时，我们需要通过第一步的条件依次向队列中加入`k`个元素。

具体代码如下：

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums.length == 0 || k == 0) return new int[]{};

        int[] result = new int[nums.length - k + 1];
        Deque<Integer> deque = new ArrayDeque<>();

        for (int i = 0, index = 0; i < nums.length && index < result.length; i++) {
            //如果当前元素大于队列中最右端元素，队列右端元素出队，直到nums[i] <= deque.peekLast()
            while (!deque.isEmpty() && nums[i] > deque.peekLast()) {
                deque.pollLast();
            }
            //将当前元素加入队列
            deque.offerLast(nums[i]);

            //如果满足窗口大小的情况下
            if (i >= k - 1) {
                //将队头元素添加到结果数组中
                result[index++] = deque.peekFirst();

                //nums[i - k + 1]即为窗口左端划出的元素值
                if (!deque.isEmpty() && nums[i - k + 1] == deque.peekFirst()) {
                    deque.pollFirst();
                }
            }
        }
        return result;
    }
}
```

