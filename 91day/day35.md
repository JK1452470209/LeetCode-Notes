#### [1737. 满足三条件之一需改变的最少字符数](https://leetcode-cn.com/problems/change-minimum-characters-to-satisfy-one-of-three-conditions/)

难度中等46收藏分享切换为英文接收动态反馈

给你两个字符串 `a` 和 `b` ，二者均由小写字母组成。一步操作中，你可以将 `a` 或 `b` 中的 **任一字符** 改变为 **任一小写字母** 。

操作的最终目标是满足下列三个条件 **之一** ：

- `a` 中的 **每个字母** 在字母表中 **严格小于** `b` 中的 **每个字母** 。
- `b` 中的 **每个字母** 在字母表中 **严格小于** `a` 中的 **每个字母** 。
- `a` 和 `b` **都** 由 **同一个** 字母组成。

返回达成目标所需的 **最少** 操作数*。*

 

**示例 1：**

```
输入：a = "aba", b = "caa"
输出：2
解释：满足每个条件的最佳方案分别是：
1) 将 b 变为 "ccc"，2 次操作，满足 a 中的每个字母都小于 b 中的每个字母；
2) 将 a 变为 "bbb" 并将 b 变为 "aaa"，3 次操作，满足 b 中的每个字母都小于 a 中的每个字母；
3) 将 a 变为 "aaa" 并将 b 变为 "aaa"，2 次操作，满足 a 和 b 由同一个字母组成。
最佳的方案只需要 2 次操作（满足条件 1 或者条件 3）。
```

**示例 2：**

```
输入：a = "dabadd", b = "cda"
输出：3
解释：满足条件 1 的最佳方案是将 b 变为 "eee" 。
```

 

**提示：**

- `1 <= a.length, b.length <= 105`
- `a` 和 `b` 只由小写字母组成

**思路**

对于情况一情况二采用分桶技术，对于情况三由于字母数量只有26个，直接暴力枚举

**代码**

```java
class Solution {
    public int minCharacters(String a, String b) {
        char[] str1 = a.toCharArray();
        char[] str2 = b.toCharArray();
        int n = str1.length;
        int m = str2.length;
        int[] count1 = new int[26];
        int[] count2 = new int[26];
        //分桶
        for (int i = 0; i < str1.length; i++) {
            count1[str1[i] - 'a']++;
        }
        for (int i = 0; i < str2.length; i++) {
            count2[str2[i] - 'a']++;
        }
        int min = Integer.MAX_VALUE;
        int sum1 = 0,sum2 = 0;
        for (int i = 0; i < 25; i++) {
            sum1 += count1[i];
            sum2 += count2[i];
            min = Math.min(min, sum1 + m - sum2);
            min = Math.min(min, sum2 + n - sum1);
        }
        int max = 0;
        for (int i = 0; i < 26; i++) {
             max = Math.max(max,count1[i] + count2[i]);
        }
        return Math.min(min,m + n - max);
    }
}
```

**复杂度**

时间复杂度:  O(N)

空间复杂度：O(1)