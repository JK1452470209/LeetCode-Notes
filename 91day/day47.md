**【Day 47】Number of Operations to Decrement Target to Zero**

```
You are given a list of positive integers nums and an integer target. Consider an operation where we remove a number v from either the front or the back of nums and decrement target by v.

Return the minimum number of operations required to decrement target to zero. If it's not possible, return -1.

Constraints

n ≤ 100,000 where n is the length of nums
Example 1
Input
nums = [3, 1, 1, 2, 5, 1, 1]
target = 7
Output
3
Explanation
We can remove 1, 1 and 5 from the back to decrement target to zero.

Example 2
Input
nums = [2, 4]
target = 7
Output
-1
Explanation
There's no way to decrement target = 7 to zero.
```

**思路**

只能获取俩遍数。转换思路为获取数组中长度可变的窗口 

**代码**

```java
public int solve(int[] nums,int target){
        int left = 0,right = 0,sum = 0;
        int len = Integer.MAX_VALUE;
        while (right < nums.length){
            if (sum < target) {
                sum += nums[right];
                right++;
            }else if (sum >= target && left < right){

                if (sum == target){
                    len =  Math.min(len,left + nums.length - right);
                    System.out.println(left + "   " + right);
                }
                sum -= nums[left];
                left++;
            }
        }

        return len == 0 ? -1:len;
    }
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)