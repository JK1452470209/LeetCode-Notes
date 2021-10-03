#### [30. 串联所有单词的子串](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)

难度困难544

给定一个字符串 `s` 和一些 **长度相同** 的单词 `words` **。**找出 `s` 中恰好可以由 `words` 中所有单词串联形成的子串的起始位置。

注意子串要与 `words` 中的单词完全匹配，**中间不能有其他字符** ，但不需要考虑 `words` 中单词串联的顺序。

 

**示例 1：**

```
输入：s = "barfoothefoobarman", words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
```

**示例 2：**

```
输入：s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
输出：[]
```

**示例 3：**

```
输入：s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
输出：[6,9,12]
```

 

**提示：**

- `1 <= s.length <= 104`
- `s` 由小写英文字母组成
- `1 <= words.length <= 5000`
- `1 <= words[i].length <= 30`
- `words[i]` 由小写英文字母组成

**思路**

暴力枚举匹配，有点滑动窗口的思想。使用哈希表记录单词的频率，然后对字符串进行遍历。每个长度单词相同，让题目更加简单一些 每次对字符串进行一个单词的匹配，如果匹配上就更新频率 使用k标记消除的次数。如果k为0则表示哈希表中全部匹配上

**代码**

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {     
    List<Integer> res = new ArrayList<>();                         
    if ("".equals(s) || words == null){                            
        return res;                                                
    }                                                              
    HashMap<String, Integer> map = new HashMap<>();                
    Integer sum = 0;                                               
    Integer wordLength = words[0].length();                        
    for (String word : words) {                                    
        map.put(word,map.getOrDefault(word,0) + 1);                
        sum += word.length();                                      
    }                                                              
    for (int i = 0; i < s.length() - sum + 1; i++) {               
        Map<String, Integer> copyMap = new HashMap<>(map);         
        int k = words.length;                                      
        int j = i;                                                 
        while (k > 0){                                             
            String str = s.substring(j, j + wordLength);           
            if (!copyMap.containsKey(str) || copyMap.get(str) < 1){
                break;                                             
            }                                                      
            copyMap.put(str,copyMap.get(str) - 1);                 
            k--;                                                   
            j += wordLength;                                       
        }                                                          
        if (k == 0){                                               
            res.add(i);                                            
        }                                                          
    }                                                              
        return res;                                                    
    }                                                                  
}
```

**复杂度**

时间复杂度：O(N^2)

空间复杂度：O(N)