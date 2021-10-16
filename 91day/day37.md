#### [69. Sqrt(x)](https://leetcode-cn.com/problems/sqrtx/)

难度简单802

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留 **整数部分** ，小数部分将被 **舍去 。**

**注意：**不允许使用任何内置指数函数和算符，例如 `pow(x, 0.5)` 或者 `x ** 0.5` 。

 

**示例 1：**

```
输入：x = 4
输出：2
```

**示例 2：**

```
输入：x = 8
输出：2
解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
```

 

**提示：**

- `0 <= x <= 231 - 1`

**思路**

二分搜索

**代码**

```java
class Solution {
    public int mySqrt(int x) {
        int left = 0,right = x;
        if(x == 0 || x == 1){
            return x;
        }
        while(left + 1 < right){
            int mid = left + (right - left)/2;
            if(mid >= x/mid){
                if(mid == x/mid){
                    return mid;
                }
                right = mid;
            }else{
                left = mid;
            }
        }
        return left;
    }
}
```

**复杂度**

时间复杂度：O(logN)

空间复杂度：O(1)