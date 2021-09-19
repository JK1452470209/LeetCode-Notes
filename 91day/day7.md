#### [61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/)

难度中等628收藏分享切换为英文接收动态反馈

给你一个链表的头节点 `head` ，旋转链表，将链表每个节点向右移动 `k` 个位置。

```
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
示例 2:

输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

**思路**

用快慢指针找出分界点k的位置，把k的next指向null，将链表断开。将尾结点的next指向head 然后返回k+1节点的位置，链表走到k.next就停下来了

刚开始就想到了使用快慢指针可以找出节点位置，但是将链表定位后一直在纠结着如何将链表拼起来。后来看了题解之后才理解到了其实只有一个链表，但是存在着操作的4个指针。应用传递！！！

**代码**

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || head.next == null) return head;
        ListNode tempNode = head;
        ListNode fast = head,slow = head;
        int index = 1;
        while (tempNode.next != null){
            index++;
            tempNode = tempNode.next;
        }
        //取模
        int count = (k >= index) ? (k % index) : k;
        for (int i = 0; i < count; i++) {
            fast = fast.next;
        }
        //快慢指针
        while (fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        fast.next = head;
        tempNode = slow.next;
        slow.next = null;

        return tempNode;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)