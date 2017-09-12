### Linked List Cycle II

说明： 如果一个链表中存在环，找到这个环的起始节点

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head == null)
            return null;
        ListNode p = head;
        ListNode q = head;
        boolean isCycle = false;
        while(q.next != null && q.next.next != null) {
            p = p.next;
            q = q.next.next;
            if(p == q) {
                isCycle = true;
                break;
            }
        }
        if(isCycle) {
          p = head;
          while(p != q) {
              p = p.next;
              q = q.next;
          }
            return p;
        }
        return null;
    }
}
```
