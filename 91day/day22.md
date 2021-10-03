#### [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

难度中等6181

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

 

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

**示例 4:**

```
输入: s = ""
输出: 0
```

 

**提示：**

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成

**思路**

暴力循环，对字符串进行扫描，用set存储每轮是否有重复字符串，出现重复字符串跳往下一轮，长度计算用第二个循环指针减去第一个循环指针位置+1

**代码**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int ret = 0;
        for (int i = 0; i < s.length(); i++) {
            HashSet<Character> set = new HashSet<>();
            for (int j = i; j < s.length(); j++) {
                if (set.contains(s.charAt(j))){
                    break;
                }
                set.add(s.charAt(j));
                ret = Math.max(ret,j - i + 1);
            }
        }
        return ret;
    }
}
```



**复杂度**

时间复杂度：O(N^2),N为字符串长度

空间复杂度：O(1)

**思路**

滑动窗口，哈希表，维护一个滑动窗口，遇到字符存进map里并记录下标，如果再下次遇到map中存在的字符，将左边的窗口收缩（指针移动），将左边的指针移动到上一次遇到该字符位置+1.注意在移动左边指针时，保证移动位置在滑动窗口中。如果不在则更新map里该字符的位置。

**代码**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        int max_len = 0,left = 0,right = 0;
        while (right < s.length()){
            if (map.containsKey(s.charAt(right))){
                int last_pos = map.get(s.charAt(right));
                if (last_pos >= left && last_pos <= right){
                    left = last_pos + 1;
                }
            }
            max_len = Math.max(max_len,right - left + 1);
            map.put(s.charAt(right),right);
            right++;
        }
        return max_len;
    }
}
```

**复杂度**

时间复杂度：O(N)，N为字符串长度

空间复杂度：O(S),S为map中字符集的个数