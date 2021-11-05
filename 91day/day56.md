#### [673. 最长递增子序列的个数](https://leetcode-cn.com/problems/number-of-longest-increasing-subsequence/)

难度中等495收藏分享切换为英文接收动态反馈

给定一个未排序的整数数组，找到最长递增子序列的个数。

**示例 1:**

```
输入: [1,3,5,4,7]
输出: 2
解释: 有两个最长递增子序列，分别是 [1, 3, 4, 7] 和[1, 3, 5, 7]。
```

**示例 2:**

```
输入: [2,2,2,2,2]
输出: 5
解释: 最长递增子序列的长度是1，并且存在5个子序列的长度为1，因此输出5。
```

**注意:** 给定的数组长度不超过 2000 并且结果一定是32位有符号整数。

**思路**

dp[i]：到nums[i]为止的最长递增子序列长度

count[i]：到nums[i]为止的最长递增子序列个数

*dp*[*i*]=max(*dp*[*j*])+1,其中0≤*j*<*i*且*num*[*j*]<*num*[*i*]

**代码**

```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        int n = nums.length;
        if(n == 1){
            return 1;
        }
        int[] dp = new int[n];
        int[] count = new int[n];
        Arrays.fill(dp, 1);
        Arrays.fill(count, 1);
        int maxLength = 0;

        for(int i = 1; i < n; i++){
            for(int j = 0; j < i; j++){
                //拼接后更长
               if(nums[i] > nums[j]){
                    if(dp[j] + 1 > dp[i]){
                        dp[i] = dp[j] + 1;
                        count[i] = count[j];
                    }
                   //拼接后一样长
                    else if(dp[j] + 1 == dp[i]){
                        count[i] += count[j];
                    }
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }
        int res = 0;
        for(int i = 0; i < n; i++){
            if(dp[i] == maxLength){
                res += count[i];
            }
        }
        return res;
    }
}
```

**复杂度**

时间复杂度：O(N^2)

空间复杂度：O(N)