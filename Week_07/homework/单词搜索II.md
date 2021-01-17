**单词搜索II**

**题目：**

给定一个 m x n 二维字符网格 board 和一个单词（字符串）列表 words，找出所有同时在二维网格和字典中出现的单词。

单词必须按照字母顺序，通过 相邻的单元格 内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母在一个单词中不允许被重复使用

**解法一： DFS + Trie**

```java
class Solution {
    private List<String> result = new ArrayList<>();
    public List<String> findWords(char[][] board, String[] words) {
        //构造字典树， 遍历board，调用dfs进行搜索和比较
        TrieNode root = buildTrie(words);
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                dfs(board, i, j, root);
            }
        }
        return result;
    }

    private void dfs(char[][] board, int i, int j, TrieNode root) {
        char c = board[i][j];
        if (c == '#' || root.next[c - 'a'] == null) {
            return;
        }
        TrieNode p = root.next[c - 'a'];
        if (p.word != null) {
            result.add(p.word);
            p.word = null;
        }

        board[i][j] = '#';
        if (i > 0){
            dfs(board, i - 1, j, p);
        }
        if (j > 0) {
            dfs(board, i, j - 1, p);
        }
        if (i < board.length - 1) {
            dfs(board, i + 1, j, p);
        }
        if (j < board[0].length - 1) {
            dfs(board, i, j + 1, p);
        }
        board[i][j] = c;
    }




    private TrieNode buildTrie(String[] words) {
        TrieNode root = new TrieNode();
        for (String s : words) {
            TrieNode p = root;
            char[] chars = s.toCharArray();
            for (char c : chars) {
                if (p.next[c - 'a'] == null){
                    p.next[c - 'a'] = new TrieNode();
                }
                p = p.next[c - 'a'];
            }
            p.word = s;
        }
        return root;
    }

    class TrieNode {
        TrieNode[] next = new TrieNode[26];
        String word;
    }
}
```

时间复杂度： 构造Trie为O（mn），m为单词数组的长度，n为单词数组中单词的长度，遍历board为O（mn），dfs中要向上下左右四个方向都遍历一遍，且遍历Trie中的节点的长度，即n的4次方（最差情况下），即O（mn*n^4），实际中效率要比这种情况高。

空间复杂度：O（mn），即构造Trie所用的空间。