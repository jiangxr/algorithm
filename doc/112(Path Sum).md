### Path Sum

说明： 给定一个数字，问是否存在一个从根节点到叶子节点的元素之和等于这个值

分析：这道题说到底还是明白如何对树进行遍历，并且终止条件是什么。当我们找到这样的路径
时，应该立即终止其他的递归。

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)
            return false;

        return hasPath(root, sum);

    }

    public boolean hasPath(TreeNode node, int sum) {
        if(node.left == null && node.right == null) {
            if(sum == node.val)
                return true;
            else
                return false;
        }

        if(node.left == null)
            return hasPath(node.right, sum - node.val);
        if(node.right == null)
            return hasPath(node.left, sum - node.val);
        return hasPath(node.left, sum - node.val) || hasPath(node.right, sum - node.val);
    }
}
```

网上的解法：

方法一：其实和我的思路一样，写法稍微简化了些。
```java
public class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null) return false;

        if(root.left == null && root.right == null && sum - root.val == 0) return true;

        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```
方法二： 利用后序遍历
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        Stack<TreeNode> s = new Stack<>();
        TreeNode pre = null;
        TreeNode cur = root;
        int total = 0;
        while(cur != null || !s.empty()) {
            while(cur != null) {
                s.push(cur);
                total += cur.val;
                cur = cur.left;
            }
            cur = s.peek();
            if(cur.left == null && cur.right == null && total == sum)
                return true;
            if(cur.right  != null && pre != cur.right)
                cur = cur.right;
            else {
                pre = cur;
                s.pop();
                total -= cur.val;
                cur = null;
            }
        }
        return false;

    }

}
```
