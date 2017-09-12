### Binary Tree Maximum Path Sum

说明：求二叉树中路径的最大值。

分析：求以某个节点为根节点左子树的最大值加上右子树的最大值再加上当前节点，得到一个结果，
对每个节点进行相同的操作。。但是时间复杂度过高。是在不可行。

网上厉害的解法：

方法一：
```java
class Solution {
    int maxValue = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        if(root == null)
            return 0;
        maxPath(root);
        return maxValue;
    }
    //dfs
    public int maxPath(TreeNode node) {
        if(node == null)
            return 0;
        //左子树节点的最大值
        int left = Math.max(0, maxPath(node.left));
        //右子树路径的最大值
        int right = Math.max(0, maxPath(node.right));
        //更新maxValue
        maxValue = Math.max(maxValue, left + right + node.val);
        //当前节点路径的最大值，这一步比较关键，是在头脑转不过弯
        return Math.max(left, right) + node.val;
    }
}
```
