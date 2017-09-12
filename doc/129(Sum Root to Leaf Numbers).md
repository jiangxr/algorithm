### Sum Root to Leaf Numbers

说明：给定一棵二叉树，每个节点的值都是0-9,则从根节点到叶子节点构成
一个数，求所有的这样路径之和。

我的解决方案：
说明：直接使用dfs即可。
```java
class Solution {
    int sum = 0;
    public int sumNumbers(TreeNode root) {
        dfs(root, 0);
        return sum;
    }

    public void dfs(TreeNode root, int total) {
        if(root == null) {
            return;
        }

        if(root.left == null && root.right == null) {
            sum += total * 10 + root.val;
        }
        dfs(root.left, total*10+root.val);
        dfs(root.right, total*10+root.val);
    }
}
```

方法一：dfs
```java
class Solution {
    public int sumNumbers(TreeNode root) {
        if(root == null)
            return 0;
        return dfs(root, 0);
    }

    public int dfs(TreeNode root, int total) {
        if(root.left == null && root.right == null)
            return total * 10 + root.val;
        int val = 0;
        if(root.left != null)
            val += dfs(root.left, total * 10 + root.val);
        if(root.right != null)
            val += dfs(root.right, total * 10 + root.val);
        return val;
    }
}
```

方法二：bfs
```java
class Solution {
    public int sumNumbers(TreeNode root) {
        if(root == null)
            return 0;
        int total = 0;
        Queue<TreeNode> q = new LinkedList<>();
        Queue<Integer> sumQ =  new LinkedList<>();
        q.offer(root);
        sumQ.offer(root.val);
        while(!q.isEmpty()) {
            TreeNode node = q.poll();
            int partialSum = sumQ.poll();
            if(node.left == null && node.right == null)
                total += partialSum;
            if(node.left != null) {
                q.offer(node.left);
                sumQ.offer(partialSum * 10 + node.left.val);
            }

            if(node.right != null) {
                q.offer(node.right);
                sumQ.offer(partialSum * 10 + node.right.val);
            }
        }
        return total;
    }

}
```
