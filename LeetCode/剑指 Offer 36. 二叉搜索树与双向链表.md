---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

<!--more-->

为了让您更好地理解问题，以下面的二叉搜索树为例：

![](https://assets.leetcode.com/uploads/2018/10/12/bstdlloriginalbst.png)

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

![](https://assets.leetcode.com/uploads/2018/10/12/bstdllreturndll.png)

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题要将二叉搜索树变成一个有序的循环双向链表，一提到二叉搜索的有序，一般都是中序遍历，中序遍历可以使二叉搜索树升序排列。然后只需要在每次中序遍历过程中将当前结点的前驱和后继结点相连即可。最后根据题目要求，最后一个结点的后继是头结点，头结点的前驱是最后一个结点，即首位相连。

具体代码如下：

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    Node pre = null, head = null;

    public Node treeToDoublyList(Node root) {
        if (root == null) return root;
        inOrder(root);
        head.left = pre;
        pre.right = head;
        return head;
    }

    private void inOrder(Node curr) {
        if (curr == null)
            return;
        inOrder(curr.left);
      	//如果pre指向为空，即当前结点为头结点，直接让curr指向头结点即可
      	//如果不为空，则让pre的后继指向当前结点即可
        if (pre == null) {
            head = curr;
        } else {
            pre.right = curr;
        }
      	//curr的前驱为pre，同时pre前移
        curr.left = pre;
        pre = curr;
        inOrder(curr.right);
    }
}
```

