#### [109. 有序链表转换二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)

难度中等587收藏分享切换为英文接收动态反馈

给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```



**思路**

昨晚数组的题目的转换之后，做链表的思路变得比较清晰。在使用快慢指针寻找中点时需要在细节上需要有些调整。

**代码**

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null){
            return null;
        }
        return dfs(head, null);
    }
    private TreeNode dfs(ListNode head,ListNode tail){
        if (head == tail){
            return null;
        }
        ListNode fast = head,slow = head;
        while (fast != tail && fast.next != tail){
            fast = fast.next.next;
            slow = slow.next;
        }

        TreeNode root = new TreeNode(slow.val);
        root.left = dfs(head,slow);
        root.right = dfs(slow.next,tail);
        return root;
    }
}
```

**复杂度**

时间复杂度：O(nlogn)

空间复杂度：O(logn)