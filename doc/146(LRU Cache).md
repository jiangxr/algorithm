### LRU Cache

说明：实现最近最少使用Cache。使其get和put的时间复杂度都是O（1）。

我的解决方案：
我的解决方案严格上来说并不是O（1），但是AC了
```java
class LRUCache {
    Map<Integer, Integer> map = new HashMap<>();
    LinkedList<Integer> list = new LinkedList<>();
    int size = 0;
    private final int capacity;
    public LRUCache(int capacity) {
        this.capacity = capacity;
    }

    public int get(int key) {
        if(capacity <= 0)
            return -1;
        if(map.containsKey(key)) {
            list.remove((Object)key);
            list.addFirst(key);
            return map.get(key);
        }
        else
            return -1;
    }

    public void put(int key, int value) {
        if(capacity <= 0)
            return;
        if(map.containsKey(key)) {
            list.remove((Object)key);
            list.addFirst(key);
            map.put(key, value);
        }
        else {
            if(size == capacity) {
                Integer t = list.removeLast();
                map.remove(t);
                size--;
            }
            map.put(key, value);
            list.addFirst(key);
            size++;
        }
    }
}
```

网上的解决方案：

方法一：
```java
import java.util.*;
class LRUCache {
    private Hashtable<Integer, DLinkNode> cache = new Hashtable<>();
    int count;
    private final int capacity;
    private DLinkNode head, tail;
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.count = 0;
        head = new DLinkNode();
        head.pre = null;
        tail = new DLinkNode();
        tail.post = null;
        head.post = tail;
        tail.pre = head;
    }

    public int get(int key) {
        DLinkNode node = cache.get(key);
        if(node == null)
            return -1;
        this.moveToHead(node);
        return node.value;
    }

    public void put(int key, int value) {
        DLinkNode node = cache.get(key);
        if(node == null) {
            DLinkNode newNode = new DLinkNode();
            newNode.key = key;
            newNode.value = value;
            this.cache.put(key, newNode);
            this.addNode(newNode);
            count++;
            if(count > capacity) {
                DLinkNode tail = this.popTail();
                this.cache.remove(tail.key);
                count--;
            }
        }else {
            node.value = value;
            this.moveToHead(node);
        }

        }

        private void addNode(DLinkNode node) {
            node.pre = head;
            node.post = head.post;
            head.post.pre = node;
            head.post = node;
        }

        private void removeNode(DLinkNode node) {
            DLinkNode pre = node.pre;
            DLinkNode post = node.post;
            pre.post = post;
            post.pre = pre;
        }

        private DLinkNode popTail() {
            DLinkNode res = tail.pre;
            this.removeNode(res);
            return res;
        }

        private void moveToHead(DLinkNode node) {
            this.removeNode(node);
            this.addNode(node);
        }

    private class DLinkNode {
        DLinkNode pre = null;
        DLinkNode post = null;
        int value;
        int key;
    }
}

```
