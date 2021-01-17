学习笔记

​       实事求是，本周的几个知识点（字典树Trie， 并查集， 双向BFS， 红黑树AVL， 启发式搜索A*）， 只听懂了第一个字典树，其他的要么没听懂， 要么没时间听，因此也只做了两道字典树相关的题目，不过本周做了不少老题，把前几周的题目又基本过了一遍，对一些题目，之前还有些懵懵懂懂， 这次通过再次重复，又加深了记忆和理解， 本周做的新题，也是通过先临摹， 然后再理解的方式直接五毒神掌， 没有浪费时间硬想。

​	   学习就是这样一个从听不懂， 到临摹， 再到枯燥的记忆，然后再到理解，最后再烂熟于心，然后再举一反三的过程，所谓书读百遍，其意自现就是这个道理。 除了学习，其实其他的方面也是一样，要想成为这个方面的专业人士，必须要过这一关，必须要做一些枯燥，反复无聊的基础工作，才能对这个事物有更深层次的理解。比如工作，虽然人人都希望做有挑战性的工作，但是机会有时候也是在日复一日的重复当中发现出来的；再比如投资，想选一只不错的股票，起码要先看完100份财报；想买一套不错的房子， 起码要看完100套房子， 这些基础的工作不累积，过不了这一关， 那么谈任何方法论都是白扯。

​	    到算法刷题也是一样， 现在就是在做打基础的工作，不像写业务逻辑代码那么爽， 但是只有把这些基本的工作坚持做完， 才算是真正的踏入这个专业的领域，现在这个打基础的过程很痛苦，说明现在正在真的成长，而不是像看个一般的视频，看的时候感觉都会，其实只过了个脑瘾，过后就都忘完了，所以还是要坚持，不管再难也要坚持，即使训练营结束之后也要继续刷题，把这些拉下的都一一补上。

​	    这周学习进度确实差强人意，所以这周总结就写一些学习这么长时间的感悟吧，整理好心情再继续努力！



Trie（字典树）

作用：实现快速前缀搜索，完成字符串的快速查询。

特点：一是树的节点不保存字符串，而是保存字符串中的每个字符

​			二是从根节点遍历到叶子节点所经过的路径就组成一个字符串

​			三是从根节点到每个叶子节点表示的字符串都不同

代码模板：

```java
class Trie {
    private Trie[] next;
    private boolean isEnd;

    /**
     * Initialize your data structure here.
     */
    public Trie() {
        this.next = new Trie[26];
        this.isEnd = false;
    }

    /**
     * Inserts a word into the trie.
     */
    public void insert(String word) {
        if (word == null || word.length() < 1) {
            return;
        }
        Trie curr = this;
        char[] words = word.toCharArray();
        for (int i = 0; i < words.length; i++) {
            int n = words[i] - 'a';
            if (curr.next[n] == null) {
                curr.next[n] = new Trie();
            }
            curr = curr.next[n];
        }
        curr.isEnd = true;
    }

    /**
     * Returns if the word is in the trie.
     */
    public boolean search(String word) {
        Trie node = searchPrefix(word);
        return node != null && node.isEnd;
    }

    /**
     * Returns if there is any word in the trie that starts with the given prefix.
     */
    public boolean startsWith(String prefix) {
        Trie node = searchPrefix(prefix);
        return node != null;
    }

    private Trie searchPrefix(String prefix) {
        Trie curr = this;
        char[] chars = prefix.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            curr = curr.next[chars[i] - 'a'];
            if (curr == null) {
                return null;
            }
        }
        return curr;
    }
}
```

 

