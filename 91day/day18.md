#### [987. 二叉树的垂序遍历](https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/)

难度困难159收藏分享切换为英文接收动态反馈

给你二叉树的根结点 `root` ，请你设计算法计算二叉树的 **垂序遍历** 序列。

对位于 `(row, col)` 的每个结点而言，其左右子结点分别位于 `(row + 1, col - 1)` 和 `(row + 1, col + 1)` 。树的根结点位于 `(0, 0)` 。

二叉树的 **垂序遍历** 从最左边的列开始直到最右边的列结束，按列索引每一列上的所有结点，形成一个按出现位置从上到下排序的有序列表。如果同行同列上有多个结点，则按结点的值从小到大进行排序。

返回二叉树的 **垂序遍历** 序列。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/29/vtree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[9],[3,15],[20],[7]]
解释：
列 -1 ：只有结点 9 在此列中。
列  0 ：只有结点 3 和 15 在此列中，按从上到下顺序。
列  1 ：只有结点 20 在此列中。
列  2 ：只有结点 7 在此列中。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/29/vtree2.jpg)

```
输入：root = [1,2,3,4,5,6,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
列 -2 ：只有结点 4 在此列中。
列 -1 ：只有结点 2 在此列中。
列  0 ：结点 1 、5 和 6 都在此列中。
          1 在上面，所以它出现在前面。
          5 和 6 位置都是 (2, 0) ，所以按值从小到大排序，5 在 6 的前面。
列  1 ：只有结点 3 在此列中。
列  2 ：只有结点 7 在此列中。
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2021/01/29/vtree3.jpg)

```
输入：root = [1,2,3,4,6,5,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
这个示例实际上与示例 2 完全相同，只是结点 5 和 6 在树中的位置发生了交换。
因为 5 和 6 的位置仍然相同，所以答案保持不变，仍然按值从小到大排序。
```

 

**提示：**

- 树中结点数目总数在范围 `[1, 1000]` 内
- `0 <= Node.val <= 1000`

**思路**

bfs记录每层坐标等信息，然后用treemap将列，行 值放进map进行排序，然后对其排序

**代码**

```java
class Solution {
    class treeTemp{
        Integer row;
        Integer col;
        Integer val;

        public Integer getRow() {
            return row;
        }

        public Integer getCol() {
            return col;
        }

        public Integer getVal() {
            return val;
        }

        public treeTemp(Integer row, Integer col, Integer val) {
            this.row = row;
            this.col = col;
            this.val = val;
        }
    }

    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        if (root == null){
            return ans;
        }
        LinkedList<TreeNode> queue = new LinkedList<>();
        LinkedList<treeTemp> treeQueue = new LinkedList<>();
        Map<Integer, TreeMap<Integer, List<Integer>>> map = new TreeMap<>(Comparator.naturalOrder());
        queue.offer(root);
        treeQueue.offer(new treeTemp(0,0,root.val));
        while (!queue.isEmpty()){
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                treeTemp treeTemp = treeQueue.poll();
                map.putIfAbsent(treeTemp.col, new TreeMap<>());
                map.get(treeTemp.col).putIfAbsent(treeTemp.row, new ArrayList<>());
                map.get(treeTemp.col).get(treeTemp.row).add(treeTemp.val);

                if (node.left != null){
                    queue.offer(node.left);
                    treeQueue.offer(new treeTemp(treeTemp.row + 1,treeTemp.col - 1,node.left.val));
                }
                if (node.right != null){
                    queue.offer(node.right);
                    treeQueue.offer(new treeTemp(treeTemp.row + 1,treeTemp.col + 1,node.right.val));
                }
            }
        }

        for (int col : map.keySet()) {
            List<Integer> level = new ArrayList<>();
            for (List list : map.get(col).values()) {
                Collections.sort(list);
                level.addAll(list);
            }
            ans.add(level);
        }

        return ans;
    }
}
```



**复杂度**

时间复杂度：O(N)

空间复杂度：O(N)