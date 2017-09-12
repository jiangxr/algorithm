### Binary Tree Preorder Traversal

说明：二叉树的前序遍历。通常又三种方法。
递归；
利用栈；
利用线索化二叉树的性质。

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if(root == null)
            return result;
        TreeNode p = root;
        while(p != null) {
            if(p.left == null) {
                result.add(p.val);
                p = p.right;
            }else {
                TreeNode q = p.left;
                while(q.right != null && q.right != p) {
                    q = q.right;
                }
                if(q.right == null) {
                    result.add(p.val);
                    q.right = p;
                    p = p.left;
                }else {
                    q.right = null;
                    p = p.right;

                }

            }
        }
        return result;

    }
}
```
