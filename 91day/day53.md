```
Given a binary tree root, return the top view of the tree, sorted left-to-right.

Constraints

n ≤ 100,000 where n is the number of nodes in root
```

**思路**

用bfs遍历并带列的值，使用hash表存储 如果有则说明该列上面已经有值。最后对hash表进行排序

**代码**

```java
	HashMap<Integer, Integer> map = new HashMap<>();

    public List<Integer> bfs(TreeNode treeNode, Integer pos){
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(treeNode);

        while (!queue.isEmpty()){
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode cur = queue.poll();
                if (!map.containsKey(pos)){
                    map.put(pos,cur.val);
                }
                if (cur.left != null){
                    bfs(cur.left,pos - 1);
                }
                if (cur.right != null){
                    bfs(cur.right,pos + 1);
                }
            }
        }
        return map.entrySet().stream()
                .sorted((entry, entry1) -> Math.max(entry.getKey(), entry1.getKey()))
                .map(Map.Entry::getValue).collect(Collectors.toList());
    }
```

**复杂度**

时间复杂度：O(NlogN)

空间复杂度：O(Q)