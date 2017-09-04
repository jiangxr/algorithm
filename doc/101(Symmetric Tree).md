### Symmetric Tree

说明：判断一个树是否是对称树。

我的解法：
一眼看去感觉很好解，但是呢，感觉无从下手的样子。然后想着想着有点思路了。主要还是递归的使用。
对于对称的节点，判断其是否值相同即可。

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return back(root, root);

    }

    public boolean back(TreeNode leftNode, TreeNode rightNode) {

        if(leftNode == null && rightNode == null)
            return true;

        if((leftNode == null && rightNode != null) || leftNode != null && rightNode == null )
            return false;

        if(leftNode.val != rightNode.val)
            return false;

        if(back(leftNode.left, rightNode.right) && back(leftNode.right, rightNode.left))
            return true;
        else
            return false;


    }

}
```

网上的解法：
注：网上的解法借助于queue来实现判断，不使用递归的方式。
```java
public boolean isSymmetric(TreeNode root) {
    Queue<TreeNode> q = new LinkedList<>();
    q.add(root);
    q.add(root);
    while (!q.isEmpty()) {
        TreeNode t1 = q.poll();
        TreeNode t2 = q.poll();
        if (t1 == null && t2 == null) continue;
        if (t1 == null || t2 == null) return false;
        if (t1.val != t2.val) return false;
        q.add(t1.left);
        q.add(t2.right);
        q.add(t1.right);
        q.add(t2.left);
    }
    return true;
}
```
