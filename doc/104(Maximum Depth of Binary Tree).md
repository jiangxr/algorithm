### Maximum Depth of Binary Tree
说明： 找出二叉树的最大深度。

分析：最大深度，找到每一条路径的深度即可。

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null)
            return 0;
        int leftMaxDepth = maxDepth(root.left);
        int rightMaxDepth = maxDepth(root.right);
        return (leftMaxDepth > rightMaxDepth? leftMaxDepth:rightMaxDepth) + 1;
    }
}
```
