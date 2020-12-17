**N叉树的层序遍历**

**题目:**

​	给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）

**解法一: 递归**

```java
class Solution {
    private  List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> levelOrder(Node root) {
       return levelOrder(root, 0);
    }

    List<List<Integer>> levelOrder(Node root, int level) {
        if (root == null) {
            return result;
        }

        if (result.size() <= level) {
            result.add(new ArrayList<>());
        }
        result.get(level).add(root.val);
        for (Node child : root.children) {
            levelOrder(child, level + 1);
        }

        return result;
    }
}
```

时间复杂度:O(n)

空间复杂度: O(n)



**解法二:迭代, 借助队列**

```java
class Solution {

    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int len = queue.size();
            List<Integer> valList = new ArrayList<>();

            for (int i = 0; i < len; i++) {
                Node curr = queue.poll();
                valList.add(curr.val);

                for (Node child : curr.children) {
                    queue.offer(child);
                }
            }
            result.add(valList);
        }

        return result;
    }
}
```

时间复杂度: O(n)

空间复杂度: O(n)