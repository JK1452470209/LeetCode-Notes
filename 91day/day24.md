【Day 24】Delete Sublist to Make Sum Divisible By K

https://binarysearch.com/problems/Delete-Sublist-to-Make-Sum-Divisible-By-K

```
​```
You are given a list of positive integers nums and a positive integer k. Return the length of the shortest sublist (can be empty sublist ) you can delete such that the resulting list's sum is divisible by k. You cannot delete the entire list. If it's not possible, return -1.

Constraints

1 ≤ n ≤ 100,000 where n is the length of nums
Example 1
Input
nums = [1, 8, 6, 4, 5]
k = 7
Output
2
Explanation
We can remove the sublist [6, 4] to get [1, 8, 5] which sums to 14 and is divisible by 7.
​```
```

**思路**

- 由前缀和我们知道子数组 A[i:j] 的和就是 pres[j] - pres[i-1]，其中 pres 为 A 的前缀和。
- 由同余定理我们知道两个模 k 余数相同的数字相减，得到的值定可以被 k 整除。

**注：-1 % 4 在 Java 中为-1，而我们期望为 3，为了解决正负数求余统一，采用 Math.floorMod**

**代码**

```java
class Solution {

    public int solve(int[] nums, int k) {

        int tar = 0;

        for (int n : nums)
            tar += n;

        tar = Math.floorMod(tar, k);

        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);

        int prefix = 0, res = nums.length;

        for (int i = 0; i < nums.length; i++) {

            prefix += nums[i];
            int mod = Math.floorMod(prefix, k);
            map.put(mod, i);

            if (map.containsKey(Math.floorMod(prefix - tar, k)))
                res = Math.min(res, i - map.get(Math.floorMod(prefix - tar, k)));
        }

        return res == nums.length ? -1 : res;
    }
}

```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(min（N,k）)