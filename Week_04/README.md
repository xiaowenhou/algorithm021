学习笔记

- 使用二分查找，寻找一个半有序数组 [4, 5, 6, 7, 0, 1, 2] 中间无序的地方
  由于半有序的数组实际上还是两个有序的数组，因此首先想到的还是二分查找，一开始先把二分查找的代码模板写上， 然后再修改条件。

  通过观察可以发现， 发生无序的地方只可能在一边， 因此还是可以通过条件判断来排除掉一半的元素。

  如果发生无序的地方在mid左侧， 那么nums[mid]会既小于nums[left]， 又小于nums[right]，说明从mid到right之间的数组已经是有序的， 此时继续向左查找， 更新right为mid -1；如果发生无序的地方在mid的右侧，那么nums[mid]会既大于nums[left]，又大于nums[right]，说明从mid到left之间的数组已经是有序的，此时继续向右查找， 更新left为mid+1；

  如此循环下去， 直到left和right分别指向发生无序的地方，left和right相邻为止。

  ```java
  private int findIndex(int[] nums)  {
      int left = 0;
      int right = nums.length - 1;
      //right - left等于1时， 即说明left和right相邻
      while (right - left > 1) {
          int mid = (left + right) / 2;
          if (nums[mid] > nums[left] && nums[mid] > nums[right]){
              left = mid;
          } else if (nums[mid] < nums[left] && nums[mid] < nums[right]) {
              right = mid;
          }
      }
  
     return left;
  }
  ```