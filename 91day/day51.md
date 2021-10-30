#### [1162. 地图分析](https://leetcode-cn.com/problems/as-far-from-land-as-possible/)

难度中等224

你现在手里有一份大小为 N x N 的 网格 `grid`，上面的每个 单元格 都用 `0` 和 `1` 标记好了。其中 `0` 代表海洋，`1` 代表陆地，请你找出一个海洋单元格，这个海洋单元格到离它最近的陆地单元格的距离是最大的。

我们这里说的距离是「曼哈顿距离」（ Manhattan Distance）：`(x0, y0)` 和 `(x1, y1)` 这两个单元格之间的距离是 `|x0 - x1| + |y0 - y1|` 。

如果网格上只有陆地或者海洋，请返回 `-1`。

 

**示例 1：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/08/17/1336_ex1.jpeg)**

```
输入：[[1,0,1],[0,0,0],[1,0,1]]
输出：2
解释： 
海洋单元格 (1, 1) 和所有陆地单元格之间的距离都达到最大，最大距离为 2。
```

**示例 2：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/08/17/1336_ex2.jpeg)**

```
输入：[[1,0,0],[0,0,0],[0,0,0]]
输出：4
解释： 
海洋单元格 (2, 2) 和所有陆地单元格之间的距离都达到最大，最大距离为 4。
```

 

**提示：**

1. `1 <= grid.length == grid[0].length <= 100`
2. `grid[i][j]` 不是 `0` 就是 `1`



**思路**

多源bfs

**代码**

```java
class Solution {
    // 本题是典型的多源头bfs  和单bfs区别是 队列开始就有一系列点 而不是1个点
    // 技巧  使用grid[x][y] 是否等于 0 判断是否被访问过以及是否是陆地
    final int[][] moves = new int[][] {{1,0},{-1,0},{0,1},{0,-1}};
    public int maxDistance(int[][] grid) {
        int max = -1, n = grid.length;
        Queue<int[]> queue = new LinkedList<>();
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j ++) {
                if(grid[i][j] == 1) {
                   queue.offer(new int[]{i, j}); 
                }
            }
        }

        if(queue.size() == 0 || queue.size() == n * n ) return -1; // 只有陆地或者海洋
        int[] cur = null;
        while(!queue.isEmpty()) {
            cur = queue.poll();
            for(int i = 0 ; i< 4 ;i++) {  // 遍历其他的海洋  遇到陆地或者被遍历过的海洋就跳过
                int nextX = cur[0] + moves[i][0];
                int nextY = cur[1] + moves[i][1];
                if( nextX < 0 || nextX >= n || nextY < 0 || nextY >= n || grid[nextX][nextY] > 0) continue; // grid[nextX][nextY] > 0 表示陆地点或者是已经被其他到这个海洋点更近的陆地点bfs访问过   题目中 ： 这个海洋单元格到离它最近的陆地单元格的距离是最大
                grid[nextX][nextY] = grid[cur[0]][cur[1]] + 1; // 传播的过程 + 1
                queue.offer(new int[]{nextX, nextY});
            } 
            
        }
        return grid[cur[0]][cur[1]] - 1;   // 距离包含了陆地的1
    }
}
```

**复杂度**

时间复杂度：O(N^2)

空间复杂度：O(N^2)