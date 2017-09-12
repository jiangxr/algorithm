### Copy List with Random Pointer

说明：实现链表的deep copy。其中每个节点多了一个random指针，
随机指向任意的一个元素。

```java
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null)
            return null;
        Map<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode p = head;
        RandomListNode newHead = null;
        RandomListNode q = null;
        while(p != null) {
            RandomListNode newNode = new RandomListNode(p.label);
            map.put(p, newNode);
            if(newHead == null){
                newHead = newNode;
                q = newNode;
            }
            else {
                q.next = newNode;
                q = q.next;
            }
            p = p.next;
        }

        p = head;
        while(p != null) {
            if(p.random != null)
                map.get(p).random = map.get(p.random);
            p = p.next;
        }
        return newHead;
    }
}
```
