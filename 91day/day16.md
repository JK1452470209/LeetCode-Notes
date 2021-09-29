#### [513. 找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)

难度中等200

给定一个二叉树的 **根节点** `root`，请找出该二叉树的 **最底层 最左边** 节点的值。

假设二叉树中至少有一个节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree1.jpg)

```
输入: root = [2,1,3]
输出: 1
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree2.jpg)

```
输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7
```

 

**提示:**

- 二叉树的节点个数的范围是 `[1,104]`
- `-231 <= Node.val <= 231 - 1` 

**思路**

bfs获取每层信息，如果不为空则取最后一层的第一个节点值

**代码**

```java
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        if(root == null){
            return 0;
        }
        LinkedList<TreeNode> queue = new LinkedList<>();
        int num = 0;
        queue.offer(root);
        while(!queue.isEmpty()){
            num = queue.peek().val;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode cur = queue.poll();
                if(cur.left != null){
                    queue.offer(cur.left);
                }
                if(cur.right != null){
                    queue.offer(cur.right);
                }
            }
        }
        return num;
    }
}
```

**复杂度**

时间复杂度：O(N),N为树节点数量

空间复杂度：O(Q),Q为队列最大长度



**思路**

dfs记录树的深度，到达每次最新的一层将节点更新，则就是树的最底层第一个节点

**代码**

```java
class Solution {
    public int ans = 0;
    public int maxDeep = -1;
    public int findBottomLeftValue(TreeNode root) {
        if(root == null){
            return 0;
        }
        dfs(root,0);
        return ans;
    }
    private void dfs(TreeNode root,int deep){
        if(root == null){
            return;
        }
        if (maxDeep < deep){
            maxDeep = deep;
            ans = root.val;
        }
        dfs(root.left,deep + 1);
        dfs(root.right,deep + 1);
        
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度: O(logN)