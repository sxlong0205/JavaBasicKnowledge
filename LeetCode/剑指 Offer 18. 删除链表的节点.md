---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

**注意：**此题对比原题有改动

<!--more-->

**示例1 ：**

```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

**示例2:**

```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

**说明：**

- 题目保证链表中节点的值互不相同
- 若使用 C 或 C++ 语言，你不需要 `free` 或 `delete` 被删除的节点

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题思想很简单，就是线性遍历整个链表，遇到与目标值相等的结点，直接删除即可。这里需要注意一种情况，就是`head`结点对应的值就是要删除的值，这时候我们直接返回`head.next`。

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
    public ListNode deleteNode(ListNode head, int val) {
        ListNode pre = new ListNode(0);
        ListNode curr = head;
        pre.next = head;

        if (head.val == val){
            return head.next;
        }
        
        while (curr != null) {
            if (curr.val == val) {
                pre.next = curr.next;
                break;
            } else {
                curr = curr.next;
                pre = pre.next;
            }
        }
        return head;
    }
}
```

还有一种递归删除方法。

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
    public ListNode deleteNode(ListNode head, int val) {
        if (head == null)
            return null;
        if (head.val == val) {
            return head.next;
        }

        head.next = deleteNode(head.next, val);
        return head;
    }
}
```

