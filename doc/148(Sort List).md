### Sort List

说明：进行链表排序，使用常数级的空间。时间复杂度要求为NlogN

解法：
```java
class Solution {
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode pre = null, slow = head, fast = head;
        while(fast != null && fast.next != null) {
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        pre.next = null;
        ListNode l1 = sortList(head);
        ListNode l2 = sortList(slow);
        return mergeSort(l1, l2);
    }

    public ListNode mergeSort(ListNode node1, ListNode node2) {
        ListNode result = null;
        ListNode p = null;
        while(node1 != null && node2 != null) {
            if(node1.val < node2.val) {
                if(result == null) {
                    result = node1;
                    p  = node1;
                }else {
                    p.next = node1;
                    p = p.next;
                }
                node1 = node1.next;
            }else {
                if(result == null) {
                    result = node2;
                    p = node2;
                }else {
                    p.next = node2;
                    p = p.next;
                }
                node2 = node2.next;
            }
        }

        if(node1 != null)
            p.next = node1;
        if(node2 != null)
            p.next = node2;
        return result;
    }


}
```
