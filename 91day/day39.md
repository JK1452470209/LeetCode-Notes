# 762.Number Stream to Intervals

## 入选理由

暂无

## 题目地址

https://binarysearch.com/problems/Triple-Inversion

## 前置知识

- 二分法

## 题目描述

```
Given a list of integers nums, return the number of pairs i < j such that nums[i] > nums[j] * 3.

Constraints

n ≤ 100,000 where n is the length of nums
Example 1
Input
nums = [7, 1, 2]
Output
2
Explanation
We have the pairs (7, 1) and (7, 2)
```

**思路**

遍历数组，用TreeMap存储已经遍历过的元素和元素出现的个数，用tailMap(K fromKey, boolean inclusive)寻找所有满足条件的值，将值的总和加到结果中。

**代码**

```java
class Solution {
    public int solve(int[] nums) {
        if (nums.length == 0) return 0;
        int res = 0;
        TreeMap<Integer, Integer> map = new TreeMap<>();
        map.put(nums[0], 1);
        for (int i = 1; i < nums.length; i++) {
            Map<Integer, Integer> candidates = map.tailMap(3 * nums[i], false);
            for (Map.Entry<Integer, Integer> entry: candidates.entrySet()) {
                res += entry.getValue();
            }
            map.put(nums[i], map.getOrDefault(nums[i], 0) + 1);
        }
        return res;        
    }
}
```

**复杂度**

时间复杂度：O(NlogN)

空间复杂度：O(N)