#### [778. 水位上升的泳池中游泳](https://leetcode-cn.com/problems/swim-in-rising-water/)

难度困难196收藏分享切换为英文接收动态反馈

在一个 N x N 的坐标方格 `grid` 中，每一个方格的值 `grid[i][j]` 表示在位置 `(i,j)` 的平台高度。

现在开始下雨了。当时间为 `t` 时，此时雨水导致水池中任意位置的水位为 `t` 。你可以从一个平台游向四周相邻的任意一个平台，但是前提是此时水位必须同时淹没这两个平台。假定你可以瞬间移动无限距离，也就是默认在方格内部游动是不耗时的。当然，在你游泳的时候你必须待在坐标方格里面。

你从坐标方格的左上平台 (0，0) 出发。最少耗时多久你才能到达坐标方格的右下平台 `(N-1, N-1)`？

 

**示例 1:**

```
输入: [[0,2],[1,3]]
输出: 3
解释:
时间为0时，你位于坐标方格的位置为 (0, 0)。
此时你不能游向任意方向，因为四个相邻方向平台的高度都大于当前时间为 0 时的水位。

等时间到达 3 时，你才可以游向平台 (1, 1). 因为此时的水位是 3，坐标方格中的平台没有比水位 3 更高的，所以你可以游向坐标方格中的任意位置
```

**示例2:**

```
输入: [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]
输出: 16
解释:
 0  1  2  3  4
24 23 22 21  5
12 13 14 15 16
11 17 18 19 20
10  9  8  7  6

最终的路线用加粗进行了标记。
我们必须等到时间为 16，此时才能保证平台 (0, 0) 和 (4, 4) 是连通的
```

 

**提示:**

1. `2 <= N <= 50`.
2. `grid[i][j]` 是 `[0, ..., N*N - 1]` 的排列。

**思路**

使用最左二分模板不断尝试更小的数。每次使用bfs对全局进行搜索。

**代码**

```java
class Solution {

    private int N;

    public final int[][] DIRECTIONS = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

    public int swimInWater(int[][] grid) {
        if (grid == null || grid[0] == null){
            return 0;
        }
        this.N = grid.length;
        int left = 0,right = N * N - 1;
        while (left < right){
            int mid = left + (right - left) / 2;
            if (grid[0][0] <= mid && bfs(grid,mid)){
                //尝试比mid小的数 缩小范围
                right = mid;
            }else {
                left = mid + 1;
            }
        }
        return left;
    }
    //每次穷举所有可能小于等于目标值的解
    private boolean bfs(int[][] grid,int target){
        LinkedList<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{0,0});
        //标记
        boolean[][] visited = new boolean[N][N];
        visited[0][0] = true;
        while (!queue.isEmpty()){
            int[] front = queue.poll();
            int x = front[0];
            int y = front[1];
            //尝试四个方向
            for (int[] direction : DIRECTIONS){
                int newX = x + direction[0];
                int newY = y + direction[1];
                if (inArea(newX,newY) && !visited[newX][newY] && grid[newX][newY] <= target){
                    //终点
                    if (newX == N - 1 && newY == N - 1){
                        return true;
                    }
                    queue.offer(new int[]{newX,newY});
                    //标记
                    visited[newX][newY] = true;
                }
            }
        }


        return false;
    }
    
    private boolean inArea(int x,int y){
        return x >= 0 && x < N && y >= 0 && y < N;
    }

}
```

**复杂度**

时间复杂度：O(N^2LogN)

空间复杂度：O(N^2)