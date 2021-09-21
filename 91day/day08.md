#### [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

难度中等1048收藏分享切换为英文接收动态反馈

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

**示例 2：**

```
输入：head = []
输出：[]
```

**示例 3：**

```
输入：head = [1]
输出：[1]
```

 

**提示：**

- 链表中节点的数目在范围 `[0, 100]` 内
- `0 <= Node.val <= 100`

 

**进阶：**你能在不修改链表节点值的情况下解决这个问题吗?（也就是说，仅修改节点本身。）



**思路**

主要细节在于反转之后还要将前后节点连接起来，保证顺序问题  移动指针时要往后移动俩位

**代码**

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }
        ListNode nodeRet = head.next;
        ListNode nodePre = new ListNode(-1,head);
        ListNode firstNode = head;
        ListNode secondNode;
        ListNode nextNode;
        while (firstNode != null && firstNode.next != null){    
             //赋值
             secondNode = firstNode.next;
             nextNode = secondNode.next;
             
             //反转
             firstNode.next = nextNode;
             secondNode.next = firstNode;
             nodePre.next = secondNode;
             
             //移动指针
             nodePre = firstNode;
             firstNode = nextNode;
        }

        return nodeRet;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(N)