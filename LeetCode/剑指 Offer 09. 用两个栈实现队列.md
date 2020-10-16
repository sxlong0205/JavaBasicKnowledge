---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail `和 `deleteHead `，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead `操作返回 -1 )

<!--more-->

**示例1 ：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```

**示例2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**限制：**

- `1 <= values <= 10000`
- 最多会对 `appendTail`、`deleteHead` 进行 `10000` 次调用

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题要求用栈实现队列，我们可以想象，把栈底看成是队列的头，那么我们每次进行压栈操作，就相当于从队尾添加元素。出队操作需要另一个栈来辅助进行，我们可以将`stack1`的元素依次弹出并压入`stack2`，这样，在`stack2`进行`pop`操作时，就可以实现出队功能，另外，如果将`stack1`元素全部压入`stack2`后`stack2`还为空，那么说明队列中没有元素，即返回`-1`。

具体代码如下：

```java
class CQueue {
    //初始化两个栈
    LinkedList<Integer> stack1;
    LinkedList<Integer> stack2;

    public CQueue() {
        stack1 = new LinkedList<>();
        stack2 = new LinkedList<>();
    }

    //入队操作直接就将元素压入stack1即可
    public void appendTail(int value) {
        stack1.push(value);
    }

    public int deleteHead() {
        //如果stack2为空，则将stack1中的元素全部压入stack2
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        //将stack1中元素全部压入stack2中后，stack2依然为空则返回-1，若不为空则返回栈顶元素
        if (stack2.isEmpty())
            return -1;
        else
            return stack2.pop();
    }
}
```

