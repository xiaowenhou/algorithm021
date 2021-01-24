**LRU缓存机制**

**题目：**

运用你所掌握的数据结构，设计和实现一个 [LRU (最近最少使用) 缓存机制](https://baike.baidu.com/item/LRU) 。

**解法一： Hash + 双向链表构造LRU缓存**

```java
class LRUCache {
    private Map<Integer, DLinkNode> cache = new HashMap<>();
    private int size;
    private int capacity;
    private DLinkNode head, tail;

    /**
     * 构造函数，创建双向链表
     *
     * @param capacity
     */
    public LRUCache(int capacity) {
        this.size = 0;
        this.capacity = capacity;
        this.head = new DLinkNode();
        this.tail = new DLinkNode();
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        DLinkNode node = cache.get(key);
        if (node == null) {
            return -1;
        }
        moveToHead(node);
        return node.value;
    }

    public void put(int key, int value) {
        DLinkNode node = cache.get(key);
        if (node == null) {//新增
            node = new DLinkNode(key, value);
            cache.put(key, node);
            addToHead(node);
            size++;
            if (size > capacity) {
                DLinkNode tailNode = removeTail();
                cache.remove(tailNode.key);
                size--;
            }
        } else {//更新
            node.value = value;
            moveToHead(node);
        }
    }

    private void moveToHead(DLinkNode node) {
        //这里一定要先删除， 然后再添加， 顺序不能乱
        removeNode(node);
        addToHead(node);
    }

    private void addToHead(DLinkNode node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    private DLinkNode removeTail() {
        DLinkNode node = tail.prev;
        removeNode(node);
        return node;
    }

    private void removeNode(DLinkNode node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private static class DLinkNode {
        int key;
        int value;
        DLinkNode prev;
        DLinkNode next;

        DLinkNode() {

        }
        DLinkNode(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
}
```

