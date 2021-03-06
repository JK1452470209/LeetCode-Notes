#### [989. 数组形式的整数加法](https://leetcode-cn.com/problems/add-to-array-form-of-integer/)

对于非负整数 `X` 而言，*X* 的*数组形式*是每位数字按从左到右的顺序形成的数组。例如，如果 `X = 1231`，那么其数组形式为 `[1,2,3,1]`。

给定非负整数 `X` 的数组形式 `A`，返回整数 `X+K` 的数组形式。

 


**示例 1：**

```
输入：A = [1,2,0,0], K = 34
输出：[1,2,3,4]
解释：1200 + 34 = 1234
```

**示例 2：**

```
输入：A = [2,7,4], K = 181
输出：[4,5,5]
解释：274 + 181 = 455
```

**示例 3：**

```
输入：A = [2,1,5], K = 806
输出：[1,0,2,1]
解释：215 + 806 = 1021
```

**示例 4：**

```
输入：A = [9,9,9,9,9,9,9,9,9,9], K = 1
输出：[1,0,0,0,0,0,0,0,0,0,0]
解释：9999999999 + 1 = 10000000000
```

 

**提示：**

1. `1 <= A.length <= 10000`
2. `0 <= A[i] <= 9`
3. `0 <= K <= 10000`
4. 如果 `A.length > 1`，那么 `A[0] != 0`



**思路**
从个位往后相加(注意进位)并存进list中，最后将list反转
**Java**

```java
class Solution {
    public List<Integer> addToArrayForm(int[] num, int k) {
        List<Integer> ret = new ArrayList<Integer>();
        for (int i = num.length - 1; i >= 0; i--){
            int sum = num[i] + k % 10;
            k /= 10;
            if (sum >= 10){
                k++;
                sum -= 10;
            }
            ret.add(sum);
        }
        //k>num.length情况
        for (;k > 0;k /= 10){
            ret.add(k % 10);
        }
        Collections.reverse(ret);
        return ret;
    }
}
```

**复杂度分析**

- 时间复杂度 :O(N)

- 空间复杂度 :O(1)

ps:时间复杂度以最长的参数计算，反转不知道是否为常数级 空间复杂度只借助了常量级空间。

刚开始知道从数据后面开始计算，只不过一直在纠结10的N次方问题 后来看到题解才知道用%模运算可以完美解决此问题。

