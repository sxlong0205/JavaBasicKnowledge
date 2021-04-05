---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

输入一个链表，输出该链表中倒数第`k`个节点。为了符合大多数人的习惯，本题从`1`开始计数，即链表的尾节点是倒数第`1`个节点。例如，一个链表有`6`个节点，从头节点开始，它们的值依次是`1、2、3、4、5、6`。这个链表的倒数第`3`个节点是值为`4`的节点。

<!--more-->

**示例 ：**

```
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题我们创建两个指针，让`fast`指针先走`k`步，然后`fast`和`slow`每次走一步直到`fast`走到链表尾部，此时`slow`指向的下个元素就是目标链表的头结点。其中我们加入了`dummy`结点方便操作。

具体代码如下：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = dummy;
        for (int i = 0; i < k; i++) {
            fast = fast.next;
        }

        ListNode slow = dummy;
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }

        return slow.next;
    }
}
```

