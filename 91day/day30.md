#### [886. 可能的二分法](https://leetcode-cn.com/problems/possible-bipartition/)

难度中等137收藏分享切换为英文接收动态反馈

给定一组 `N` 人（编号为 `1, 2, ..., N`）， 我们想把每个人分进**任意**大小的两组。

每个人都可能不喜欢其他人，那么他们不应该属于同一组。

形式上，如果 `dislikes[i] = [a, b]`，表示不允许将编号为 `a` 和 `b` 的人归入同一组。

当可以用这种方法将所有人分进两组时，返回 `true`；否则返回 `false`。

 



**示例 1：**

```
输入：N = 4, dislikes = [[1,2],[1,3],[2,4]]
输出：true
解释：group1 [1,4], group2 [2,3]
```

**示例 2：**

```
输入：N = 3, dislikes = [[1,2],[1,3],[2,3]]
输出：false
```

**示例 3：**

```
输入：N = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
输出：false
```

 

**提示：**

- `1 <= N <= 2000`
- `0 <= dislikes.length <= 10000`
- `dislikes[i].length == 2`
- `1 <= dislikes[i][j] <= N`
- `dislikes[i][0] < dislikes[i][1]`
- 对于 `dislikes[i] == dislikes[j]` 不存在 `i != j`

**思路**

图的遍历 染色法

**代码**

```java
class Solution {
    ArrayList<Integer>[] graph;
    Map<Integer, Integer> color;

    public boolean possibleBipartition(int N, int[][] dislikes) {
        graph = new ArrayList[N+1];
        for (int i = 1; i <= N; ++i)
            graph[i] = new ArrayList();

        for (int[] edge: dislikes) {
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }

        color = new HashMap();
        for (int node = 1; node <= N; ++node)
            if (!color.containsKey(node) && !dfs(node, 0))
                return false;
        return true;
    }

    public boolean dfs(int node, int c) {
        if (color.containsKey(node))
            return color.get(node) == c;
        color.put(node, c);

        for (int nei: graph[node])
            if (!dfs(nei, c ^ 1))
                return false;
        return true;
    }
}

```

**复杂度**

时间复杂度：O(E+V）

空间复杂度：O(E+V)