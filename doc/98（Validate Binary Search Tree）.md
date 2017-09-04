### Validate Binary Search Tree
说明：判断一棵树是否是二叉搜索树。

我的解法：
直接使用二叉树的中序遍历，如果中序遍历得到的序列是递增的，则这棵树就是二叉搜索树。

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        if(root == null)
            return true;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        TreeNode p = root;
        Integer value = null;
        while(!stack.empty()) {
            if(p != null) {
                while(p.left != null) {
                    stack.push(p.left);
                    p = p.left;
                }
            }
            p = stack.pop();
            if(value != null) {
                if(value >= p.val)
                    return false;
            }
            value = p.val;
            p = p.right;
            if(p != null)
                stack.push(p);


        }
        return true;
    }
}
```
