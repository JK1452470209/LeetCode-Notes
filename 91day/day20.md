#### [347. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

难度中等870收藏分享切换为英文接收动态反馈

给你一个整数数组 `nums` 和一个整数 `k` ，请你返回其中出现频率前 `k` 高的元素。你可以按 **任意顺序** 返回答案。

 

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

 

**提示：**

- `1 <= nums.length <= 105`
- `k` 的取值范围是 `[1, 数组中不相同的元素的个数]`
- 题目数据保证答案唯一，换句话说，数组中前 `k` 个高频元素的集合是唯一的

 

**进阶：**你所设计算法的时间复杂度 **必须** 优于 `O(n log n)` ，其中 `n` 是数组大小。

**思路**

用hash表存储数据计数数量，并将hash表中的值进行分桶，让次数一样的分在同一个桶中，然后只要倒序把桶中的数转进返回数据即可。

**代码**

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        List<Integer> res = new LinkedList<>();
        List<Integer>[] bucket = new List[nums.length + 1];
        Map<Integer, Integer> counter = new HashMap<>();

        for (int num: nums){
            counter.put(num, counter.getOrDefault(num, 0) + 1);
        }

        for (Map.Entry<Integer, Integer> entry: counter.entrySet()) {
            int val = entry.getValue();
            if (bucket[val] == null){
                bucket[val] = new LinkedList<>();
            }
            bucket[val].add(entry.getKey());
        }

        int kNum = 0;
        for (int i = bucket.length - 1; i >= 0; i--)
            if (bucket[i] != null)
                for (int elem: bucket[i]){
                    res.add(elem);
                    kNum++;
                }
        int[] ret = new int[k];
        for (int i = 0; i < ret.length; i++){
            ret[i] = res.get(i);
        }

        return ret;
    }
}
```

**复杂度**

时间复杂度：O(N)，N为数组的长度

空间复杂度：O(N，N为数组的长度