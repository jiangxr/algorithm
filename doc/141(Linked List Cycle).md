### Linked List Cycle

说明：不使用额外的存储空间，判断一个链表是否存在环。。

分析：使用两个指针p，q。p指针每次走一步，q指针每次走两步。
如果两个指针能够相遇，则存在环。否则不存在环。

我的解决方法：
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null  || head.next == null)
            return false;
        ListNode p = head;
        ListNode q = head;
        while(p != null && q != null) {
            p = p.next;
            q = q.next;
            if(q == null)
                break;
            q = q.next;
            if(p == q)
                return true;
        }
        return false;
    }
}
```
