### Binary Tree Postorder Traversal

说明：二叉树的后续遍历


```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if(root == null)
            return result;
        TreeNode dump = new TreeNode(0);
        dump.left = root;
        TreeNode cur = dump;
        TreeNode prev = null;
        while(cur != null) {
            if(cur.left == null) {
                cur = cur.right;
            }else {
                prev = cur.left;
                while(prev.right != null && prev.right != cur) {
                    prev = prev.right;
                }

                if(prev.right == null) {
                    prev.right = cur;
                    cur = cur.left;
                }else {
                    printReverse(cur.left, prev, result);
                    prev.right = null;
                    cur = cur.right;
                }
            }
        }
        return result;
    }

    private void reverse(TreeNode from, TreeNode to) {
        if(from == to)
            return;
        TreeNode x = from;
        TreeNode y = from.right;
        TreeNode z = null;
        while(true) {
            z = y.right;
            y.right = x;
            x = y;
            y = z;
            if(x == to)
                break;
        }
    }

    private void printReverse(TreeNode from, TreeNode to, List<Integer> list) {
        reverse(from, to);
        TreeNode p = to;
        while(true) {
           list.add(p.val);
            if(p == from) {
                break;
            }
            p = p.right;
        }
        reverse(to, from);
    }

}
```
