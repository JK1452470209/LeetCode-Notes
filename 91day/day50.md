```
​```
给定一个包含了一些 0 和 1 的非空二维数组 grid 。
一个 岛屿 是由一些相邻的 1 （代表土地） 构成的组合，
这里的「相邻」要求两个 1 必须在水平或者竖直方向上相邻。
你可以假设 grid 的四个边缘都被 0（代表水）包围着。
找到给定的二维数组中最大的岛屿面积。（如果没有岛屿，则返回面积为 0 。)

示例 1:

[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
对于上面这个给定矩阵应返回 6。注意答案不应该是 11 ，因为岛屿只能包含水平或垂直的四个方向的 1 。

示例 2:

[[0,0,0,0,0,0,0,0]]
对于上面这个给定的矩阵，返回 0。

 
注意：给定的矩阵 grid 的长度和宽度都不超过 50
​```
```

**思路**

(补卡)dfs搜索上下左右，并走过的地点进行标记，保存最大值

**代码**

```java
public int maxAreaOfIsland(int[][] grid){
        int ret = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 0){
                    continue;
                }
                ret = Math.max(ret,dfs(grid,i,j));
            }
        }
        return ret;
    }

    private int dfs(int[][] grid, int row, int col) {
        int n = grid.length;
        int m = grid[0].length;
        if (row > n || row < 0 || col > m || col < 0){
            return 0;
        }
        if (grid[row][col] == 0){
            return 0;
        }
        grid[row][col] = 0;
        return 1 + dfs(grid,row - 1,col) + dfs(grid,row + 1,col) + dfs(grid,row,col - 1) + dfs(grid,row,col + 1);
    }
```



**复杂度**

时间复杂度：O(M*N)

空间复杂度：O(M*N)