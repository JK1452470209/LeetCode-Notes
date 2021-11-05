```
You are given a two-dimensional list of integers graph representing a directed graph as an adjacency list. You are also given an integer target.

Return the length of a shortest cycle that contains target. If a solution does not exist, return -1.

Constraints

n, m ≤ 250 where n and m are the number of rows and columns in graph
```

**思路**

判断是否有环科院借用visited数组标记，同理找出有环也可以用visited寻找。要找出最短路径 需要记录层数。用bfs会很方便。

**代码**

```java
public int sovle(int[][] graph,int target){
        Queue<Integer> queue = new LinkedList<>();
        HashSet<Integer> visited = new HashSet<>();
        queue.offer(target);
        visited.add(target);
        int level = 0;
        while (!queue.isEmpty()){
            level++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Integer node = queue.poll();
                visited.add(node);
                for (int c_node : graph[node]) {
                    if (visited.contains(c_node)){
                        if (c_node == target){
                            return level;
                        }
                    }else {
                        queue.offer(c_node);
                    }
                }
            }
        }
        return -1;
    }
```

**复杂度**

时间复杂度：O(N)

空间复杂度:	O(N)