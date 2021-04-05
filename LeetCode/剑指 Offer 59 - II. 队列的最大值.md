---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的均摊时间复杂度都是`O(1)`。

若队列为空，`pop_front` 和 `max_value` 需要返回 `-1`

<!--more-->

**示例1：**

```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```

**示例 2：**

```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

**限制：**

- `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
- `1 <= value <= 10^5`

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

我觉得这道题出的不够好，为了考双端队列而使用双端队列。具体思路和[剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)一毛一样，一共有两个队列，一个是普通的队列，用以存放push_back的数字，实现push_back和pop_front操作，另一个采用单调队列的思想，维护一个递减序列，每次取最大值就让队头元素出队，每次push_back的元素和队尾元素比较，如果push_back元素大于队尾元素，让队列右端元素出队直到push_back元素小于队尾元素，然后将push_back元素入队。

具体代码如下：

```java
class MaxQueue {
    Deque<Integer> maxQueue;
    Deque<Integer> normalQueue;

    public MaxQueue() {
        maxQueue = new ArrayDeque<>();
        normalQueue = new ArrayDeque<>();
    }
    
    public int max_value() {
        return maxQueue.isEmpty() ? -1 : maxQueue.peekFirst();
    }
    
    public void push_back(int value) {
        while (!maxQueue.isEmpty() && value > maxQueue.peekLast()) {
            maxQueue.pollLast();
        }
        maxQueue.offerLast(value);
        normalQueue.offerLast(value);
    }
    
    public int pop_front() {
        if (normalQueue.isEmpty()) {
            return -1;
        }
        int temp = normalQueue.pollFirst();
        if (temp == maxQueue.peekFirst())
            maxQueue.pollFirst();
        return temp;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

