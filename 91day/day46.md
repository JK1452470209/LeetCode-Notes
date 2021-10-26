#### [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)

难度困难1391收藏分享切换为英文接收动态反馈

给你一个字符串 `s` 、一个字符串 `t` 。返回 `s` 中涵盖 `t` 所有字符的最小子串。如果 `s` 中不存在涵盖 `t` 所有字符的子串，则返回空字符串 `""` 。

 

**注意：**

- 对于 `t` 中重复字符，我们寻找的子字符串中该字符数量必须不少于 `t` 中该字符数量。
- 如果 `s` 中存在这样的子串，我们保证它是唯一的答案。

 

**示例 1：**

```
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
```

**示例 2：**

```
输入：s = "a", t = "a"
输出："a"
```

**示例 3:**

```
输入: s = "a", t = "aa"
输出: ""
解释: t 中两个字符 'a' 均应包含在 s 的子串中，
因此没有符合条件的子字符串，返回空字符串。
```

 

**提示：**

- `1 <= s.length, t.length <= 105`
- `s` 和 `t` 由英文字母组成

 

**进阶：**你能设计一个在 `o(n)` 时间内解决此问题的算法吗？

**思路**

一直往右边进行试探匹配到t个字符时，左侧开始收缩。滑动窗口大小不固定，收缩到边界时记录left与right下标。

**代码**

```java
class Solution {
    public String minWindow(String s, String t) {

        Map<Character, Integer> map = new HashMap<>();
        int num = t.length();
        for (int i = 0; i < num; i++)
            map.put(t.charAt(i), map.getOrDefault(t.charAt(i), 0) - 1);
        int len = Integer.MAX_VALUE, match = 0, resLeft = 0, resRight = 0;
        int left = 0, right = 0;
        while (right < s.length()) {
            char ch = s.charAt(right);
            if (map.containsKey(ch)) {
                int val = map.get(ch) + 1;
                if (val <= 0)
                    match++;
                map.put(ch, val);
            }
            while (match == num) {
                if (right - left + 1 < len) {
                    len = right - left + 1;
                    resLeft = left;
                    resRight = right;
                }
                char c = s.charAt(left);
                if (map.containsKey(c)) {
                    int val = map.get(c) - 1;
                    if (val < 0)
                        match--;
                    map.put(c, val);
                }
                left++;
            }
            right++;
        }
        return len == Integer.MAX_VALUE ? "" : s.substring(resLeft, resRight + 1);
    }
}

```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(T)