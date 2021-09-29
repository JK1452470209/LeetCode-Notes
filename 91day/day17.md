#### [297. 二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

难度困难645收藏分享切换为英文接收动态反馈

序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**提示:** 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 [LeetCode 序列化二叉树的格式](https://leetcode-cn.com/faq/#binary-tree)。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg)

```
输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
```

**示例 2：**

```
输入：root = []
输出：[]
```

**示例 3：**

```
输入：root = [1]
输出：[1]
```

**示例 4：**

```
输入：root = [1,2]
输出：[1,2]
```

 

**提示：**

- 树中结点数在范围 `[0, 104]` 内
- `-1000 <= Node.val <= 1000`

**思路**

记录左右节点值，关键在于把树当作完全二叉树。一个节点的编号是 i，那么其左子节点就是 2 * i，右子节点就是 2 * i + 1。

**代码**

```java
public class Codec {

    public String serialize(TreeNode root) {
        String ans = "";
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()){
            TreeNode node = queue.poll();
            if (node != null){
                ans += node.val + ",";
                queue.offer(node.left);
                queue.offer(node.right);
            }else {
                ans += "#,";
            }
        }
        return ans.substring(0,ans.length() - 1);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        
        if ("#".equals(data)){
            return null;
        }
        String[] nodes = data.split(",");
        TreeNode des = new TreeNode(Integer.valueOf(nodes[0]));
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.offer(des);
        int i = 1;
        while (i < nodes.length - 1){
            TreeNode node = queue.poll();
            String lv = nodes[i];
            String rv = nodes[i + 1];
            i += 2;
            if (!"#".equals(lv)){
                TreeNode l = new TreeNode(Integer.valueOf(lv));
                node.left = l;
                queue.offer(l);
            }
            if (!"#".equals(rv)){
                TreeNode r = new TreeNode(Integer.valueOf(rv));
                node.right = r;
                queue.offer(r);
            }
        }
        return des;
    }
}
```

**复杂度**

时间复杂度：O(N)，其中 N 为树的节点总数

空间复杂度：O(Q)，满二叉树时 Q=N N为节点总数