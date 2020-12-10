**N叉树的前序遍历**

**题目:** 给定一个 N 叉树，返回其节点值的*前序遍历*。

**解法一:**递归

```java
class Solution {

    private List<Integer> result = new ArrayList<>();

    public List<Integer> preorder(Node root) {
        if (root == null) {
            return result;
        }

        result.add(root.val);
        for (Node node : root.children) {
            preorder(node);
        }

        return result;
    }
}
```

时间复杂度: O(n)

空间复杂度:O(n)	



**解法二:** 迭代

```java
class Solution {

    private List<Integer> result = new ArrayList<>();

    public List<Integer> preorder(Node root) {
        if (root == null) {
            return result;
        }

        Stack<Node> stack = new Stack<Node>();
        stack.push(root);
        while (!stack.isEmpty()) {
            root = stack.pop();
            result.add(root.val);

            for (int i = root.children.size() - 1; i >= 0; i--) {
                stack.push(root.children.get(i));
            }
        }

        return result;
    }
}
```

时间复杂度: O(n)

空间复杂度:O(n)