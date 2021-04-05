---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

<!--more-->

**示例1 ：**

```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

**示例2:**

```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

**限制：**

-   `0 <= k <= arr.length <= 10000`
-   `0 <= arr[i] <= 10000`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题提供两种解法，要取出最小的k个数，先对数组进行排序，然后返回前k个数即可。

具体代码如下：

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        Arrays.sort(arr);
        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = arr[i];
        }
        return result;
    }
}
```

另一种方法就是利用大顶堆，先将数组中的`k`个数入堆，然后遍历数组中后面的数，如果当前数值小于堆顶元素，直接将堆顶元素弹出，然后将当前数压入堆，这样，堆中始终维护的是数组中最小的`k`个数，最后直接返回即可。

具体代码如下：

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        int[] result = new int[k];
        if (k == 0)
            return result;
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>((o1, o2) -> o2 - o1);
        for (int i = 0; i < k; i++) {
            priorityQueue.add(arr[i]);
        }

        for (int i = k; i < arr.length; i++) {
            if (arr[i] < priorityQueue.peek()) {
                priorityQueue.poll();
                priorityQueue.add(arr[i]);
            }
        }


        for (int i = 0; i < k; i++) {
            result[i] = priorityQueue.poll();
        }
        return result;
    }
}
```





