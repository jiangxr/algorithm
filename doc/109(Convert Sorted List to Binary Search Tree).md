### Convert Sorted List to Binary Search Tree

说明：将一个排序好的链表转为高度平衡的二叉排序树

分析：因为是链表类型，所以，查找数据的速度过慢，所以首先将链表转为ArrayList,使查找的时间复杂度
为O(1)。然后使用和上题完全相同的解法即可。

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if(head == null)
            return null;
        List<Integer> list = new ArrayList<>();
        ListNode p = head;
        while(p != null) {
            list.add(p.val);
            p = p.next;
        }
        return generateTree(list, 0, list.size() - 1);

    }

    private TreeNode generateTree(List<Integer> list, int lo, int hi) {
        if(lo > hi)
            return null;
        int mid = (lo + hi) >> 1;
        TreeNode head = new TreeNode(list.get(mid));
        head.left = generateTree(list, lo, mid -1);
        head.right = generateTree(list, mid + 1, hi);
        return head;
    }
}
```
