---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 `min` 函数在该栈中，调用 `min`、`push` 及 `pop` 的时间复杂度都是 `O(1)`。

<!--more-->

**示例：**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

**提示：**

1. 各函数的调用总次数不超过 20000 次

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题可能一看到题目，有可能会想到利用`PriorityQueue`来解决问题，但是`PriorityQueue`无法同时满足返回最小和栈结构。本题可以创建一个辅助栈专门存放当前最小的元素，返回栈中最小的元素直接操作最小栈中的元素即可，其他的操作按照正常的栈来操作。用不同的集合类可能会造成时间复杂度上的差异，这里使用`Deque`。

具体代码如下：

```java
class MinStack {
    Deque<Integer> stack;
    Deque<Integer> minStack;

    public MinStack() {
        stack = new ArrayDeque();
        //存放当前栈中最小元素的栈
        minStack = new ArrayDeque();
        minStack.push(Integer.MAX_VALUE);
    }

    public void push(int x) {
        stack.push(x);
        //每次push操作中minStack压入当前栈中最小的元素
        minStack.push(Math.min(minStack.peek(), x));
    }

    public void pop() {
        stack.pop();
        minStack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int min() {
        return minStack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.min();
 */
```



