---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

输入两个链表，找出它们的第一个公共节点。

如下面的两个链表**：**

![img](https://gitee.com/xlshi/blog_img/raw/master/mac/20201210200854.png)

在节点 c1 开始相交。

<!--more-->

**示例 1：**

![img](https://gitee.com/xlshi/blog_img/raw/master/mac/20201210200858.png)

```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

**示例 2：**

![img](https://gitee.com/xlshi/blog_img/raw/master/mac/20201210200908.png)

```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

**示例 3：**

![img](https://gitee.com/xlshi/blog_img/raw/master/mac/20201210200904.png)

```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```

**注意：**

-   如果两个链表没有交点，返回 null.
-   在返回结果后，两个链表仍须保持原有的结构。
-   可假定整个链表结构中没有循环。
-   程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题是左神讲过的原题，要判断两个链表是否相交，就需要消除两个链表的长度差(如果两链表长度相等可以忽略这一步)，具体做法就是定义两个指针分别指向两个链表，如果两个指针所指的当前结点不想等，则向后遍历。如果其中一个指针指向了链表的尾部，这时候另一个指针一定指向的是较长链表，我们把指向空的指针重新指向**长链表**的头结点(注意这里是指向长链表的头结点，即现在两个指针指向同一个链表)，然后再让两个指针一次一步继续向后走，当最开始指向长链表的指针到链表尾部的时候，将它指向短链表的头结点。此刻，两个指针交换了最初指向的链表，而且从此刻开始出发的话，两个指针距离链表尾部的距离是一样的，然后两个指针都向后遍历，如果遇到相等的结点，则证明两个链表相交，如果不相等则不相交。

具体代码如下：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1 = headA, p2 = headB;

        while (p1 != p2) {
            p1 = p1 == null ? headB : p1.next;
            p2 = p2 == null ? headA : p2.next;
        }

        return p1;
    }
}
```

