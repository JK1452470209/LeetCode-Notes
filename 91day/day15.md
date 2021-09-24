#### [129. 求根节点到叶节点数字之和](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)

难度中等423收藏分享切换为英文接收动态反馈

给你一个二叉树的根节点 `root` ，树中每个节点都存放有一个 `0` 到 `9` 之间的数字。

每条从根节点到叶节点的路径都代表一个数字：

- 例如，从根节点到叶节点的路径 `1 -> 2 -> 3` 表示数字 `123` 。

计算从根节点到叶节点生成的 **所有数字之和** 。

**叶节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

```
输入：root = [1,2,3]
输出：25
解释：
从根到叶子节点路径 1->2 代表数字 12
从根到叶子节点路径 1->3 代表数字 13
因此，数字总和 = 12 + 13 = 25
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg)

```
输入：root = [4,9,0,5,1]
输出：1026
解释：
从根到叶子节点路径 4->9->5 代表数字 495
从根到叶子节点路径 4->9->1 代表数字 491
从根到叶子节点路径 4->0 代表数字 40
因此，数字总和 = 495 + 491 + 40 = 1026
```

 

**提示：**

- 树中节点的数目在范围 `[1, 1000]` 内
- `0 <= Node.val <= 9`
- 树的深度不超过 `10`

**思路**

使用dfs一直在纠结如何将值往下传递，尝试了很久用set<string>存然后转换。看了题解 ...太绝了

**代码**

```java
class Solution {
    public int ans;

    public int sumNumbers(TreeNode root) {
        dfs(root,0);
        return ans;
    }

    private void dfs(TreeNode root,int last){
       if (root == null){
           return;
       }
       if(root.left == null && root.right == null){
           ans += last * 10 + root.val;
       }
       dfs(root.left,last * 10 + root.val);
       dfs(root.right,last * 10 + root.val);
    }
}
```

**复杂度**

时间复杂度：O(N),N为节点数

空间复杂度：O(h),h为树的高度



**思路**

bfs解法 每次更新每次的val值，遇到叶子节点时加到sum中

**代码**

```java
class Solution {

    public int ans;

    public int sumNumbers(TreeNode root) {

        if (root == null){
            return 0;
        }
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()){
            TreeNode cur = queue.poll();
            if (cur.left == null && cur.right == null){
                ans += cur.val;
            }
            if (cur.left != null){
                cur.left.val = cur.val * 10 + cur.left.val;
                queue.offer(cur.left);
            }
            if (cur.right != null){
                cur.right.val = cur.val * 10 + cur.right.val;
                queue.offer(cur.right);
            }
        }
        return ans;
    }
}
```

**复杂度**

时间复杂度：O(N),N为节点数量

空间复杂度：O(Q),Q为队列最大长度