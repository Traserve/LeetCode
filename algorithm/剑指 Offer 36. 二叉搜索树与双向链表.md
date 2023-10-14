# 剑指 Offer 36. 二叉搜索树与双向链表

[题目链接](https://leetcode.cn/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

为了让您更好地理解问题，以下面的二叉搜索树为例：

![img](images/bstdlloriginalbst.png)

 

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

![img](images/bstdllreturndll.png)

 

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。

## 解法

二叉搜索树中序遍历升序。

```java
class Solution {

    Node pre = null, head = null;
    public Node treeToDoublyList(Node root) {
        if (root == null) {
            return null;
        }
        traversal(root);
        // 首尾相连
        head.left = pre;
        pre.right = head;
        return head;
    }

    public void traversal(Node root) {
        if (root == null) {
            return;
        }
        traversal(root.left);
        // 中序遍历处理
        if (pre == null) {
            head = root;
        } else {
            pre.right = root;
        }
        root.left = pre;
        pre = root;
        traversal(root.right);
    }
}
```

