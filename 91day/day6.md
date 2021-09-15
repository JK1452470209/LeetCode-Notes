#### [768. 最多能完成排序的块 II](https://leetcode-cn.com/problems/max-chunks-to-make-sorted-ii/)

难度困难100收藏分享切换为英文接收动态反馈

*这个问题和“最多能完成排序的块”相似，但给定数组中的元素可以重复，输入数组最大长度为`2000`，其中的元素最大为`10**8`。*

`arr`是一个可能包含**重复元素**的整数数组，我们将这个数组分割成几个“块”，并将这些块分别进行排序。之后再连接起来，使得连接的结果和按升序排序后的原数组相同。

我们最多能将数组分成多少块？

**示例 1:**

```
输入: arr = [5,4,3,2,1]
输出: 1
解释:
将数组分成2块或者更多块，都无法得到所需的结果。
例如，分成 [5, 4], [3, 2, 1] 的结果是 [4, 5, 1, 2, 3]，这不是有序的数组。 
```

**示例 2:**

```
输入: arr = [2,1,3,4,4]
输出: 4
解释:
我们可以把它分成两块，例如 [2, 1], [3, 4, 4]。
然而，分成 [2, 1], [3], [4], [4] 可以得到最多的块数。 
```

**注意:**

- `arr`的长度在`[1, 2000]`之间。
- `arr[i]`的大小在`[0, 10**8]`之间。

**思路**

第一道困难题，想不出思路，看了题解才知道。其方法在于排序后，对数的计数时 计数不相等就是不能分块的，计数相等则可以分块。

**代码**

```java
class Solution {
    public int maxChunksToSorted(int[] arr) {
        int[] sorted_arr = arr.clone();
        Arrays.sort(sorted_arr);
        int count = 0,num1 = 0,num2 = 0;
        for (int i = 0; i < arr.length; i++) {
            num1 += arr[i];
            num2 += sorted_arr[i];
            if (num1 == num2){
                count++;
            }
        }
        return count;
    }
}
```

**复杂度**

时间复杂度：O(N^2) 排序加循环

空间复杂度：O(N)



**优化**

使用单调递增栈，维护该数组元素最大值，如果遇到小于前面的数 则将数融合取较大的数

**代码**

```java
class Solution {
    public int maxChunksToSorted(int[] arr) {
        LinkedList<Integer> stack = new LinkedList<>();
        for (int num : arr) {
            if (!stack.isEmpty() && num < stack.getLast()){
                //将最后一个取出
                int cur = stack.removeLast();
                //维持栈的单调递增
                while (!stack.isEmpty() && num < stack.getLast()){
                    stack.removeLast();
                }
                stack.add(cur);
            }else {
                stack.add(num);
            }
        }
        return stack.size();
    }
}
```

**复杂度**

时间复杂度：O(N) 省去了对数组进行排序的时间

空间复杂度：O(N)