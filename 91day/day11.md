#### [142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

难度中等1179

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。**注意，pos 仅仅是用于标识环的情况，并不会作为参数传递到函数中。**

**说明：**不允许修改给定的链表。

**进阶：**

- 你是否可以使用 `O(1)` 空间解决此题？



**思路**

哈希表判断是否有环

**代码**

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        HashMap<ListNode, Object> map = new HashMap<>();
        while (head != null){
            if (map.containsKey(head)){
                return head;
            }
            map.put(head,null);
            head = head.next;
        }
        return null;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(N)

**思路**

快慢指针法，快指针每次走俩步，慢指针每次走一步 等到快慢指针相遇时，把慢指针移动到链表头，以相同步长向下走，相遇时就是环的入口

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head,slow = head;
        while (fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow){
                slow = head;
                while (fast != slow){
                    fast = fast.next;
                    slow = slow.next;
                }
                return slow;
            }
        }
        
        return null;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)