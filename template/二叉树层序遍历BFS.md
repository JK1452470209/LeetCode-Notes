```java
public void BFS(TreeNode root) {
            if (root == null){
                return;
            }
            LinkedList<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
            while (!queue.isEmpty()){
                LinkedList<TreeNode> curs = queue;
                queue = new LinkedList<>();
                //doSomething
                for (TreeNode cur : curs) {
                    if (cur.left != null){
                        queue.offer(cur.left);
                    }
                    if (cur.right != null){
                        queue.offer(cur.right);
                    }
                }
            }
        }
```

