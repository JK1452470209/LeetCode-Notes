#### [394. 字符串解码](https://leetcode-cn.com/problems/decode-string/)

难度中等876收藏分享切换为英文接收动态反馈

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: `k[encoded_string]`，表示其中方括号内部的 *encoded_string* 正好重复 *k* 次。注意 *k* 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 *k* ，例如不会出现像 `3a` 或 `2[4]` 的输入。

 

**示例 1：**

```
输入：s = "3[a]2[bc]"
输出："aaabcbc"
```

**示例 2：**

```
输入：s = "3[a2[c]]"
输出："accaccacc"
```

**示例 3：**

```
输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
```

**示例 4：**

```
输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
```



**思路**

使用字符栈与数字栈，遇到 **[** 就进栈 遇到 **]** 就出栈，出栈时将字符栈，数字栈同时出栈并运算。还需要考虑数字的进位问题 ret变量缓存着从栈底弹出字符串总和，并且有将字符串压入栈底的作用

**代码**

```java
class Solution {
    public String decodeString(String s) {
        Stack<String> stacks = new Stack<>();
        Stack<Integer> nums = new Stack<>();
        String ret = "";
        int num = 0;
        for (char c : s.toCharArray()){
            if ('0' <= c && c <= '9'){
                num=num*10+c-'0';
            }else if('a' <= c && c <= 'z'){
                ret += c;
            }else if (c == '['){
                stacks.push(ret);
                nums.push(num);
                ret = "";
                num = 0;
            }else {
                Integer cur = nums.pop();
                String stackTemp = stacks.pop();
                for (int i = 0; i < cur; i++) {
                    stackTemp += ret;
                }
                ret = stackTemp;
            }
        }
        return ret;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(N)



**dfs解法**

**思路**

递归写法，注意start变量需要在dfs时同步更新，故使用成员变量

**代码**

```java

class Solution {
    public String decodeString(String s) {
        private int start = 0;
        public String decodeString(String s) {
            return dfs(s.toCharArray());
        }

        private String dfs(char[] s){
            String repeat_str = "", repeat_count = "";
            while (start < s.length){
                if (Character.isDigit(s[start])){
                    repeat_count += s[start];
                }else if (s[start] == '['){
                    start += 1;
                    String t_str = dfs(s);

                    for (Integer i = 0; i < Integer.valueOf(repeat_count); i++) {
                        repeat_str += t_str;
                    }
                    repeat_count = "";
                }else if (s[start] == ']'){
                    return repeat_str;
                }else {
                    repeat_str += s[start];
                }
                start++;
            }
            return repeat_str;
        }
    }
}
```



**复杂度**

时间复杂度：O(N)

空间复杂度：O(N)