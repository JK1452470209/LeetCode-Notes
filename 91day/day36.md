#### [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/)

难度中等396收藏分享切换为英文接收动态反馈

给你一个整数数组 `nums`，请你将该数组升序排列。

**示例 1：**

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]
```

**示例 2：**

```
输入：nums = [5,1,1,2,0,0]
输出：[0,0,1,1,2,5]
```

 

**提示：**

1. `1 <= nums.length <= 50000`
2. `-50000 <= nums[i] <= 50000`

**思路**

内置api，嘿嘿

**代码**

```java
class Solution {
    public int[] sortArray(int[] nums) {
        Arrays.sort(nums);
        return nums;
    }
}
```

**复杂度**

时间复杂度：O(NlogN)，最差O(N^2)

空间复杂度：O(1)

**思路**

快速排序

**代码**

```java
class Solution {
    public int[] sortArray(int[] nums) {
        quickSort(nums,0,nums.length - 1);
        return nums;
    }

    private void quickSort(int[] nums,int low,int high){
        if (low < high){
            int index = partition(nums,low,high);
            quickSort(nums,low,index - 1);
            quickSort(nums,index + 1,high);
        }
    }

    private int partition(int[] nums, int low, int high) {
        int pivot = nums[low];
        while (low < high){
            //从右边开始扫描，扫比出pivot小的
            while (low < high && pivot <= nums[high]){
                high--;
            }
            //此时high是小于pivot的下标，移动到pivot处
            if (low < high){
                nums[low] = nums[high];
            }
            //从左边开始扫描，扫出比pivot大的
            while (low < high && pivot >= nums[low]){
                low++;
            }
            //此时low是大于pivot的下标，移动到high处
            if (low < high){
                nums[high] = nums[low];
            }
            //将pivot回填到正确位置
            nums[low] = pivot;
        }

        return low;
    }
}
```

**复杂度**

时间复杂度：O(NlogN)，最差O(N^2)

空间复杂度：O(1)