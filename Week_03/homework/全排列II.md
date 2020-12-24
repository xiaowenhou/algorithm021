**全排列II**

**题目：**

**解法一：**

```java
class Solution {
    private List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> permuteUnique(int[] nums) {
        //先对数组排序，方便后续剪枝
        Arrays.sort(nums);
        permuteUnique(new boolean[nums.length], nums, new ArrayDeque<>());
        return result;
    }

    private void permuteUnique(boolean[] used, int[] nums, Deque<Integer> deque) {
        //终止条件，当选择的路径等于数组长度时终止
        if (deque.size() == nums.length) {
            result.add(new ArrayList<>(deque));
            return;
        }

        //选择列表，因为没有顺序，所以每次都是全部元素
        for (int i = 0; i < nums.length; i++) {
            //如果之前已经选择过的元素， 则跳过
            if (used[i]) {
                continue;
            }
			//剪枝，如果两个元素的值相同， 并且上一个元素已经被重置， 则可以跳过
            if (i > 0 && nums[i - 1] == nums[i] && !used[i - 1]) {
                continue;
            }

            //做出选择， 并且记录为 已经选择
            used[i] = true;
            deque.addLast(nums[i]);
            permuteUnique(used, nums, deque);
            //撤销选择， 并且将记录也撤销
            used[i] = false;
            deque.removeLast();
        }
    }
}
```

时间复杂度：O()

空间复杂度：O()