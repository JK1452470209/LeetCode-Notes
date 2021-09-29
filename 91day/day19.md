#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

难度简单12218收藏分享切换为英文接收动态反馈

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

 

**提示：**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **只会存在一个有效答案**

**进阶：**你可以想出一个时间复杂度小于 `O(n2)` 的算法吗？

**思路**

暴力循环寻找答案

**代码**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length; i++){
            for(int j = i + 1; j < nums.length; j++){
                if(nums[i] + nums[j] == target){
                    return new int[]{i,j};
                } 
            }
        }
        return null;
    }
}
```

**复杂度**

时间复杂度：O(N^2)，N为数组长度

空间复杂度：O(1)

**思路**

hash表，边存数值边匹配

**代码**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> map = new HashMap();
        for(int i = 0; i < nums.length; i++){
            if(map.containsKey(target - nums[i])){
                Integer temp = map.get(target - nums[i]);
                return new int[]{temp,i};
            }
            map.put(nums[i],i);
        }
        return null;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(N)