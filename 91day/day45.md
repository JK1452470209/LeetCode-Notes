#### [438. 找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

难度中等630

给定两个字符串 `s` 和 `p`，找到 `s` 中所有 `p` 的 **异位词** 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

**异位词** 指由相同字母重排列形成的字符串（包括相同的字符串）。

 

**示例 1:**

```
输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
```

 **示例 2:**

```
输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
```

 

**提示:**

- `1 <= s.length, p.length <= 3 * 104`
- `s` 和 `p` 仅包含小写字母

**思路**

滑动窗口+hash表

**代码**

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> ans = new ArrayList<>();
        HashMap<Character,Integer> map = new HashMap<>();
        char[] chars = p.toCharArray();
        for (char c : chars) {
            map.put(c,map.getOrDefault(c,0) + 1);
        }
        int left = 0;
        int right = 0;
        for (; right < s.length(); right++) {
            char l = s.charAt(left);
            char r = s.charAt(right);
            if (right >= p.length()) {
                if (map.containsKey(l)) map.put(l, map.get(l) + 1);
                else map.put(l, 1);
                if (map.get(l) == 0) map.remove(l);
                left++;
            }
            if (map.containsKey(r)) map.put(r, map.get(r) - 1);
            else map.put(r, -1);
            if (map.get(r) == 0) map.remove(r);

            if (map.size() == 0) ans.add(left);
        }
        return ans;

    }
}
```

**时间复杂度**

时间复杂度：O(N)

空间复杂度：O(1)