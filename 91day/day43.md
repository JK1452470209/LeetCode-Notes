#### [1456. 定长子串中元音的最大数目](https://leetcode-cn.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)

难度中等31收藏分享切换为英文接收动态反馈

给你字符串 `s` 和整数 `k` 。

请返回字符串 `s` 中长度为 `k` 的单个子字符串中可能包含的最大元音字母数。

英文中的 **元音字母** 为（`a`, `e`, `i`, `o`, `u`）。

 

**示例 1：**

```
输入：s = "abciiidef", k = 3
输出：3
解释：子字符串 "iii" 包含 3 个元音字母。
```

**示例 2：**

```
输入：s = "aeiou", k = 2
输出：2
解释：任意长度为 2 的子字符串都包含 2 个元音字母。
```

**示例 3：**

```
输入：s = "leetcode", k = 3
输出：2
解释："lee"、"eet" 和 "ode" 都包含 2 个元音字母。
```

**示例 4：**

```
输入：s = "rhythms", k = 4
输出：0
解释：字符串 s 中不含任何元音字母。
```

**示例 5：**

```
输入：s = "tryhard", k = 4
输出：1
```

 

**提示：**

- `1 <= s.length <= 10^5`
- `s` 由小写英文字母组成
- `1 <= k <= s.length`

**思路**

滑动窗口，往右滑动匹配到正确字符则添加 左边边界碰到正确字符对应count-1.每次统计最大count

**代码**

```java
class Solution {
    public int maxVowels(String s, int k) {
        int left = 0,right = 0;
        int count = 0;
        char[] chars = s.toCharArray();

        int tempCount = 0;
        while (right < s.length()) {
            if (chars[right] == 'a' || chars[right] == 'e' || chars[right] == 'i' || chars[right] == 'o' || chars[right] == 'u'){
                tempCount++;
            }
            right++;

            if(right > k) {
                if (chars[left] == 'a' || chars[left] == 'e' || chars[left] == 'i' || chars[left] == 'o' || chars[left] == 'u') {
                    tempCount--;
                }
                left++;
            }
            count = Math.max(count,tempCount);
        }

        System.out.println(count);
        return count;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)