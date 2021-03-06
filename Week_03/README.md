学习笔记

本周数据结构的部分基本上告一段落， 主要是讲算法，包括递归，分治和回溯。分治和回溯的本质也是递归。

递归的关键点在于找到最小最近的重复性， 因为递归的本质是自己调用自己，因此找到了问题的最小最近重复性， 然后不断下探即可以用简单的十几行代码解决一个看似非常复杂的问题。

递归的四要素：

	1. 退出条件， 如果没有退出条件就是死递归了，一定会报错
	2. 当前层的逻辑，就是所谓的最小最近重复性问题的解决逻辑。感觉找到这点是最重要的，在做递归类的题目的时候发现就是无法精准的找到最小最近重复性的问题。
	3. 下探到下一层。注意传递的参数， 有的参数只在当前层有效， 有的则是需要传递到每一层
	4. 存储状态。非必要，但一些复杂的题目中会需要

递归的要点：

1. 不要人肉递归
2. 找最近最小重复性， 即找最小子问题
3. 数学归纳

递归的代码模板

```java
public void recur(int level, int param) {
    //terminator  终止条件
    if (level > MAX_LEVEL) {
        //process result 执行结果
         return;   
    }

    // process current logic  执行当前层的逻辑
    process(level, param);

    //drill down  下到下一层
    recur(level+1, newParam);

    //restore current status存储当前状态
}
```

​       总结：超哥在讲解的时候可以说把递归讲得很清楚了， 但是自己在做递归的题目的时候还是没有抓手，经常出现无处下手一脸懵逼的状况， 要么就是好像有点思路， 但是代码写着写着就写不下去了， 看题解之后感觉恍然大悟，原来并不复杂啊， 但是自己想就是想不到。

​	    后来深入思考之后，发现自己本质的问题还是工作量不够，即递归类的题目还是做的太少， 递归类的题目不像之前的常规题目， 常规题目中的各种数组循环遍历，Map，队列， 栈等在平时开发中也会用到， 但是递归类的题目和解法在实际工作中很少用，因此大脑对于这块的内容就是一个完完全全的初学者。就像我们刚接触代码时， 可能一个简单的Hello world都会出各种问题，稍微复杂一些的问题脑子中就没有思路如何用代码解决， 但是随着练习的增多，慢慢就有感觉了， 那么递归和编程中的其他技能也是如此吧， 想要真正掌握， 能够信手拈来的解决问题，关键就是要过遍数， 要多练， 一直保持大脑对这部分知识和技能的活跃性， 最后才能内化成自己真正能够掌握的东西。

​        分治：分治的本质就是把一个大的问题拆分成各个子问题， 然后子问题求出解之后， 再将子问题的解合并在一起得到最初问题的解。其本质也是递归

​		分治类似递归也有四要素：

   1. 终止条件， 即问题再也无法进行拆分或者得到解决

   2. 当前层的逻辑，即如何拆分问题

   3. 下探到下一层，即子问题再进行拆分

   4. 合并子问题求解的结果

      问题： 自己当前的问题是可以写出来代码的模板， 但是落实到具体的题目， 一是无法直接应用要素去解决问题，二是分析已经知道题解的题目， 也没法将题解拆分成这四部分， 就是还是没有掌握分治解题的套路，究其原因还是练习不够， 做的题目太少

      回溯：回溯是一层一层的试探，在试探的过程中如果发现能够求解则求解， 如果发现不能求解则返回上一层继续试探， 有一种试错的感觉， 最终试出来正确的解法。

​	

测试git提交是否正常