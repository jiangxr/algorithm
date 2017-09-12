### Reorder List

说明：给一个链表n0,n1,...nn，将其转为n0,nn,n2,nn-1...

我的解决方案：

```java
class Solution {
    public void reorderList(ListNode head) {
        if(head == null)
            return;
        List<ListNode> list = new ArrayList<>();
        ListNode p = head;
        while(p != null) {
            list.add(p);
            p = p.next;
        }
        int m = 0;
        int i = 0;
        int j = list.size() - 1;
        while(i <= j) {
           if(p == null) {
               p = list.get(i);
               i++;
               m = 1;
           }else {
               if(m == 0) {
                   p.next = list.get(i);
                   i++;
                   m = 1;
                   p = p.next;
                   if(i > j)
                       p.next = null;
               }else {
                   p.next = list.get(j);
                   j--;
                   m = 0;
                   p = p.next;
                   if(i > j)
                       p.next = null;
               }
           }
        }

    }
}
```

网上的解决方法：
方法一：
```java
class Solution {
    public void reorderList(ListNode head) {
        if(head == null || head.next == null)
            return;
        ListNode p1 = head;
        ListNode p2 = head;
        while(p2.next != null && p2.next.next != null) {
            p1 = p1.next;
            p2 = p2.next.next;
        }

        ListNode pre = p1;
        ListNode middle = p1.next;
        while(middle.next != null) {
            ListNode tmp = middle.next;
            middle.next = tmp.next;
            tmp.next = pre.next;
            pre.next = tmp;
        }

        pre = p1;
        p2 = head;
        while(p2 != p1) {
            ListNode tmp = pre.next;
            pre.next = tmp.next;
            tmp.next = p2.next;
            p2.next = tmp;
            p2 = p2.next.next;
        }

    }
}
```
