---
zmathjax: true
toc: true
categories:
 - LeetCode
tags:
 - 刷题笔记
---

#### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

<!--more-->

**示例1：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e1.png)

```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**示例2：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e2.png)

```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

**示例3：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e3.png)

```
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

**示例4：**

```
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```

**提示：**

-   `-10000 <= Node.val <= 10000`
-   `Node.random` 为空（null）或指向链表中的节点。
-   节点数目不超过 1000 。

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解：

本题解法五花八门，我在这里提供一种思路最简单的方法，就是利用`HashMap`。我们首先遍历一次链表，将每个结点复制一个相同的新结点并存入`HashMap`中，其中`Key`为原结点，`Value`为原结点的复制结点，第一遍遍历不用管每个结点的`next`和`random`指针。第二遍遍历链表，我们要利用每个原结点的`next`和`random`指针信息来完善新的复制链表，其中，新结点的`next`指向的就是原始结点`next`指向的结点对应的复制结点，即`map.get(p).next = map.get(p.next);`，新结点的`random`指向的就是原始结点的`random`所对应的复制结点，即`map.get(p).random = map.get(p.random);`最后我们返回`HashMap`中`head`对应的`Value`，即新的复制链表的头结点。

具体代码如下：

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null)
            return head;

        Node p = head;
      	//创建HashMap用来存放原始链表和新链表的对应关系
        Map<Node, Node> map = new HashMap<>();
        while (p != null) {
            Node temp = new Node(p.val);
          	//将每个原始结点拷贝一份，其中原始结点作为Key，复制结点作为Value
            map.put(p, temp);
            p = p.next;
        }

        p = head;
        while (p != null) {
          	//新结点的next就是原结点next指向的结点的复制结点
            map.get(p).next = map.get(p.next);
          	//新结点的random结点就是原始结点random指向的结点的复制结点
            map.get(p).random = map.get(p.random);
            p = p.next;
        }
				//返回新链表的头结点即可
        return map.get(head);
    }
}
```

