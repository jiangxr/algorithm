### Insertion Sort List

说明：实现链表的插入排序

我的解决方案：
注：指针的移动一不小心就会错误。请进行注意。
```java
class Solution {
    public ListNode insertionSortList(ListNode head) {
        if(head == null)
            return null;
        if(head.next == null)
            return head;
        ListNode newHead = new ListNode(0);
        newHead.next = head;
        ListNode p = head.next;
        ListNode pre = newHead;
        ListNode q = head;
        q.next = null;
        while(p != null) {
            while(q != null && q.val <= p.val) {
                pre = q;
                q = q.next;
            }

            ListNode pNext = p.next;
            p.next = q;
            pre.next = p;
            p = pNext;
            pre = newHead;
            q = newHead.next;
        }
        return newHead.next;

    }
}
```
