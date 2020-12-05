**学习笔记**

**第一周学习总结**

1. **改写deque的API代码**

   ​	老实现:

   ```java
   public class OldDequeue {
   
       public static void main(String[] args) {
           Deque<String> deque = new LinkedList<>();
           deque.push("a");
           deque.push("b");
           deque.push("c");
           System.out.println(deque);
   
           String str = deque.peek();
           System.out.println(str);
           System.out.println(deque);
   
           while (deque.size() > 0) {
               System.out.println(deque.pop());
           }
           System.out.println(deque);
       }
   }
   ```

   ​	新实现:

   ```java
   public class NewDequeue {
       public static void main(String[] args) {
           Deque<String> deque = new LinkedList<>();
   
           deque.addFirst("a");
           deque.addFirst("b");
           deque.addFirst("c");
           System.out.println(deque);
   
           String str = deque.peekFirst();
           System.out.println(str);
           System.out.println(deque);
   
           while (deque.size() > 0) {
               System.out.println(deque.removeFirst());
           }
           System.out.println(deque);
       }
   }
   ```



2. **分析 Queue 和 Priority Queue 的源码 (JDK8)**

   Queue: 

   ​	在JDK8中, Queue在java.util包下, 是一个接口, 该接口实现了Collection接口和Iterable接口, 标识Queue是一个可迭代的集合. Queue中定义了操作Queue的六个基本方法(add, offer, remove, poll, element, peek).

   ​	add和offer都是向Queue中添加元素, 区别在于如果队列已满, add方法会直接抛出异常, 而offer方法会返回false;

   ​	remove和poll都是将队列头部的元素返回并删除, 区别在于如果队列为空, remove会直接抛出异常, 而poll方法会返回null;

   ​	element和peek都是返回队列头部的元素, 但是并不删除队列中的元素,区别在于如果队列为空, element会直接抛出异常, 而peek方法会返回null;

   ​	Queue有四个子接口, BlockingDeque(阻塞双端队列), BlockingQueue(阻塞队列), Deque(双端队列), TransferQueue(传输队列), 这些子接口在Queue的基础上进一步丰富了Queue的功能, 子接口下还有十几个实现类, 这些实现类都实现了更加丰富和强大的功能供开发人员在各个场景下使用.比如常见的ArrayBlockingQueue, ConcurrentLinkedQueue,LinkedBlockingQueue, LinkedList, PriorityQueue等都是Queue的实现类.

   ​	

   PriorityQueue:

   ​	PriorityQueue是AbstractQueue的子类, 也是Queue的实现类. PriorityQueue能够实现按照元素的优先级进行排序存储. 

   ​	Priority内部通过一个Object[]存放元素, 并且在添加元素和删除元素时都会再次对队列中的元素进行优先级排序. 如果元素已经实现了comparator方法, 则使用comparator方法对队列中的元素重新排序, 如果没有实现comparator方法, 则按照自然顺序排序.

   ​	添加元素时, 如果队列空间不足, PriorityQueue会进行扩容, 当队列长度小于64时, 会扩容一倍; 当队列长度大于64时, 会扩容50%.

   

3. **总结**

   五毒神掌: 即一道题至少过遍数过五遍, 每一遍写完代码仅仅完成了这一遍的50%, 还要进一步看力扣中文站和国际站上同语言票数高的代码寻求主动反馈后才算一遍彻底完成.

   ​	第一遍: 初次看到该题, 思考五分钟, 如果有思路, 则实现, 如果没有思路, 直接看题解, 先广度优先, 学习别人的思路和代码之后,  默写代码.

   ​	第二遍: 不看题解, 自己思考实现

   ​	第三遍: 24小时之后, 再实现一遍

   ​	第四遍: 一周之后, 再实现一遍

   ​	第五遍: 面试前前, 再实现一遍

   

   切题四件套: 面试中具体解题时的步骤

    1. 审题, 针对题目的细节和面试官进行沟通, 确保自己对题目理解没有歧义

    2. 列出所有可能的解法, 对每一个解法都和面试官进行简单的讲解(大概实现, 时间复杂度, 空间复杂度), 选出最优解

    3. 写代码

    4. 给出几个测试样例

       切题四件套实际上也是在工作中面临一个新的任务时的常见解决方式, 首先要和领导沟通清楚任务的关键要素, 例如时间节点, 任务背景, 可用的资源, 要达到的目的等, 确保大方向不出问题; 其次是思考出所有能够完成任务的方式(比如所有可以实现某个需求的解决方案), 通过对比, 衡量等确定最合适的解决方案; 接着是动手完成任务; 最后是通过测试或者反馈检验任务完成的结果.

   

   常用套路: 

   ​	数组类的题目, 采用快慢指针求解

   ​		常见代码模板: 一重循环的写法, 两重循环嵌套的写法

   ​	链表类的题目, 一般可以用循环和递归发方式求解

   ​		常见代码模版:  创建一个前置节点指向头结点, 交换节点时的指针操作

   ​	有对称性, 相近性的题目可以考虑栈.
