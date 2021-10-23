```
​```
You are given a list of integers nums representing coordinates of houses on a 1-dimensional line. You have 3 street lights that you can put anywhere on the coordinate line and a light at coordinate x lights up houses in [x - r, x + r], inclusive. Return the smallest r required such that we can place the 3 lights and all the houses are lit up.

Constraints

n ≤ 100,000 where n is the length of nums
Example 1
Input
nums = [3, 4, 5, 6]
Output
0.5
Explanation
If we place the lamps on 3.5, 4.5 and 5.5 then with r = 0.5 we can light up all 4 houses.
​```
```

**思路**

能力检测二分，寻找最左符合条件的数。参考大佬答案

**代码**

```java
class Solution {
    public double solve(int[] nums) {
        if(nums.length <= 3) return 0;
        Arrays.sort(nums);

        int l = 0, r = nums[nums.length - 1];

        while(l <= r){
            int m = l + (r - l) / 2;
            
            if(find(m, nums)){
                r = m - 1;
            } else {
                l = m + 1;
            }
        }

        if(l > nums[nums.length - 1] || !find(l, nums)){
            return -1;
        }
        return l / 2.0;
    }

    public boolean find(int mid, int[] nums){
        int range = nums[0]+mid, lights = 0;
        
        for(int i = 0;i < nums.length;i++){
            if(nums[i] > range){
                lights++;
                range = nums[i] + mid;
            }
        }
        

        return lights <= 2;
    }
}
```

**复杂度**

时间复杂度：O(NlogN）

空间复杂度：O(logN)