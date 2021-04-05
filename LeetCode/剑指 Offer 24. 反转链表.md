---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

<!--more-->

**示例 ：**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

**限制：**

```
0 <= 节点个数 <= 5000
```

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题最直观的想法就是修改每个节点的指向，让后一个节点的`next`指针指向前一个节点，但是因为让后一个节点指向前一个节点会造成链表断掉，所以我们还需要一个临时节点存储当前节点。每次将`curr`和`pre`向后移动，将当前节点用临时节点存储起来，当前节点的`next`指向`pre`，依次遍历整个链表

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
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode temp = curr;
            curr = curr.next;
            temp.next = pre;
            pre = temp;
        }
        return pre;
    }
}
```

递归方法的思想就是依次递归到链表的尾部，然后依次将当前节点的`head.next.next = head`，然后将`head.next = null`即可

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
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null)
            return head;

        ListNode temp = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return temp;
    }
}
```

