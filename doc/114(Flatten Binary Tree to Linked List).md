### Flatten Binary Tree to Linked List

说明： 将树结构转为链式结构

我的解法：使用前序遍历
```java
class Solution {
    public void flatten(TreeNode root) {
        if(root == null)
            return;
        TreeNode pre = null;
        Stack<TreeNode> s = new Stack<>();
        s.push(root);
        TreeNode p = null;
        while(!s.empty()) {
            p = s.pop();
            if(p.right != null)
                s.push(p.right);
            if(p.left != null) {
                s.push(p.left);
                p.left = null;
            }
            if(pre == null) {
                pre = p;
            }else {
                pre.right = p;
                pre = p;
            }
        }
    }
}
```
