#### [876. 链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

难度简单413

给定一个头结点为 `head` 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

 

**示例 1：**

```
输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
```

**示例 2：**

```
输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。
```

 

**提示：**

- 给定链表的结点数介于 `1` 和 `100` 之间。

**思路**

先计算链表总长度，再用长度定位到链表的中间并返回

**代码**

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        int index = 1;
        ListNode cur = head;
        while(cur.next != null){
            cur = cur.next;
            index++;
        }
        for(int i = 0; i < index / 2; i++){
            head = head.next;
        }
        return head;
    }
}
```

**复杂度**

时间复杂度：O(N)，N为链表长度

空间复杂度：O(1)

**思路**

快慢指针法，快指针步长为2 慢指针步长为1，快指针走到终点时，慢指针就是中点

**代码**

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)