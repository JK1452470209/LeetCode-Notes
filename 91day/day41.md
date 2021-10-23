822. Kth-Pair-Distance

## 入选理由

暂无

## 题目地址

https://binarysearch.com/problems/Kth-Pair-Distance

## 前置知识

- 排序
- 二分法

## 题目描述

```
Given a list of integers nums and an integer k, return the k-th (0-indexed) smallest abs(x - y) for every pair of elements (x, y) in nums. Note that (x, y) and (y, x) are considered the same pair.

Constraints

n ≤ 100,000 where n is the length of nums
Example 1
Input
nums = [1, 5, 3, 2]
k = 3
Output
2
Explanation
Here are all the pair distances:

abs(1 - 5) = 4
abs(1 - 3) = 2
abs(1 - 2) = 1
abs(5 - 3) = 2
abs(5 - 2) = 3
abs(3 - 2) = 1
Sorted in ascending order we have [1, 1, 2, 2, 3, 4].
```

**思路**

暴力枚举所有解，然后排序找出第k个（时间超时

**代码**

```java
public Integer Distance_(int[] ints,int k){
        List<Integer> ret = new ArrayList<>();
        for (int i = 0; i < ints.length; i++) {
            for (int j = i + 1; j < ints.length; j++) {
                ret.add(Math.abs(ints[i] - ints[j]));
            }
        }
        ret.sort(Integer::compareTo);
        return ret.get(k - 1);
    }
```

**复杂度**

时间复杂度：O(N^2)

空间复杂度：O(N)

**思路**

二分+滑动窗口 copy大佬的

**代码**

```java
public int solve(int[] nums, int k) {
        Arrays.sort(nums);
        int absMin = 0;
        int absMax = nums[nums.length-1] - nums[0];

        while (absMin <= absMax) { 
            int absMid = (absMin + absMax) / 2;
            System.out.println("mid: " + absMid);
            if (count(nums, absMid) <= k) {
                absMin = absMid + 1;
            } else {
                absMax = absMid - 1;
            }
        }

        return absMin;
    }

    private long count(int[] nums, int targetDiff) {
        long counter = 0;
        int l = 0;
        for (int r=1; r<nums.length; r++) {
            while (nums[r] - nums[l] > targetDiff) {
                l++;
            }

            counter += r - l;
        }
        return counter;
    }
```

**复杂度**

时间复杂度：O(NlogN)

空间复杂度：O(1)

