**N叉树的后序遍历**

**题目:**给定一个 N 叉树，返回其节点值的*后序遍历*。

**解法一: 递归**

```java
class Solution {

    private List<Integer> result = new LinkedList<>();

    public List<Integer> postorder(Node root) {
        if (root == null) {
            return result;
        }

        for (Node node : root.children) {
            postorder(node);
        }
        result.add(root.val);

        return result;
    }
}
```

时间复杂度: O(n)

空间复杂度: O(n)



**解法二: 迭代**

```java
class Solution {

    private List<Integer> result = new LinkedList<>();

    public List<Integer> postorder(Node root) {
        if (root == null) {
            return result;
        }

        Stack<Node> stack = new Stack<Node>();
        stack.push(root);
        while (!stack.isEmpty()) {
            root = stack.pop();
            result.add(0, root.val);

            for (int i = 0; i < root.children.size(); i++) {
                stack.push(root.children.get(i));
            }
        }
        return result;
    }
}
```

时间复杂度: O(n)

空间复杂度:O(n)