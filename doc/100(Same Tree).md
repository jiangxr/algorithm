### Same Tree
说明：判断两个树是否相同。相同是指：结构相同且对应节点的值相同。

递归解法：
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null)
            return true;
        if((p == null && q != null) || (p != null && q == null))
            return false;
        return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```
