#### [100. 相同的树](https://leetcode-cn.com/problems/same-tree/)

难度简单686收藏分享切换为英文接收动态反馈

给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

示例 1：


输入：p = [1,2,3], q = [1,2,3]
输出：true
示例 2：


输入：p = [1,2], q = [1,null,2]
输出：false
示例 3：


输入：p = [1,2,1], q = [1,1,2]
输出：false


提示：

两棵树上的节点数目都在范围 [0, 100] 内
-104 <= Node.val <= 104

**思路**

dfs 对左右节点需使用&&操作 只有其中有一个false则不成立。分解为子问题，相同的树分解为左子是否相同，右子是否相同

**代码**

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {

        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        if (p.val != q.val) return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

**复杂度**

时间复杂度：O(N),N为树的节点数量

空间复杂度：O(h)，h为树的高度



**思路**

bfs 层次遍历。去查看树的每层结构是否相同。可以借助队列实现层次遍历，在每次取队头元素的时候比较俩颗树的队头是否一致。如果不一致，直接返回false。访问完都没有发现不一致就是true

**代码**

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null){
            return true;
        }
        if (p == null || q == null){
            return false;
        }
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.offer(p);
        queue.offer(q);
        while (!queue.isEmpty()){
            TreeNode first = queue.poll();
            TreeNode second = queue.poll();
            if (first == null && second == null){
                continue;
            }
            if (first == null || second == null){
                return false;
            }
            if (first.val != second.val){
                return false;
            }
            queue.offer(first.left);
            queue.offer(second.left);
            queue.offer(first.right);
            queue.offer(second.right);
        }
        return true;
    }
}
```



**复杂度**

时间复杂度：O(N)

空间复杂度：O(Q),Q为队列长度的最大值



