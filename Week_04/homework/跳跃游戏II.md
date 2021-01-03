**跳跃游戏II**

**题目：**

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。



**解法一：贪心算法**

```java
class Solution {
    public int jump(int[] nums) {
        int step = 0;
        int end = 0;
        int maxIndex = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            maxIndex = Math.max(maxIndex, nums[i] + i);
            if (i == end) {
                end = maxIndex;
                step++;
            }
        }
        return step;
    }
}
```

时间复杂度：O(n)

空间复杂度：O(1)