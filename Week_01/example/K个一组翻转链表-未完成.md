**K个一组翻转链表**

**题目:**

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

 

示例：

给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5

 

说明：

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。



**解法一:**

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;

        ListNode prev = dummy;
        ListNode end = dummy;
        while (end.next != null) {
            //先向前遍历k个元素
            for (int i = 0; i < k && end != null; i++) {
                end = end.next;
            }
            if(end == null) {
                break;
            }

            //将k个元素反转
            ListNode start = prev.next;
            ListNode next = end.next;
            end.next = null;
            prev.next = reverse(start);

            start.next = next;
            prev = start;
            end = prev;
        }

        return dummy.next;
    }


    private ListNode reverse(ListNode head) {
        ListNode prev = null;

        ListNode curr = head;
        while (curr != null) {
            ListNode next = curr.next;

            curr.next = prev;

            prev = curr;
            curr = next;
        }

        return prev;
    }
}
```



时间复杂度:O(n^2)

空间复杂度:O(1)



**解法二**:递归???

