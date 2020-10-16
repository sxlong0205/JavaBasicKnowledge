---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

<!--more-->

**示例1 ：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

**限制：**

```
0 <= 链表长度 <= 10000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本来逆序我们可以想到头插法，但是题目要求用数组返回，那我们直接使用栈结构。将`head`所有结点值压入栈，然后将所有结点值出栈，顺序存入数组。

具体代码如下：

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        LinkedList<Integer> result = new LinkedList<>();
        while (head != null) {
            result.addFirst(head.val);
            head = head.next;
        }
        int[] res = new int[result.size()];
        for (int i = 0; i < result.size(); i++) {
            res[i] = result.get(i);
        }
        return res;
    }
}
```

