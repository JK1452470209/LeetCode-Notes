#### [657. 机器人能否返回原点](https://leetcode-cn.com/problems/robot-return-to-origin/)

难度简单214收藏分享切换为英文接收动态反馈

在二维平面上，有一个机器人从原点 (0, 0) 开始。给出它的移动顺序，判断这个机器人在完成移动后是否在 **(0, 0) 处结束**。

移动顺序由字符串表示。字符 move[i] 表示其第 i 次移动。机器人的有效动作有 `R`（右），`L`（左），`U`（上）和 `D`（下）。如果机器人在完成所有动作后返回原点，则返回 true。否则，返回 false。

**注意：**机器人“面朝”的方向无关紧要。 “R” 将始终使机器人向右移动一次，“L” 将始终向左移动等。此外，假设每次移动机器人的移动幅度相同。

 

**示例 1:**

```
输入: "UD"
输出: true
解释：机器人向上移动一次，然后向下移动一次。所有动作都具有相同的幅度，因此它最终回到它开始的原点。因此，我们返回 true。
```

**示例 2:**

```
输入: "LL"
输出: false
解释：机器人向左移动两次。它最终位于原点的左侧，距原点有两次 “移动” 的距离。我们返回 false，因为它在移动结束时没有返回原点。
```

**思路**

用map存储次数

**代码**

```java
class Solution {
    public boolean judgeCircle(String moves) {
        HashMap<Character,Integer> map = new HashMap();
        map.put('U',0);
        map.put('D',0);
        map.put('R',0);
        map.put('L',0);
        char[] chars = moves.toCharArray();
        for (int i = 0; i < moves.length(); i++) {
            map.put(chars[i],map.getOrDefault(chars[i],0) + 1);
        }
        if (map.get('U').intValue() == map.get('D').intValue() && map.get('R').intValue() == map.get('L').intValue()){
            return true;
        }
        return false;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)



**思路**

用x y记录坐标

**代码**

```java
class Solution {
    public boolean judgeCircle(String moves) {
        int x = 0,y = 0;
        char[] chars = moves.toCharArray();
        for(int i = 0;i < moves.length(); i++){
            if(chars[i] == 'R') x++;
            if(chars[i] == 'L') x--;
            if(chars[i] == 'U') y++;
            if(chars[i] == 'D') y--;
        }
        return x==0 && y==0;
    }
}
```

**复杂度**

时间复杂度：O(N)

空间复杂度：O(1)