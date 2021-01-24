**学习笔记**

**一、几种简单排序的实现**

**冒泡排序**

```java
public static int[] bubbleSort(int[] nums) {
    for (int i = 0; i < nums.length - 1; i++) {
        for (int j = 0; j < nums.length - 1 - i; j++) {
            if (nums[j] > nums[j + 1]) {
                int temp = nums[j];
                nums[j] = nums[j + 1];
                nums[j + 1] = temp;
            }
        }
    }
    return nums;
}
```

时间复杂度：O（n^2）

空间复杂度：O（1）



**选择排序**

```java
private static int[] selectSort(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
        int minIndex = i;
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] < nums[minIndex]) {
                minIndex = j;
            }
        }

        int temp = nums[minIndex];
        nums[minIndex] = nums[i];
        nums[i] = temp;
    }
    return nums;
}
```

时间复杂度：O（n^2）

空间复杂度：O（1）



**插入排序**

```java
private static int[] insertSort(int[] nums) {
    for (int i = 1; i < nums.length; i++) {
        int preIndex = i - 1;
        int current = nums[i];
        while (preIndex >= 0 && nums[preIndex] > current) {
            nums[preIndex + 1] = nums[preIndex];
            preIndex--;
        }
        nums[preIndex + 1] = current;
    }

    return nums;
}
```

时间复杂度：O（n^2）

空间复杂度：O（1）



**二、几种高级排序的实现**

**快速排序**

```java
public class QuickSortDemo {

    private static void quickSort(int[] array, int begin, int end) {
        if (end <= begin) {
            return;
        }
        int pivot = partition(array, begin, end);
        quickSort(array, begin, pivot - 1);
        quickSort(array, pivot + 1, end);
    }

    private static int partition(int[] array, int begin, int end) {
        int counter = begin;
        //默认标杆为end所在的元素
        for (int i = begin; i < end; i++) {
            //将所有小于标杆的元素都放在标杆前面
            if (array[i] < array[end]) {
                int temp = array[i];
                array[i] = array[counter];
                array[counter++] = temp;
            }
        }

        //将标杆放在它该在的位置
        int temp = array[end];
        array[end] = array[counter];
        array[counter] = temp;
        return counter;
    }

    public static void main(String[] args) {
        int[] nums = new int[]{5, 7, 3, 4, 1, 9, 6, 0, 2};
        quickSort(nums, 0, nums.length - 1);
        Arrays.stream(nums).forEach(System.out::print);
    }
}
```

时间复杂度：最好O（nlogn）， 最差O（n^2）

空间复杂度：O（nlogn）

**归并排序**

```java
public class MergeSortDemo {
    private static void mergeSort(int[] array, int left, int right) {
        if (right <= left) {
            return;
        }

        int mid = (left + right) >> 1;
        //分别对左半边和右半边调用归并排序
        mergeSort(array, left, mid);
        mergeSort(array, mid + 1, right);
        //对排序后的结果进行合并
        merge(array, left, mid, right);
    }

    private static void merge(int[] array, int left, int mid, int right) {
        //定义额外数组，存储合并后的结果
        int[] temp = new int[right - left + 1];
        int i = left, j = mid + 1, k = 0;

        //依次对左半边和右半边进行合并
        while (i <= mid && j <= right) {
            temp[k++] = array[i] <= array[j] ? array[i++] : array[j++];
        }
        //将剩余的元素添加到数组中
        while (i <= mid) {
            temp[k++] = array[i++];
        }
        while (j <= right){
            temp[k++] = array[j++];
        }

        //拷贝回原数组
        System.arraycopy(temp, 0, array, left, temp.length);
    }


    public static void main(String[] args) {
        int[] nums = new int[]{5, 7, 3, 4, 1, 9, 6, 0, 2};
        mergeSort(nums, 0, nums.length - 1);
        Arrays.stream(nums).forEach(System.out::print);
    }
}
```

时间复杂度：O（nlogn）

空间复杂度：O（n）

**堆排序**

```java
public class HeapSortDemo {

    public static void headSort(int[] array) {
        if (array.length == 0) {
            return;
        }

        int length = array.length;
        for (int i = length / 2 - 1; i >= 0; i--) {
            heapify(array, length, i);
        }
        for (int i = length - 1; i >= 0 ; i--) {
            int temp = array[0];
            array[0] = array[i];
            array[i] = temp;
            heapify(array, i, 0);
        }
    }

    private static void heapify(int[] array, int length, int i) {
        int left = 2 * i + 1, right = 2 * i + 2;
        int largest = i;
        if (left < length && array[left] > array[largest]) {
            largest = left;
        }
        if (right < length && array[right] > array[largest]) {
            largest = right;
        }
        if (largest != i) {
            int temp = array[i];
            array[i] = array[largest];
            array[largest] = temp;
            heapify(array, length, largest);
        }
    }

    public static void main(String[] args) {
        int[] nums = new int[]{5, 7, 3, 4, 1, 9, 6, 0, 2};
        headSort(nums);
        Arrays.stream(nums).forEach(System.out::print);
    }
}
```

时间复杂度：O（nlogn）

空间复杂度：O（1）

**三、布隆过滤器**

​        布隆过滤器像是一个门卫， 这个门卫记性非常好， 只要是他见过的， 一定能记住， 如果来一个人他不认识， 那么这个人他肯定没在门卫这里登记过， 但是这个门卫也存在问题，他的眼神不好，有时候会出现认错人的情况， 如果一个人他没在门卫这里登记过， 但是他长得和在门卫这里登记过的某个人非常像，那么他就有可能认错人， 把这个人当作是登记过的人给放进去。

​        布隆过滤器的具体实现是根据算法计算要存储数据的hashcode， 然后将hashcode转换成二进制存储在一个二进制数组中， 具体存储的方式是将对应的二进制数组的相应位标记位1，因为是使用二进制数组， 因此占用的空间非常小， 而且查询效率非常高。当有数据过来判断时， 先计算该数据的hashcode， 然后根据hashcode到二进制数组中相应的位查看， 如果这些位都为1， 则说明该数据在布隆过滤器中存在， 放行， 如果有某个位不为1， 则说明该数据不存在。因为有可能出现不同的数据计算出来的hashcode转换成二进制后恰巧被其他几个数据的二进制位覆盖， 因此布隆过滤器确定存在的值不一定真的存在，其确定不存在的值则一定不存在。

​		布隆过滤器常用在应对缓存击穿时或者网关应用阻挡恶意请求时，能够高效的过滤掉系统中不存在的数据，避免无效的请求打到后台应用。

**四、LRU缓存**

​	    最近最少使用，常用于缓存的淘汰策略。具体实现可以通过HashMap + 双向链表实现，也是大厂常考的一道面试题， 因为一方面可以考察候选者的代码基本功， 另一方面LRU缓存在实际工作中使用的比较多， 比如Redis中内置的缓存淘汰策略中就包括LRU， 以及Mysql的InnoDB引擎，其内存结构中的BufferPool， 在容量不足以容纳下次查询的结果时，会进行刷脏页落盘，具体将哪些脏页移出内存到磁盘也是使用LRU策略。

​		其原理就是Map下挂一个双向链表， 该双向链表有明确的容量， 当有元素插入的时候， 就依次从头部向双向链表中插入一条记录，超出容量时将最后一个节点移出链表，如果对某个元素进行查询，那么将该元素放在链表的头部。通过Map和双向链表的结合， 可以做到插入，查找都是O（1）的时间复杂度。

​		代码模板见题目。

**五、位运算**

​		位运算在实际工作中用的场合也比较多，起码整数除以2可以通过右移一位得到这个用的就很多， 此外由于位运算比较符合计算机的组成规律，因此在一些高质量的框架代码中也经常能够看到位运算， 比如JDK中的HashMap实现中就使用了位运算。位运算的学习主要是多在纸上画出来， 按位计算以及多练。 

**六、本周总结**

​	本周学习的内容相比上一周轻松不少， 因为是平时工作经常接触并且面试常考的问题， 从动力上以及理解上都相比上一周好了不少。此外，现在慢慢看到之前坚持五毒神掌的作用了， 因为一直有坚持做老题，尤其是前两周中学习的链表相关的题目，因此这周学习LRU需要手写双向链表的时候就比较轻松了， 不论是在双向链表的头部添加节点， 还是删除某个节点， 或者移动节点等操作都能很快想出来如何操作，可见学习就是熟能生巧的过程， 不论学习什么都是第一遍是最难的， 但是不断重复重复， 将这个新的知识点和之前的知识点连接在一起以后， 就慢慢搞懂了， 而且会的越多， 学的越快， 因为新的知识更容易和之前的老知识关联起来。

​	    